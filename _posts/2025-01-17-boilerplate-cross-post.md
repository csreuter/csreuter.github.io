---
layout: post
title: A History of CMDBs
subtitle: How boring might be new again
description: CMDBs were made for an older era of infrastructure management. Companies using the cloud means new concepts (ephemeral resources, high volume of resources, and many more abstractions), and that means a new type of CMDB is required.
canonical-url: https://www.cloudquery.io/blog/a-history-of-cmdbs
tags: [cloudquery, cmdb, cloud]
thumbnail-img: /assets/img/cmdb-thumbnail.png
share-img: /assets/img/cmdb-thumbnail.png
comments: false
---
{: .box-note}
**tl;dr**
<br>
CMDBs were made for an older era of infrastructure management. Companies using the cloud means new concepts (ephemeral resources, high volume of resources, and many more abstractions), and that means a new type of CMDB is required.

### **40 Years of Trying to Track Infrastructure**

Did you know that before AI, there was a similar hyped-up phase called “migrating to the cloud”? Almost 20 years ago (oh no, I’m old), the internet was run on a bunch of physical computers that individual companies owned (or rented). Sometimes they owned the data center itself, or sometimes they shared space with other companies in a “[**colo**](https://en.wikipedia.org/wiki/Colocation_centre)”.

Around 2006 vendors started popping up who provided computing-primitives-as-a-service. S3, EC2, and later RDS…along with the concepts to help them work together: IAM, firewalls, IPs, security groups. These were all broken down into individual microservices (although microservice really meant something else back then, but I’m co-opting it now in retrospect for infrastructure architecture and not application architecture), made elastic and scalable, and adopted by companies in the great Cloud Migration of the 2010s.

Prior to 2006, vendors had to buy servers, hard drives, server racks, NICs, switches, routers, power supplies, cooling systems. It was a complicated world, but we were able to keep track of it back then with a little help from a tool called a CMDB. Some of us called these “distributed systems” back then, given that many companies in the 90s were moving from mainframes to commodity hardware (Anyone remember [**Sun**](https://en.wikipedia.org/wiki/Sun_Microsystems)'s 'The Network is the Computer'?). To understand why this migration was so disruptive, we need to look at the tool that kept the pre-cloud world running.

### **What is a CMDB?**

A configuration management database (CMDB) helps companies keep track of the computing-related assets they use, along with their configuration. They started in the late 80s/early 90s, when companies found themselves in the business of managing lots and lots of physical servers, storage systems, networking, etc.

These distributed systems resulted in server sprawl, especially for the largest and most sophisticated companies of the era. The related assets needed to be updated and managed, but keeping track of the management and updates was incredibly painful: Excel Sheets (or Lotus 123), paper files, or even worse: nothing.

Along with exploding IT assets across data centers, audit & regulatory pressures around computing were ramping up. [**ITIL**](https://en.wikipedia.org/wiki/ITIL), originally created by the UK government, drove a wave of “Configuration Management” practices. Vendors followed, notably BMC, IBM Tivoli, HP OpenView, and more.

Fundamentally, legacy CMDBs were all about top-down governance, manual record keeping, and designed for the data center era. The focus was on accuracy through process discipline, and not about real-time snapshots of configuration state or infrastructure usage.

### **CMDBs are dead?**

As the Great Cloud Migration of the 2010s ™️ drove a rapid shift in how people used infrastructure, CMDBs fell out of favor. Why?

- Scale: cloud infrastructure lets people use a LOT more resources, and the architecture of that infrastructure became more complex
- CI/CD: The rise of CI/CD led configuration to be declared in code and changes evaluated in near-real-time.
- Shifting left: In the past, IT teams controlled infrastructure with an iron fist. Why not, it made sense? The data center was the fief, and the developers were their subjects. Empowering developers to declaratively define infrastructure in code ([**Terraform**](https://github.com/hashicorp/terraform)) meant they were creating infrastructure from scratch…and they definitely didn't want to update a static CMDB when they did so!

In short, CMDBs became stale the minute DevOps, cloud, and automation landed. They indexed on process over reality.

### **CMDBs are back?**

In the 2010s, 2nd-generation CMDBs like [**ServiceNow**](https://www.servicenow.com/products/servicenow-platform/configuration-management-database.html) and [**Flexera**](https://www.flexera.com/) did thrive. They wrapped traditional CMDB ideas in IT service management (ITSM) workflows, discovery scanners, and compliance frameworks (which, by the way, had blossomed to eclipse ITIL and become another beast driving an entire industry called "compliance").

For companies running fleets of virtual machines that were subject to regulation and beholden to compliance frameworks, they worked well enough.

However, by the late 2010s, the cloud has become an oversaturated, heterogeneous, messy mess of messes. AWS has thousands of SKUs, there are specialty vendors galore, and AI started to drive an overabundance of resources: some ephemeral, some serverless, some fully managed….and all of them sprawling.

Suddenly, companies realized they still needed a way to inventory their world across their entire environment without becoming trapped in the process-driven CMDB of yesteryear. In a constantly changing, API-driven cloud world, the CMDB needed to change.

### **Cloud CMDBs are for modern cloud environments**

Today, a CMDB isn’t really a CMDB anymore: it is a cloud inventory, with a real-time graph of your cloud infrastructure across your entire environment. Cloud CMDBs at its core must be a data pipeline, automatically reading and managing thousands of cloud provider APIs, making that data accessible in a standardized SQL format for analysis and integration by customers.

While this may sound straightforward, the modern cloud is a tricky beast:

- Ephemeral resources galore means it must be updated continuously
- Complex API relationships (many accounts, many regions, hundreds-thousands of different APIs per vendor)
- APIs have rate limits (d’oh!)
- Data structures aren’t normalized, and are at times poorly documented

It turns out that making your own modern CMDB might be a harder challenge than you expected.

Here’s the plot twist: in the age of AI mania, cloud sprawl, and platform engineering, a CMDB is foundational to a business that needs to understand the state of their cloud infrastructure. Whether they are governing, securing, optimizing cost, automating, or simply reporting, authoritative configuration and asset data gives companies the confidence they need to achieve their goals.

The legacy CMDB might be dead, but it's been reborn for the cloud age. Not as a static database, but as a living, breathing inventory of your entire cloud estate. Maybe it wasn't dead all along, but just built for the wrong era. Who wants to struggle under the burden of process anyway?

If you want to automate your multi-cloud asset inventory, [**get started with CloudQuery**](https://www.cloudquery.io/download) — the leading open-source Cloud CMDB — or [**explore the CloudQuery Platform**](https://cloud.cloudquery.io/) for a fully managed experience. Want to discuss your specific use case? [**Contact us**](https://www.cloudquery.io/contact-us) or join the [**CloudQuery community**](https://community.cloudquery.io/) to connect with other users and experts.

---

*Originally published on [CloudQuery's Blog](https://www.cloudquery.io/blog/a-history-of-cmdbs)*
