---
layout: post
title: The Future of Data Engineering in the Warehouse
subtitle: New workloads are commodities, traditional data engineering is...complex?
description: Where data engineering workloads will live in the future.
tags: [data warehouse, Snowflake, data engineering]
thumbnail-img: /assets/img/data-eng-future-social-preview.jpg
share-img: /assets/img/data-eng-future-social-preview.jpg
comments: false
---
## What’s in a data engineer?

A common (or even a royal) data engineer is someone applying software engineering practices to data - storing, moving and modeling data in a production capacity. Historically this has involved stitching together many systems, writing code, working with distributed infrastructure depending on scale, and making it repeatable and resilient.

They’re typically at companies that either have significant quantities of data or high demand for using that data for both operational and analytics purposes

## The shift to the warehouse

{: .box-note}
For the purposes of this piece, we’ll use Snowflake to represent the cloud data warehouse offerings. They seem to have the clearest strategy & the most success when it comes to moving workload into the warehouse.

### **Warehouse-native data engineering**

A modern data engineering pattern has evolved for workloads that are analytical in nature, driven by new companies, a a scarcity of data engineering skills, and access to new tools. While there exist many enterprises that still run their data engineering practices out of Hadoop and Spark, the [Fivetran](https://www.fivetran.com/)/[dbt](https://www.getdbt.com/)/[Snowflake](https://www.snowflake.com/en/) pattern reigns supreme as the most popular way to get data into a new warehouse and then mold it with SQL to your liking for the purpose of analytics.

This has been encouraged (obviously) by Snowflake. Fivetran and dbt were the [2022](https://www.fivetran.com/press/fivetran-named-snowflake-data-integration-partner-of-the-year-adds-new-product-capabilities-extends-enterprise-customer-growth) and [2023](https://www.prnewswire.com/news-releases/dbt-labs-named-snowflake-data-integration-partner-of-the-year-301864344.html) data integration partners of the year for Snowflake respectively, and for good reason: there’s a ton of transformation now happening in the warehouse. This modern stack simplifies transformation in the warehouse, and extend access to that transformation to a less technical user, at the expense of Snowflake credits and scaling limitations. 

In an expression:

{: .box-note}
workloads with basic requirements + new tools + scarcity of data engineering resources = transformation in the warehouse

![Spongebob Data Engineering meme](/assets/img/data-eng-future-social-preview.jpg)

### **Traditional data engineering**

There exist workloads beyond in-warehouse transformations, that I would call “traditional data engineering”. These workloads involve use cases beyond the SQL transformation that are most often the best fit for a warehouse. 

These are compute intensive, judging by the kind of technologies that data engineers with big data typically use: [Spark](https://spark.apache.org/), [Hive](https://hive.apache.org/), [Docker](https://www.docker.com/), [Kubernetes](https://kubernetes.io/), [Flink](https://flink.apache.org/), [Kafka](https://kafka.apache.org/), [Dask](https://www.dask.org/), [Ray](https://www.ray.io/), [Presto](http://prestodb.github.io/), [Iceberg](https://iceberg.apache.org/), [Cassandra](https://cassandra.apache.org/_/index.html), and others. They feature heavy transformations written in code, operational workflows, and reactive data movement such as events or streaming. In short: they’re heavy, they are complex, and they are a major growth opportunity for Snowflake now that the analytical workloads are well-in-hand.

There’s great opportunity for Snowflake in traditional data engineering, as it can drive huge consumption. The introduction of [Snowpark](https://docs.snowflake.com/en/developer-guide/snowpark/index), which encompasses support for [Python](https://docs.snowflake.com/en/developer-guide/snowpark/python/index), [Java](https://docs.snowflake.com/en/developer-guide/snowpark/java/index), [Scala](https://docs.snowflake.com/en/developer-guide/snowpark/scala/index), and now even [containers](https://medium.com/snowflake/snowpark-container-services-a-tech-primer-99ff2ca8e741), appears to be Snowflake’s native answer to non-SQL workloads like ML, data quality, streaming, etc. 

With Snowpark, now you can run your custom code in the warehouse - don’t land your data elsewhere, just put it all in Snowflake! If you bring your transformations to Snowflake, will they be cheaper than wherever you are running them now? 🤷🏼 Maybe, and this appears to be the story that Snowflake is telling, particularly with Databricks in mind.

There is some reported adoption of Snowpark, but anecdotally, not that many people that I know are using it. Using Snowpark requires that the data exists in the warehouse, which is less likely to happen the more complex the workload (does it use many tool, stitch together multiple data sources, etc.). This aligns with Snowflake’s previous strategy of bringing as much consumption as possible into the walled garden.

## The future of data engineering

Imagine some spectrum of data engineering workloads, split between those solely in the warehouse, those solely outside of the warehouse, and those in between. How do our data engineering profiles map to this spectrum?

![Current Data Engineering Spectrum](/assets/img/data-eng-spectrum-current.png)

Today the basic, new workloads are mostly being built with the modern data engineering pattern. Think of new companies setting up a warehouse, BI and analytics for small teams, analytics engineers, etc. Eventually, some of those workloads become more complex - meaning they data sources, SLAs, or requirements that mean the warehouse along is not enough. Today, complex workloads are happening mostly outside of the warehouse, with the warehouse as primarily a destination for any transformed analytical data. 

Over time, these workloads will both shift left. Snowflake will consume even more new workloads, and traditional workloads will start to incorporate warehouses to a greater degree (more than just a source, or for a small number of transformations). Something like this:

![Future Data Engineering Spectrumd](/assets/img/data-eng-spectrum-future.png)

Traditional data engineering workloads are the largest and most valuable to vendors, not only for the scale (big companies do lots of data engineering) and the actual consumption that they represent (changing lots of 1s and 0s is worth $$$), but also for the end product that they produce: analytical datasets, aka Snowflake’s bread & butter. 

It is most likely that the future state for traditional workloads is living in BOTH in the warehouse and outside of the warehouse. It does not seem reasonable that Snowflake, that previously was a data warehouse, could encompass all data engineering (transformation + operational workflows) within itself effectively. Not only has it not been done before, it seems incredibly unlikely to happen for several reasons:

- Their compute engine is optimized for OLAP
    - Snowflake does have a “single platform for analytical and transactional” story called [Unistore](https://www.snowflake.com/en/data-cloud/workloads/unistore/), but it was announced in June 2022 and a public preview is still coming soon.
- They have Python/Java/Scala support, but it requires that data to be in the warehouse and it can’t federate
- Transformations are compute-intensive and probably very expensive on Snowflake
- Due to Snowflake’s business model, they want all data in the Snowflake walled garden - this is a disincentive to playing nicely with others

## What will Snowflake do?

Ultimately, this comes down to a bet by Snowflake.

1. Do they think they can build a platform that can capture complex data engineering workflows?
2. If they accept the premise that complex workloads will only ever partially live on Snowflake at best, which is more valuable:
    1. Focusing on data engineering within the Snowflake platform (their same old playbook), at the expense of hybrid workloads
    2. Encouraging hybrid data engineering at the expense of maximizing data engineering on the Snowflake platform, in order to capture & monetize the associated analytical workloads

The future of data engineering in the warehouse is a bit of a clickbait title, I admit that. It really matters a lot, to a lot of people. 

### The user

Data warehouses make analytics easier. Imagine if they made data engineering easier, at scale, for even the hardest workloads! Moats would be drained, walls broken down, companies would rise & fall.

### The vendors

Snowflake has enjoyed remarkable growth over the past 10 years, culminating in their IPO last year. A continued growth story depends on pulling more traditional data engineering, into the warehouse. [BigQuery](https://cloud.google.com/bigquery), [Redshift](https://aws.amazon.com/redshift/), and [Databricks](https://www.databricks.com/) (in the opposite sense) rely on similar capabilities.

What will happen? Let’s all pay attention, as the future unfolds in front of us.


{: .box-note}
A new feature hails below!

{: .box-note}
**What was I listening to when writing this?**
<br>
[Dire Straits - Once Upon A Time In The West - Live At Hammersmith Odeon](https://www.youtube.com/watch?v=LG9RQS76zGc)
