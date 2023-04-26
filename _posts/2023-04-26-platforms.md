---
layout: post
title: Are Software Platforms Inevitable?
subtitle: A look at how software platforms come to be
description: Software platforms emerged from the 90s productivity suites and now dominate business software. This is a look at how they came to be, and if we're stuck with them.
tags: [software, platform, SaaS]
thumbnail-img: /assets/img/villain.png
share-img: /assets/img/villain.png
comments: false
---
{: .box-note}
I didn’t ChatGPT this but it was tempting

## Individual tools of the 90s

According to my dad and a whole bunch of other reliable sources, [VisiCalc](https://en.wikipedia.org/wiki/VisiCalc) was the first commercially successful application - a must-have that in part drove the adoption of the Apple II. It was eventually followed (and killed) by [Lotus 1-2-3](https://en.wikipedia.org/wiki/Lotus_1-2-3) in the early 80s, which became a killer app of the IBM PC from era (so much so that I was still using Lotus Notes for email in 2019 while working at IBM)(1).

In the 90s some of the most popular consumer applications were Microsoft Word & Excel, WinAmp, Netscape, McAfee, etc. What made VisiCal, Lotus 1-2-3, Winamp, and any other early applications popular? They were built and scoped to a very specific use case. Individual applications were almost always the first or second of their kind - and they had to be built slowly and with a narrow scope. Incremental change is the name of the innovation game, after all.

Software at the time was also just broadly ***new***, digital natives weren’t a thing, and users craved simplicity. Hardware limitations also stopped monsters from creating large, feature rich applications. 

Now, software tools fall into the platform trap. Uninhibited by the constraints of societal software adoption, the banes of hardware and driver hell and *oh no I unplugged the keyboard now my CD drive stopped spinning forever*….software developers are frequently building platforms. Are we bound to this future forever?

## Early platforms

For the purposes of this piece, I define a software platform as a tool or set of closely related & integrated tools from the same creator, with features and functionality intended for broad or different use cases. These began their reign of terror in the 90s and early 00s, and haven’t stopped since.

Even during these adolescent years of the software industry, the temptation of platforms lured the great business analysts of the period - those people setting business strategy for behemoths with resources to burn. Microsoft very famously had a tool for everything, [building a monopoly](https://www.justice.gov/atr/us-v-microsoft-courts-findings-fact) that [eventually dissolved](https://stratechery.com/2017/microsofts-monopoly-hangover/) with bundling tactics that were later found to be illegal. Not only was this just an anti-competitive behavior: Microsoft had dreams of stringing all of their products together to create a platform for everyone. This was exemplified by the mini-platform that they put together for word processing, spreadsheets and publishing: [Microsoft Works](https://en.wikipedia.org/wiki/Microsoft_Works).

![Microsoft Works](/assets/img/works.png){:width="100%"}

By this same definition, Google’s products are one of the largest software platforms in the world. Google arose in the new world of the post-dotcom boom and promptly started acquiring and integrating tools - AdSense, YouTube, etc. They’ve built and killed so many tools there’s a [whole website dedicated to it](https://killedbygoogle.com/). 

Over time the Google platform has led to a distracted, confusing set of loosely bundled tools with perhaps the broadest target user base in the world. Google’s goal is clear: to maximize advertising revenue by giving away some really useful tools (Maps), some formerly useful ones (GMail), and some really shitty ones (Wave? Buzz? Tango? Take your pick.).

Even the earliest open source darlings built platforms: Mozilla took a turn towards platforms when they released Mozilla Application Suite before splitting into three distinct efforts (Firefox, Thunderbird and whatever the [rest of this list are](https://en.wikipedia.org/wiki/List_of_Mozilla_products)). It would be tempting to accuse Red Hat of the same behavior but it seems to me that Operating Systems should probably be a unique class of platform from this discussion.

As SaaS software became a real & mature thing (following closely on the tails of early consumer-oriented SaaS software), a new class of platform emerged: B2B-focused platforms.

## The Mega Platform

From the consumer & prosumer focused productivity tools of the 90s and 00s came a new class of platform: the B2B focused software platform. Today there are B2B software platforms all over the world: Salesforce, HubSpot, Slack, Zendesk, Rippling, Oracle E-Business Suite, Zoho, IBM Cloud Pak For Data, etc. While many of these tools have widespread adoption, most of them are broadly loathed.

Why do people hate using platforms?

## How platforms come to be

> Every program attempts to expand until it can read mail. Those programs which cannot so expand are replaced by ones which can. - [Zawinski’s Law](https://en.wikipedia.org/wiki/Jamie_Zawinski#Zawinski's_Law)
> 

The platforms named above all offer a broad set of functionality. Salesforce built a CRM and then proceeded to turn it into a Frankenstein by way of acquisition. Advertising, data, productivity and analytics tools have been added and integrated to varying degrees with a whole smorgasbord of other acquired products. This has made for a messy, slow, miserable experience especially for the core legacy product. Instead of fixing the concept of a Person Account in Salesforce to account for the shift to PLG GTM models (a real improvement for their primary CRM users), they instead bought Mulesoft and Tableau. Now, their core business is under attack.

{: .box-note}
📈 Acquiring new tech and shoving it into your product can result in a net negative experience for users


Many companies choose the route of building a platform without acquisitions. Many of the 2010s era tech companies are guilty of this. See Alteryx, Domino, Evernote, Cloudera and more. - they started losing at their core market and struggled to find a way to win at their core market. This led to companies like Alteryx [calling themselves the Data Science and Analytics Automation Platform](https://www.google.com/search?q=alteryx) (not joking). While Alteryx used to be a great data prep tool, it failed to makes strides with their core business and instead looked at the data science and analytics markets with large, jealous eyes to the detriment of their visual transformation product.

{: .box-note}
🎪 Building new features for new users and shoving them into your product can result in a net negative experience for all users


![Microsoft Works](/assets/img/villain.png){:width="100%"}

What do acquisition and feature building have in common? They’re the result of a tempting but lazy tradeoff. Instead of innovating in their core business, management teams instead look to new users. Tech companies over the long run overwhelmingly push to dip their fingers in other pies, because their pie isn’t getting bigger fast enough and they can’t take a bigger piece of the pie. They do this at the expense of innovating on their core product.

## Are platforms inevitable?

![Microsoft Works](/assets/img/thanos.png){:width="100%"}

Given the incentive structure of public and venture-funded companies, they might be. The path to platform is easy to see:

- Decision makers identify new users/markets/whatever to target
- Acquisitions happen or new features/new products are added to the roadmap
- Chaos and lack of focus ensues
- ???
- Profit I guess?

Maybe the real problem is that innovation and creativity is hard, and value capture is easier when you can create average features for a totally new market. Perhaps there is an incentive structure for individual tools to stay focused - and that answer might be open source - but until that incentive structure is clearer, I worry that even the most niche of niche tool will either turn into a monstrosity or be incorporated into one.

1: IBM was a great company to work for - but sometimes good comes with bad, especially at that scale.

### I’m here to chat

If you want to talk about quantifying activation, I’d be happy to. [Find me on Twitter](https://twitter.com/csreuter), or you can email me at christopher (dot) s (dot) reuter (at) gmail (dot) com.
