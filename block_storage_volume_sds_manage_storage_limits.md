---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-18"

keywords: volume, capacity, Block Storage

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing volume count and capacity limits
{: #manage-storage-limit}

SDSaaS offers block-level data storage volumes that can be attached to an instance as either a boot volume or as a data volume. Answer the following questions when you're ordering Block Storage volumes or requesting an increase in your volume or capacity limits.
{: shortdesc}

## Overview
{: #manage-storage-limit-overview}

With SDSaaS, you can create up to 750 boot and data Block Storage volumes per account in a region. You can request an increase of this quota by contacting [IBM Support](/unifiedsupport/cases/add){: external} and submitting a support case.

Capacity for secondary volumes ranges 10 - 16,000 GB. You can also expand volume capacity within its IOPS tier profile or custom band.


## Volume count and storage limits checklist
{: #manage-storage-limit-checklist}

Review the following checklist items and record your answers. Provide this information when you create a support case.

- **Ticket Subject**:
    >"*Request to Increase Block Storage Volume Count Limit*".

- **How many extra volumes do you need? Provide your account, region, and the zone where you want more volumes.**
    >*"200 volumes in US South-2"*.

- **Of the secondary volumes, how many secondary volumes do you need and of what capacity?**
    >*"75% of the secondary volumes are under 250 GB and 25% are up to 16,000 GB."*

- **How many total volumes use customer-managed encryption?**
    >*"100 volumes (or 50%) are to use customer-managed encryption".*

- **Provide an estimate of when you expect or plan to provision all of the requested volumes.**
    >*"I expect to create these volumes within 90 days".*

- **Provide a 90-day forecast of expected average capacity usage of these volumes.**
    >*"I expect 25% of the volumes to be used in 30 days, 50 percent to be used in 60 days and 75% to be used in 90 days".*
    >"*For secondary volumes, I expect to create 50% of the secondary volumes at less than 250 GB within 30 days and secondary volumes greater than 250 (if possible, estimate volume size) within 60 days."*

Respond promptly to all questions and statements in your request. They're necessary for processing and approval. If some things are unclear, there's opportunity to clarify your answers.
{: important}

You're notified about the update to your limits throughout the case process.
