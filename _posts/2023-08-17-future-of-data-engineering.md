---
layout: post
title: The Future of Data Engineering
subtitle: New workloads are commodities, complex data engineering is...complex?
description: Where data engineering workloads will live in the future.
tags: [data warehouse, Snowflake, data engineering]
thumbnail-img: /assets/img/preview-card-future-data-eng.png
share-img: /assets/img/preview-card-future-data-eng.png
comments: false
---
## What’s a data engineer?

The mode data engineer is applying software engineering practices to data - moving and modeling data in a production capacity. This involves stitching together many systems, writing code, working with distributed infrastructure depending on scale, and making it repeatable and resilient.

They’re typically at companies with complex ecosystems, significant quantities of data, and high demand for using that date for both operational and for analytical purposes.

## The shift to the warehouse

{: .box-note}
For the purposes of this piece, we’ll use Snowflake to represent the cloud data warehouse offerings. They seem to have the clearest strategy & the most success when it comes to moving workload into the warehouse.

###Warehouse-native data engineering

A modern data engineering pattern has evolved for net new workloads, driven by new companies and new tools. While it hasn’t taken hold in as many enterprises, the Fivetran/dbt/Snowflake pattern reigns supreme as the simplest way to get data into a warehouse and then mold it to your liking for the purpose of analytics.

This has been encouraged (obviously) by Snowflake. Fivetran and dbt were the [2022](https://www.fivetran.com/press/fivetran-named-snowflake-data-integration-partner-of-the-year-adds-new-product-capabilities-extends-enterprise-customer-growth) and [2023](https://www.prnewswire.com/news-releases/dbt-labs-named-snowflake-data-integration-partner-of-the-year-301864344.html) data integration partners of the year for Snowflake respectively, and for good reason: it’s all happening in the warehouse. These tools simplify transformation, and extends access to it, at the expense of Snowflake credits and scaling limitations.

###Traditional data engineering

There’s great opportunity for Snowflake in traditional data engineering, as it can drive huge consumption. Traditional data engineering workloads are compute intensive, judging by the kind of technologies that data engineers with big data typically use: Dask, Ray, Spark, Hive, Flink, Cassandra, and others. They feature heavy transformations and operational data movement, and are a major growth opportunity for Snowflake now that the analytical workloads are well-in-hand.

The introduction of Snowpark, which encompasses support for [Python](https://docs.snowflake.com/en/developer-guide/snowpark/python/index), [Java](https://docs.snowflake.com/en/developer-guide/snowpark/java/index), [Scala](https://docs.snowflake.com/en/developer-guide/snowpark/scala/index), and now even [containers](https://medium.com/snowflake/snowpark-container-services-a-tech-primer-99ff2ca8e741), appears to be Snowflake’s native answer to heavy transformations. Now you can run your custom code in the warehouse - don’t land it elsewhere, just put it all in Snowflake! If you bring your transformations to Snowflake, will they be cheaper than wherever you are running them now? 🤷🏼 Maybe!

There is reported adoption of Snowpark, but anecdotally, not that many people that I know are using it. Using Snowpark generally required that the data exists in the warehouse beforehand, which is less likely to happen the more complex the workload. This aligns with Snowflake’s previous strategy of bringing as much consumption as possible into the walled garden.

## The future of data engineering

Imagine some spectrum of data engineering workloads, split between those solely in the warehouse, those solely outside of the warehouse, and those in between. How do our data engineering profiles map to this spectrum?

![Current Data Engineering Spectrum](/assets/img/data-eng-spectrum-current.png)

Today the basic, new workloads are mostly being built with the modern data engineering pattern. Think of new companies setting up a warehouse, BI and analytics for small teams, analytics engineers, etc. Eventually, some of those workloads become more complex. Today, complex workloads are happening mostly outside of the warehouse, with the warehouse as primarily a destination for any transformed analytical data. 

Over time, these workloads will both shift left. Snowflake will consume even more new workloads, and traditional workloads will start to incorporate warehouses to a greater degree. Something like this:

![Future Data Engineering Spectrumd](/assets/img/data-eng-spectrum-future.png)

Complex data engineering workloads are the largest and most valuable to vendors, not only for the actual consumption that they represent (changing lots of 1s and 0s is worth $$$), but also for the end product that they produce: analytical datasets, aka Snowflake’s bread & butter. 

It is most likely that the future state for complex workloads is living in BOTH in the warehouse and outside of the warehouse. It does not seem reasonable that Snowflake, that previously was a data warehouse, can encompass all data engineering (transformation + operational workflows) within itself effectively.

## What will Snowflake do?

Ultimately, this comes down to a bet by Snowflake.

1. Do they think they can build a platform that can capture complex data engineering workflows?
2. If they accept the premise that complex workloads will only ever partially live on Snowflake at best, which is more valuable:
    1. Focusing on data engineering within the Snowflake platform (their same old playbook), at the expense of hybrid workloads
    2. Encouraging hybrid data engineering at the expense of maximizing data engineering on the Snowflake platform, in order to capture & monetize the associated analytical workloads
