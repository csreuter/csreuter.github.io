---
layout: post
title: Creating The Prefect Activation Metric
subtitle: or, Did It Really Need To Be This Complex?
description: How we created our activation metric at Prefect, how we use it, and some lessons learned
tags: [growth, activation]
thumbnail-img: /assets/img/activation-feature-table.png
share-img: /assets/img/activation-feature-table.png
comments: false
---

# Creating the Prefect Activation Metric

At [Prefect](https://www.prefect.io/), we use activation metrics to measure how our users are engaging with our product. The purpose of these metrics are twofold: to determine an individual user’s engagement with Prefect Cloud, and to measure our user base in aggregate. Scores for individual users help us deliver targeted content, identify prospective clients early in the adoption process, and understand a user’s journey. Aggregate scores help us understand what growth tactics to invest in. In this post, I’ll cover our activation metrics (we have three), how we made them, and how we use them.

# Why use an activation metric?

When I first joined Prefect, we looked at a variety of different attributes at the user and account level. There are [concepts in Prefect](https://docs.prefect.io/concepts/overview/) like `flow` and `task`, `collaborator` and `automation`, so on and so forth. Most of the time when someone asked “how is this user doing”, we would look at a dashboard that had all of these individual metrics neatly laid out over time. It took mental effort to develop an understanding of a single customer, and it was difficult to comprehend how effectively our users adopted our product across cohorts.

We found ourselves looking for an easy-to-understand and interpret measure of how a user was adopting Prefect. At the time, our goal was to identify those users that were worth talking to and those that still needed time to activate.

# When activation matters

Prefect is a [product-led company](https://openviewpartners.com/blog/what-is-product-led-growth/) with an [open source product](https://github.com/PrefectHQ/prefect), a free tier of our [commercial product](https://www.prefect.io/pricing/), and a large self-serve customer base. Many of our paying customers never talk to our sales team, and for good reason: we are a [tool built by developers for developers](https://xkcd.com/378/).

This go-to-market (GTM) model means that we rely on product experience and documentation to activate users. We provide value before ever asking for a dollar. This inverts the typical (or legacy, depending on your perspective) SaaS GTM model where users never used a product before paying for it. 

In a scenario where you’re a typical Enterprise SaaS company, you would naturally focus on demand generation, sales pipeline and your sales conversion rates. You would hire large demand generation and sales teams and you could live in [Salesforce](https://www.salesforce.com/).

The concept of activation matters for Prefect because the product is the sales rep, and product usage is the pipeline.

# What are our metrics

We have 3 activation metrics that represent 3 different abstractions of Prefect Cloud: `workspaces`, `users`, and `accounts`. 

Our activation scores are simple weighted averages that yield a composite score between 0 and 100. Here is a snapshot of the `workspace` activation score:

![Prefect's Activation Score](/assets/img/workspace-activation.png){:width="50%"}

Each row can be assigned a score of 0 to 100, and each row has a weight. We assigned 50% of the overall score to usage and 50% to feature milestones. You’ll notice that the feature milestones align closely to the [Prefect Growth Framework](https://chrisreuter.me/2023-01-13-navigating-ambiguity/).

# But Chris, this is so complicated

I will admit that this is a relatively complex activation metric. In fact, you will hear from many people that a simple activation milestone is simpler and clearer for teams to understand. 

I would posit that this activation metric achieves its purpose: giving product advocates, salespeople, our support team and anyone else who cares a quick idea of how far along a user/workspace/account is. We are abstracting away complexity for a simple purpose - a fast, discrete assessment and an accurate aggregate measure of performance over time.

The case can be made for both a simple and a complex activation metric. What is right for you will depend on a variety of things: point in time, goals, who you hire, and more.

# How we made them

### Cloud 1 & Pairwise Matrix

Our first activation metric was based on a pairwise [correlation matrix](https://en.wikipedia.org/wiki/Correlation#Correlation_matrices). We had a large table of users, counts of events they had performed, and how much they had spent lifetime. It looked something like this:

![Feature Table](/assets/img/activation-feature-table.png){:width="75%"}

 I wrote a simple Python script that calculated correlation between each feature, and laid the results out in what is called a pairwise matrix. I used `.corr()` and Seaborn’s `heatmap` to create the below matrix ([guide here](https://medium.com/@szabo.bibor/how-to-create-a-seaborn-correlation-heatmap-in-python-834c0686b88e)).

![Correlation Matrix Heatmap](/assets/img/activation-heatmap.png){:width="50%"}

We used this heatmap to identify where correlation between spend and 1st order events seemed high, and worked backwards from there to find 2nd order events/actions that were correlated with the 1st order events.

We then applied a little bit of gut feel and assigned weights to each of these actions. This resulted in our first activation metric that looked like this:

![The original activation score](/assets/img/cloud1-activation.png){:width="50%"}

### Cloud 2 & the move to 3 scores

When we released our next generation product, we introduced additional abstractions - `workspaces` and `accounts`.

Inspired by our original activation metric, we composed 3 new activation metrics in a similar format to our Cloud 1 metric - with our new concepts (deployments, work queues, etc.). We didn’t have a great feature to optimize for (as we had with spend previously), but we liked the format of the metric and created something similar. Below is the `workspace` activation metric.

![Prefect's Activation Score](/assets/img/workspace-activation.png){:width="50%"}

# How we use them

Thanks to the help of our data team, activation scores are calculated nightly using Prefect + [dbt](https://github.com/dbt-labs/dbt-core). We store all of this data in BigQuery for aggregate analysis and make it available at the individual level to a variety of other tools using Census.

### Individual metrics

- [customer.io](https://customer.io/)
    - We use our activation score & it’s components to power our onboarding and engagement workflows in our marketing automation tool, customer.io.
- [Orbit](https://orbit.love/)
    - We have started pushing activation data to Orbit, our central clearinghouse for community data. This helps anyone working with community members to understand where they are with their Prefect Cloud journey.
- Salesforce
    - We augment leads and contacts with activation data to give account executives a snapshot of their prospects & customers. This helps our reps start with a better understanding of a user’s situation.

### Aggregate

We perform product experiments (often UI-based), like adding a mock code terminal to empty Prefect screens, in-product tours, or adding Prefect Collections into the UI. We track cohort activation scores relative to a start date and relate them to these experiments to determine what impact (if any) they had on user activation.

# Some lessons learned

Our activation metric and its subcomponents powers many of our processes today:

- Onboarding personalization
- Snapshot of user success for our GTM teams
- Measuring impact of growth experiments

However, it was not an overnight success. We didn’t have a ton of people adopt the activation metric at first. They didn’t get what it was, and it wasn’t immediately useful to them. However, when they needed a quick way to understand a user’s progress, my team would ******always****** offer up the activation score and a definition of what it was.

{: .box-note}
1️⃣ The lesson learned here: be persistent & make it useful. If it is helpful, it will be adopted. People won’t get it right away, and that’s OK. They will over time.

One hidden benefit of creating an activation score on the complex side of the spectrum is that it forces you to effectively create and maintain many metrics. We ended up using the subcomponents of the user activation score in our email onboarding workflow.

{: .box-note}
2️⃣ Data related to activation can be operationally helpful, and not just an analytics experiment

Finally, I’ve learned from our activation metric is that our product is never-changing. Our activation score is effectively a [slowly changing dimension](https://en.wikipedia.org/wiki/Slowly_changing_dimension), as the behavior of users changes with the dramatic changes to Prefect itself. Having introduced a score that was intended, in part, to help our sales team understand user behavior. Looking back, I wouldn’t be afraid to change the definition of our activation metric - the market is changing, our product is changing, and our user behavior is ever-changing.

{: .box-note}
3️⃣ Your activation metric doesn’t have to be static - don’t be afraid to change it early and often.

### I’m here to chat

If you want to talk about quantifying activation, I’d be happy to. [Find me on Twitter](https://twitter.com/csreuter), or you can email me at christopher (dot) s (dot) reuter (at) gmail (dot) com.
