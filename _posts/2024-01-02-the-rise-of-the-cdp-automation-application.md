---
layout: post
title: The rise of the CDP Automation Application
subtitle: What's with all the new CDP + Workflow tools?
description: Is it a bird, a plane, a CDP, or a workflow buidler?
tags: [workflow, CDP, SaaS]
thumbnail-img: /assets/img/cdp-preview.png
share-img: /assets/img/bartcdp-preview.png
comments: false
---
## The Customer Data Platform (CDP)

Traditionally (and these aren’t even that old, so tradition is used loosely here) a CDP is a headless tool that is used to create a dataset representing all of the information about a company’s customers. These are accessible by other tools, focusing on:

- integration of data about customers from various sources
- de-duplication of said data and customers
- persisting all of it to your data warehouse (hence the headless)

Examples of CDPs that built the category are Segment and Amplitude, followed by an open source version with Posthog.

## Co-opting the CDP

Recently there has been a surprising growth in the number of tools acting explicitly or implicitly as a Customer Data Platform (CDP). Some of which I’ve used, some of which I haven’t:

- customer.io
- Atlan
- Pocus
- Census
- Hightouch
- Klaviyo

These include marketing platforms, data catalogs, reverse ETL, and even sales accelerator tools. All of these that I have included have some marketing around them being a CDP out there in the world. So why did all of these different categories decide to enter the CDP space? I would posit the answer is related to automation.

## Workflows are processes

Everybody has recurring tasks that they perform at home. Maybe you make oatmeal every morning. Let’s assume you aren’t a maniac and you make your oatmeal the correct way (on the stove) - every morning you take out a pot, measure some milk, put it in the pot, measure some oats, put those in the pot, turn on the heat, and so on.

Cooking oatmeal is a workflow: you decide you’re hungry, so you take the steps needed to make delicious, savory oatmeal. Workflows are processes (like cooking oatmeal), with step by step actions that occur based on some trigger condition.

## Automation

In yesteryear, and still to some extent, business processes were performed by humans. A credit card application was at one point reviewed by a human, who followed some process and then returned an approval or denial. Today, most credit card applications along with other rote tasks are automated by a computer. 

These automated workflows are inherently cheaper than those performed by humans: we’re really slow counters compared to machines, and we’re really bad at doing more than one task at once. Therefore, much of work today is humans designing workflows that computers then execute.

## The distribution of automation and growth of SaaS

Automation from 1980 to 2010 was migrating out of individual tools where they started (by and large databases), and into the 3rd party GUI schedulers (Control-M, ActiveBatch, JAMS, Stonebranch) or business-user focused RPA tools (Pegasystems, UiPath, Zapier, Appian). Integrating or embedding these tools into your own application is super painful because of the nature of their design: rigid for a reason[^1].

One great example of early automation is Salesforce, who built their own (awful) workflow tool built around Apex and XML. This was a company with hundreds of millions of dollars, and their automations barely hung together. Imagine trying to build automation within your own application pre-2010 when you were a tool NOT focused on automation.

~10 years ago, code-first orchestrators (Airflow next, now Prefect and others) entered the scene[^2]. As the barriers to entry for creating applications have slowly been reduced to rubble[^3], so have the barriers to entry for embedding workflow automation into applications: all thanks to the orchestrators. Code-first orchestration tools mean that automation can be exposed to users of SaaS applications when previously that was really hard to build for those application developers.

From Orbit to Klaviyo to customer.io: powerful automation is now been distributed into the SaaS applications. So why are they calling themselves CDPs?

## The CDP Automation Application

**The answer is: CDPs serve automation…always have.**

The entire reason for a CDP to exist, is to take some action based on unified information. Automation without triggers is useless: if you don’t know you’re hungry, you (probably) will never start the process to make yourself some oatmeal.

<div style="text-align: center">
![CDPs + Workflow Tools](/assets/img/cdp-1.png){:width="80%"}
</div>

The original CDPs were headless: developer tools aimed at being for integration and segmentation in service of analytics. What they morphed into were operational integration tools: serving some action (make my oatmeal!) in some other system (Control-M, ActiveBatch, some custom tool, etc).

It seems to me that what these tools are hearing from users:

- I want a unified view of all my data (CDP)
- I want to take action with it (Automation/workflow tool)
- All in one place

and that they’re taking action to build this thing - carving out market share from two different categories.

<div style="text-align: center">
![CDP Automation Application](/assets/img/cdp-2.png){:width="30%"}
</div>

## What’s next?

Is the modal CDP destined to move towards the SaaS applications that are adding workflows[^4]? Or is co-opting of the CDP market an indication of intense competition for market share driven by hungry startups?

My bet: this is an overall market expansion for both automation and CDPs, where the low end of the market (less technical users and those who wouldn’t buy a standalone or automation tool) will enjoy features provided by the tools they already use, and eventually become a funnel into the high end CDP and workflow tools mentioned above.

{: .box-note}
**What was I listening to when writing this?**
<br>
[Chris Thile - Another New World](https://www.youtube.com/watch?v=_n3wHljJQ4M)

[^1]: Rigid for a reason because users are stupid and need it, ask any product manager
[^2]: See [this excellent read](https://www.prefect.io/blog/brief-history-of-workflow-orchestration) on the history of this time period by Bill Palombi
[^3]: Everything needed to create an application (infra, networking, UI frameworks, etc) is now super cheap and super easy to use
[^4]: For more on platforms check out [this piece I wrote](https://chrisreuter.me/2023-04-26-platforms/)
