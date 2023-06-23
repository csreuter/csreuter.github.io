---
layout: post
title: Building a Growth Tech Stack
subtitle: Prefect's technology stack that powers the Growth team
description: What are the most important tools to have, for a healthy Growth function?
tags: [software, platform, SaaS, growth, technology]
thumbnail-img: /assets/img/tech-stack-splash.jpg
share-img: /assets/img/tech-stack-splash.jpg
comments: false
---
Tools aimed at PLG companies are really hot right now - super hot! I thought it would be helpful to see the tools that the Prefect Growth team uses, and those tools that we are the primary owners (and primary value extractors) of.

## What we do

The Growth team at Prefect is a full-funnel team that is structured similarly to the principles laid out by [Lenny Rachitsky](https://www.lennysnewsletter.com/) and many others:

- Acquisition
    - Core Metric: Sign-ups
    - Activities: Paid advertising, email, content, sponsorships
- Activation
    - Core Metric: Active Teams
    - Activities: Email, in-application nudges & development, support product advocate team
- Monetization
    - Core Metric: Self-serve revenue
    - Activities: Pricing, in-application nudges

## The Stack

![Prefect's Growth Tech Stack](/assets/img/growth-tech-stack.png)
    

While we benefit from a variety of tools, the Growth team are the primary owners of just 3 tools and 1 core dataset. While every company will differ, each tool category is probably a must in order to support a healthy, data-driven Growth function.

## Categories, Defined

- **Data Sources:** The things that you are measuring exist in a variety of applications.
- **Replication:** Getting the data from those data sources, into a centralized place.
- **Data Warehouse & CDP:** A data warehouse is a centralized place to store all of your information. CDPs consolidate user information, attempting to “de-dupe” your data.
- **Transformation:** Transforms your raw data into useful information.
- **Reverse ETL:** Gets data out of your data warehouse, and into applications .
- **Automation & Actions:** Broadly, marketing automation and segmentation.
- **CRM:** You’ll need to work with your sales team eventually.
- **Orchestration:** Scheduling & visibility into all of your workflows between the stack.

## Our Core Growth Tools

### Custom Activation Metrics & Other Data

The hero of our stack is a consolidated and augmented view of our users. We consolidate a variety of key metrics and their subcomponents at the user level, tracking things like activation & activity on our platform, payments, activity in our community, onboarding steps, etc. Without this information, the other tools that we use would be worthless.

One great example of a specific, targeted action only enabled by a large, clean, consolidated dataset is our onboarding activation campaign. Email campaigns may seem easy at first, but presenting the user with a customized experience unique to their situation that also feels like it is from a human is tricky.

I’m lucky enough to work with brilliant individuals like our Growth Lead Sarah Krasnik [(read her writing here](https://substack.com/@sarahkrasnik), who has helped us to establish an onboarding flow that is best-in-class with dozens of possible permutations.

### [customer.io](https://customer.io/)

The secondary hero of our stack is [customer.io](http://customer.io). This is a marketing automation tool where we run all of our automated email campaigns, user segmentation, triggering of custom UI experiences in Prefect Cloud for users entering unique situations, sending of Slack notifications for purchases, and more.

Examples of our campaigns include onboarding activation, re-engagement, “you didn’t complete this…”, “free trial started”, and more.

I believe that [customer.io](http://customer.io) is aimed at B2C situations, and possibly with a focus on mobile apps, but we’ve adapted it to fit our needs quite easily. This might be because PLG really means B2C2B, but that’s a song for another time.

[Customer.io](http://Customer.io) also features a simple data model (one huge table, a row is a person and an attribute is a column) with support for events and now custom objects (although we don’t use these). Segments are easy to build and stay updated based on you updating your data.

There’s also a nice API, wonderful campaign workflow builder with support for webhooks (incoming AND outgoing) and updating attributes, newsletters (which are meh but at least they are there), Liquid templating, a GUI email builder, native form support, and more.

Finally, we love self serve tools here at the ~~Hall of Justice~~ Prefect. [customer.io](http://customer.io) is completely ungated from a feature perspective, which lets you build a first-class experience without having to be a top 1% company AND without ever having to talk to a salesperson.

### [Chameleon](https://www.chameleon.io/)

Chameleon is a simple but useful tool. It is a UI overlay that allows anyone to quickly & easily create visual elements within the Prefect application.

We run some basic onboarding tours using Chameleon within the UI. We also surface product announcements, maintenance times, and custom banners (often related to plans & pricing). Some of these custom banners are triggered from a [customer.io](http://customer.io) webhook.

### [Orbit](https://orbit.love/)

Orbit is a community management tool that we find very useful. It both collects data for us via native integrations with popular 3rd party tools like LinkedIn, YouTube, Slack, GitHub, and more. This is primarily used as our “CRM before the CRM”, giving anyone interacting with community members a snapshot into that member’s activity.

Orbit’s list functionality is heavily used by the Prefect team, for things like greeting first-time Slack posters.

## Where To Start

The key to a healthy Growth function is lots of cleaned data. Without investing in a strong data platform, none of the others tools that I mentioned matter. You can read more on how to do this, in [my piece on creating an activation metric](https://chrisreuter.me/2023-03-14-activation-metric/).

Once you have a good start on data, a logical next step is to get it into a tool that allows you take action with it. We love the flexibility of a tool like customer.io, as it allows a Growth team to create workflows that can trigger actions in other systems very easily with fine-grained logic. You should pick the tool that is right for you.

Best of luck, and if you have any questions I’m always available via the links at the bottom.
