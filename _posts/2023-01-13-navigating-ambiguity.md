---
layout: post
title: Navigating ambiguity & prioritizing efforts
subtitle: The Prefect Growth Framework
description: A few sentences on prioritizing product work using a Growth Framework
tags: [growth, framework, product funnel]
comments: true
---

**tl;dr:** To know where to focus our work on the Product Growth team, we’ve created the [Prefect](https://www.prefect.io) Growth Framework. This helps us to prioritize what we work on, and what not to work on.

{: .box-note}
**Note:** This is based on an internal blog post. I have removed some proprietary or sensitive information. I hope you still find this helpful.

### How we got here

In the first week that I joined [Prefect](https://www.prefect.io), I watched a recording of our most recent company update (called a Chapter Update). It featured our CEO describing something that was called Orion. I eventually learned that Orion was really the engine behind Prefect 2 - our next generation orchestration platform. Surprise, we were rebuilding the product of the company that I just joined!

Our team had a vision for a better, more flexible orchestration tool that was built for incremental adoption. It turns out through the glasses of retrospect that redeveloping Prefect from the ground up was an obvious decision: it has been a groundbreaking advancement in orchestration for many of our existing users, and has made it easy for an entire new class of Python developers to adopt orchestration.

Developing Orion and the new version of Prefect Cloud around it started with big ideas that were clear priorities. It looked something like this:

-  Make the open source engine & make it reliable
-  Make the Cloud version & make it reliable
-  Perfect the migration

As we got closer to achieving those above 3 obvious priorities, we started to ask ourselves: 

> How do we decide what to work on next?

### Obvious Priorities

There are still two types of decisions in our world: those that are obvious, and those that aren’t. Unsurprisingly, the obvious decisions are becoming more scarce while those that aren’t obvious are becoming more frequent. For those decisions that aren’t obvious, we knew that we needed some way to decide where to focus our efforts.

Luckily, and at times to my chagrin, there is no shortage of ideas here at Prefect. What we do have are a limited number of human hours needed to execute on the right ideas. As one smart person once told me:

> Ideas are cheap, implementation is hard

### Navigating ambiguity

Obvious decisions almost always align with at least one strategic imperative (we have 3 core imperatives), making it easy to say “let’s just do it”. But what happens when you are faced with many alternatives, none of which seem to be a no-brainer impact on revenue, product innovation or efficiency?

To help us prioritize our engineering and product efforts, the Product Growth team operates using a Growth Framework. Building a Growth Framework can help companies prioritize their efforts and avoid spending time on things that don’t matter.

### How we built our Framework

The Prefect Growth Framework is a list of roughly sequential things that a user of Prefect must do, in order to become a paying customer. A simplified version of a Growth Framework for any SaaS product might look like this:

![Simplified Framework](/assets/img/ambiguity-1.png){:width="35%"}

You can think of the three steps above as aligning to an organization model.

![Framework with Organizations](/assets/img/ambiguity-2.png){:width="45%"}

The Prefect Growth Framework started out as something like the above. In order to make this actionable, we expanded on each step in order to tie them to a discrete & measurable action.

![The Prefect Growth Framework](/assets/img/ambiguity-3.png)

The above list of steps are what any individual user typically performs in order to become a paying Prefect Cloud customer. They don’t have to go through all of these steps, and sometimes the journey isn’t exactly linear. While it may seem daunting, it is simply a detailed representation of a funnel.

### Making decisions with a Framework

On the Product team focused on Growth here at [Prefect](https://www.prefect.io), we have made a conscious choice: **if a proposed idea isn’t an obvious choice, we prioritize it using the growth framework.**

One benefit of creating a detailed Growth Framework is that most of the steps are represented by a metric that we can track. With some exceptions (we can’t and won’t track what open source users are doing), we can identify how many users are progressing through this Framework across different times, cohorts, origins, etc.

One example of a Framework metric is the metric for the workspace creation step. This is measured by **workspaces created** divided by **accounts created**. If this metric is 50%, this means that half of our users that created an account have created a workspace. Generally, the denominator of each step is the numerator of the step before it.

Aligning Framework steps to metrics means that we can then assess our funnel performance, determine which steps have the biggest opportunity and prioritize work for those steps.

{: .box-note}
**Note:** It is important to develop a theoretical Growth Framework even when there are steps that you can’t track directly. “What metric would we track?” and then optimizing for that theoretical metric is a good substitute for taking actions against an existing metric.

### Assessing & iterating on your decisions

Now that we have established a Framework for making decisions, we need to sprinkle some art into this science: which Growth Framework steps are most important?

You could approach this in several different ways. We started by laying out our Growth Framework metrics in a product funnel. It looked something like this:

![Product Funnel Metrics](/assets/img/ambiguity-5.png){:width="60%"}

In our case, we are generally focusing on the framework steps that have the lowest conversion rates. In the graph above, that would be the lines with the largest gaps between them.

Your product might be different: you may intentionally have large cliffs between steps. We view some of our product funnel steps as naturally qualifying: if someone achieves a certain step, it means they are more “qualified” to reach the end of our funnel. Spending time focusing on a framework step that is a “qualifying” framework step may give you an artificial top-line bump while causing a negligible or negative impact on your downstream metrics.

Implementing product changes/improvements that are explicitly tied to specific Framework steps & metrics allows us to iterate quickly and understand impact. We recently introduced a change that resulted in a Framework conversion metric improving by nearly 20% across monthly cohorts. We’ve had other changes make a negligible impact. These variable results have only reinforced the need for us to measure, test, and iterate quickly on our work.

### Navigating ambiguity through a Framework

What happens when you have a wealth of ideas, but limited resources to implement them all? You define & measure your funnel, creating a Growth Framework that can help you inform where you focus your time and how to assess if your time is well spent.

Of course, life is never easy, and we struggle every day with things like:

- Our open source product resulting in a lack of data
- A complex product built for developers
- A B2C2B buying model (I’ll write more on this later)
- A proliferation of obvious priorities

Even with these challenges, we have found that a Growth Framework helps give us some clarity as to what we work on, and how impactful our work is.
