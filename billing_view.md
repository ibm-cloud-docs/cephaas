---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-10"

keywords: administration, billing, platform

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# Billing
{: #billing}

## View billing information
{: #view-billing-info}

For viewing your billing details, perform the following procedure.

1. Log in to your IBM Cloud account where your service instance is created.
2. From the top menu bar, select **Manage** > **Billing and usage**.
3. Click **Usage** in the left navigation panel.
4. Scroll down and find the row that is Ceph as a Service and click **View Plans**.
5. Select **View details** in the **Performance** row.
6. You can view all the service instances for the selected Performance Plan and the corresponding usage data along with the incurred costs.


## {{site.data.keyword.cephaas_full_notm}} Pricing
{: #billing-pricing}

You can select the term (1, 2, 3, 4, or 5 years), performance tier or capacity tier which best matches your needs. IBM Storage Ceph as a Service hardware contains optimized rack(s), servers, storage, networking switches, and software integrated, which connect to the IBM Cloud.

The Service is an infrastructure as a service (IaaS) offering where the operating system, middleware, and application software is licensed and managed by IBM. The hardware is owned and maintained by IBM and the service infrastructure is installed in your designated datacenter.

## Storage tiers
{: #billing-request-classes}

### Performance tier
{: #performance-tier}

The Performance Tier of IBM Storage Ceph as a Service is tailored to performance intensive application workloads. To serve these workloads, the hardware consists of NVMe storage devices and high-bandwidth network cards as well as the CPU and memory components needed to utilize this equipment.

Typical workloads for this tier are supporting VM infrastructure with storage or service high-performance object storage.

When committing to a certain capacity, the delivered hardware includes at least 30% extra capacity for optional excess usage.

This Tier is offered in the following capacity options:

- 100 TB
- 200 TB
- 300 TB
- 400 TB
- 500 TB
- 600 TB
- 700 TB
- 800 TB

### Capacity tier
{: #capacity-tier}

The Capacity tier of IBM Storage Ceph as a Service offers cost-effective online storage of less frequently used data.

Typical workloads for this tier are backup workloads. The storage capacity can grow easily over time as more backups are written. Client only pays for what they need, while their data stays on-premises and IBM Site Reliability Engineering (SRE) team keeps the data available.

When committing to a certain capacity, the delivered hardware includes at least 30% extra capacity for optional excess usage.

This tier is offered in the following capacity options:

- 800 TB
- 1600 TB
- 2400 TB
- 3200 TB

## Understanding your overall capacity
{: #overall-capacity}

For each deployment, the hardware setup includes the committed monthly capacity along with an additional 30% burst capacity. Burst capacity allows you to temporarily expand your overall available capacity, if needed.

If you exceed your committed capacity and start utilizing the burst capacity, overage fees will apply based on the extra capacity used.

Burst capacity is included by default in the deployment. However, you have the option to opt out.

Your overall available capacity consists of the committed capacity combined with the burst capacity.
