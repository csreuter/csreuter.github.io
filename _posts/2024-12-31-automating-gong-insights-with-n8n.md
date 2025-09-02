---
layout: post
title: Automating Gong Insights with n8n
subtitle: Daily quote extraction from sales calls using AI
description: How I built an n8n workflow to automatically extract interesting quotes from Gong sales calls and post them to Slack
tags: [automation, n8n, gong, ai, chatgpt, slack, workflow]
thumbnail-img: /assets/img/n8n-gong.png
share-img: /assets/img/n8n-gong.png
comments: true
---

![n8n workflow](/assets/img/n8n-gong.png)

At CloudQuery, we're lucky enough to have a good volume of organic, inbound calls as well as existing customers that we're in touch with weekly.

## The Challenge

Social proof is one of the best marketing levers we have, but listening to Gong calls takes significant time. While I lean on my sales counterpart to flag calls I should listen to, it became tedious to also extract good customer quotes from those same calls - especially given our volume.

## The Solution: n8n

My friends (and enemies) all know I love [n8n](https://www.n8n.io): a GUI-based workflow tool. With their native support for Gong, Slack, ChatGPT, and custom code functions, it's a no-brainer (for me) to use n8n.

### How It Works

The workflow follows these steps:

1. **Daily Gong Scrape**: Sets a date that is the beginning of the day before, passes that date to Gong's API for listing calls, filters our Outbound calls, and then gets the transcript and participants for each call.
2. **AI Processing**: I have a (chatGPT-created) function call that organizes all of the data into prompts, and then passes that prompt to chatGPT. 

Here's the full prompt:

![Prompt](/assets/img/n8n-prompt.png)

3. **Slack Integration**: At the beginning of the workflow, I post a message to an internal Slack channel. Each quote is then displayed as a threaded response to this message.

![Slack message](/assets/img/n8n-slack.png)


## The n8n Workflow

Here's the complete n8n workflow configuration that powers this automation:

<details>
<summary>Click to expand the full n8n workflow JSON</summary>

{% highlight json %}
{
  "name": "Gong Quote Finder",
  "nodes": [
    {
      "parameters": {
        "filters": {
          "fromDateTime": "={{ $json.oneDayAgo }}"
        },
        "options": {},
        "requestOptions": {}
      },
      "type": "n8n-nodes-base.gong",
      "typeVersion": 1,
      "position": [
        336,
        352
      ],
      "id": "29b6c499-86b4-4882-bee3-2ee389517333",
      "name": "Get calls from past week",
      "credentials": {
        "gongApi": {
          "id": "9oBwBDJJDYXwwDzp",
          "name": "Gong account"
        }
      }
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 2
          },
          "conditions": [
            {
              "id": "c432e990-2116-4150-88db-3688aebc6f69",
              "leftValue": "={{ $json.direction }}",
              "rightValue": "Outbound",
              "operator": {
                "type": "string",
                "operation": "notEquals"
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.filter",
      "typeVersion": 2.2,
      "position": [
        512,
        432
      ],
      "id": "6e52cd80-8540-4a8d-96b4-e7d01cca83eb",
      "name": "Filter Outbound"
    },
    {
      "parameters": {
        "operation": "get",
        "call": {
          "__rl": true,
          "value": "={{ $json.id }}",
          "mode": "id"
        },
        "options": {
          "properties": [
            "transcript",
            "parties"
          ]
        },
        "requestOptions": {}
      },
      "type": "n8n-nodes-base.gong",
      "typeVersion": 1,
      "position": [
        672,
        528
      ],
      "id": "8f4653e0-894b-48c0-a8d8-a6705d450f81",
      "name": "Get transcript and participants",
      "credentials": {
        "gongApi": {
          "id": "9oBwBDJJDYXwwDzp",
          "name": "Gong account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "return items.map(item => {\n  const participants = item.json.parties || [];\n  const transcript = item.json.transcript || [];\n\n  // Build a lookup table { speakerId: name }\n  const speakerMap = {};\n  for (const p of participants) {\n    speakerMap[p.speakerId] = p.name || p.emailAddress || \"Unknown\";\n  }\n\n  // Flatten transcript → \"Name: sentence\"\n  let tStr = \"\";\n  for (const turn of transcript) {\n    const name = speakerMap[turn.speakerId] || \"Unknown\";\n    for (const s of (turn.sentences || [])) {\n      tStr += `${name}: ${s.text}\\n`;\n    }\n  }\n\n  // Participants summary string\n  const pStr = participants\n    .map(p => `${p.name || p.emailAddress} (${p.affiliation || \"\"})`)\n    .join(\", \");\n\n  // Final prompt\n  const prompt = `Participants:\\n${pStr}\\n\\nTranscript:\\n${tStr}`;\n\n  return { json: { ...item.json, prompt } };\n});"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        816,
        608
      ],
      "id": "75a4a69d-18f9-4316-9693-af68e4ce459c",
      "name": "Create prompts",
      "executeOnce": false
    },
    {
      "parameters": {
        "modelId": {
          "__rl": true,
          "value": "gpt-5",
          "mode": "list",
          "cachedResultName": "GPT-5"
        },
        "messages": {
          "values": [
            {
              "content": "=You are analyzing a call transcript. Below is the participant list and the transcript.\n\nYour task: extract only the single best direct quote from a customer (not from CloudQuery employees) that would be most useful for product marketing purposes.\n\nImportant instructions:\n\t•\tChoose the most substantive, impactful quote — the one that best reflects value, pain points, or comparisons.\n\t•\tDo not include more than one quote.\n\t•\tReturn both a direct quote from the customer, and then a paraphrased quote that includes context that we could use on the marketing website.\n\t•\tInclude speaker attribution when possible (which participant said it).\n\t•\tIf no relevant quote is found, return nothing.\n\t•\tReturn the output in the following structured JSON format:\n\n{\n  \"best_quote\": {\n    \"quote\": \"<exact quote>\",\n    \"paraphrased_quote\": \"<paraphrased quote for use in marketing purposes>\",\n    \"speaker\": \"<name>\",\n    \"company\": \"<company>\"\n  }\n\nHere's the transcript and parties:\n{{ $json.prompt }}\n\n}"
            }
          ]
        },
        "jsonOutput": true,
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "typeVersion": 1.8,
      "position": [
        976,
        688
      ],
      "id": "9d05183d-251e-4d4f-94b6-87ff142c0aaf",
      "name": "Have GPT get quotes",
      "credentials": {
        "openAiApi": {
          "id": "Ag7JyI9zZlkCdENC",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "authentication": "oAuth2",
        "select": "channel",
        "channelId": {
          "__rl": true,
          "value": "C0905FL7DNK",
          "mode": "list",
          "cachedResultName": "marketing-team"
        },
        "text": "=:sparkles: Interesting Gong quotes of the week :sparkles:",
        "otherOptions": {
          "includeLinkToWorkflow": false,
          "mrkdwn": true
        }
      },
      "type": "n8n-nodes-base.slack",
      "typeVersion": 2.3,
      "position": [
        0,
        160
      ],
      "id": "26abbca3-8524-4a86-a235-66120af01203",
      "name": "Kickoff message",
      "webhookId": "ee9a7d45-eec8-41c7-8451-035afadcef9a",
      "executeOnce": true,
      "credentials": {
        "slackOAuth2Api": {
          "id": "17AqD8uTrzEnUuGQ",
          "name": "Slack account"
        }
      }
    },
    {
      "parameters": {
        "authentication": "oAuth2",
        "select": "channel",
        "channelId": {
          "__rl": true,
          "value": "C0905FL7DNK",
          "mode": "list",
          "cachedResultName": "marketing-team"
        },
        "text": "=*<{{ $('Get transcript and participants').item.json.metaData.url }}|{{ $('Get transcript and participants').item.json.metaData.title.replace(/[<>|]/g, \"\")}}>*\n\n\"{{ $json.message.content.best_quote.paraphrased_quote }}\"\" \n\n_-{{ $json.message.content.best_quote.speaker }} from {{ $json.message.content.best_quote.company }}_",
        "otherOptions": {
          "includeLinkToWorkflow": false,
          "thread_ts": {
            "replyValues": {
              "thread_ts": "={{ $('Kickoff message').first().json.message_timestamp }}"
            }
          },
          "unfurl_links": false,
          "unfurl_media": false
        }
      },
      "type": "n8n-nodes-base.slack",
      "typeVersion": 2.3,
      "position": [
        1456,
        816
      ],
      "id": "6a7e821e-1725-4204-a414-77af85d22fdf",
      "name": "Reply in thread",
      "webhookId": "ad4d48d7-1be3-4dd8-a177-803effbb8099",
      "credentials": {
        "slackOAuth2Api": {
          "id": "17AqD8uTrzEnUuGQ",
          "name": "Slack account"
        }
      }
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 2
          },
          "conditions": [
            {
              "id": "f7de17b4-44cf-4e07-97d2-e6073174a515",
              "leftValue": "={{ $json.message.content.best_quote.paraphrased_quote }}",
              "rightValue": "",
              "operator": {
                "type": "string",
                "operation": "notEmpty",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.filter",
      "typeVersion": 2.2,
      "position": [
        1264,
        768
      ],
      "id": "a4cda9b9-73fe-49e4-9175-b78a2229abd4",
      "name": "Filter empty quotes"
    },
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 8
            }
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.2,
      "position": [
        -128,
        -16
      ],
      "id": "38c53378-51af-48ef-b31d-691714bcdfb3",
      "name": "Trigger daily"
    },
    {
      "parameters": {
        "jsCode": "// n8n Function node\nconst date = new Date();\n\n// subtract 1 day\ndate.setDate(date.getDate() - 1);\n\n// format to YYYY-MM-DD 00:00:00\nconst year = date.getFullYear();\nconst month = String(date.getMonth() + 1).padStart(2, '0');\nconst day = String(date.getDate()).padStart(2, '0');\n\nconst formatted = `${year}-${month}-${day} 00:00:00`;\n\nreturn [\n  {\n    json: {\n      oneDayAgo: formatted\n    }\n  }\n];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        160,
        272
      ],
      "id": "7aad5914-8e51-410f-b2db-582f3d0680eb",
      "name": "Set date (n - 1 day)"
    }
  ],
  "pinData": {},
  "connections": {
    "Get calls from past week": {
      "main": [
        [
          {
            "node": "Filter Outbound",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Filter Outbound": {
      "main": [
        [
          {
            "node": "Get transcript and participants",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get transcript and participants": {
      "main": [
        [
          {
            "node": "Create prompts",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Create prompts": {
      "main": [
        [
          {
            "node": "Have GPT get quotes",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Have GPT get quotes": {
      "main": [
        [
          {
            "node": "Filter empty quotes",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Kickoff message": {
      "main": [
        [
          {
            "node": "Set date (n - 1 day)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Filter empty quotes": {
      "main": [
        [
          {
            "node": "Reply in thread",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Trigger daily": {
      "main": [
        [
          {
            "node": "Kickoff message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Set date (n - 1 day)": {
      "main": [
        [
          {
            "node": "Get calls from past week",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": true,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "c50567a7-afdd-45d6-8cb9-f302d4661392",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "7494247a158e2c999b388670661bf7529fbb8284d7ed0b3c6efc35b40af4c8d4"
  },
  "id": "Uz2BYGiLiBXvzHRo",
  "tags": []
}
{% endhighlight %}

</details>

You can also download the workflow file directly to import into your n8n instance: [Gong Quote Finder.json](/assets/files/Gong-Quote-Finder.json)


## What's Next

Now that I've wired up Gong, Slack, and ChatGPT, I can picture even more automation:

- Automated follow-ups on Outbound calls
- Integrating this quote library as a tool for an AI agent, giving our sales team real-time, natural language access to customer stories
- Automated case study pipeline (we have this half-built today)

---

*Want to build something similar? The n8n workflow file is available above, and I'm happy to answer any questions you may have*
