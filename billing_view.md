---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-20"

keywords: administration, billing, platform, ceph as a service, cephaas, invoices, storage tiers, performance tier,  capacity tier

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Billing
{: #billing}

This section provides you with an overview on pricing information and invoices for your service subscriptions.
{: shortdesc}



## Invoices
{: #billing-invoices}

To find your invoices, on the {{site.data.keyword.cloud_notm}} console, from the navigatation menu, go to **Manage > Billing and Usage > Invoices**.


## Pricing
{: #billing-pricing}

You can select the term (3, 4, or 5 years) performance tier or capacity tier that best matches your needs. {{site.data.keyword.cephaas_full_notm}} hardware contains optimized racks, servers, storage, networking switches, and software that is integrated, when connected to {{site.data.keyword.cloud_notm}}.

The Service is an infrastructure as a service (IaaS) offering where the operating system, middleware, and application software are licensed and managed by IBM. The hardware is owned and maintained by IBM and the service infrastructure is installed in your designated data center.

## Storage tiers
{: #billing-request-classes}

### Performance tier
{: #performance-tier}

The Performance Tier of {{site.data.keyword.cephaas_full_notm}} is tailored to performance-intensive application workloads. To serve these workloads, the hardware consists of NVMe storage devices and high-bandwidth network cards as well as the CPU and memory components that are needed to use this equipment.

Typical workloads for this tier includes support for VM infrastructure with storage or services for high-performance object storage.

When committing to a certain capacity, the delivered hardware includes at least 30% extra capacity for optional excess usage.

This tier is offered in the following capacity options for the terms 3, 4, or 5 years:

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

The Capacity tier of {{site.data.keyword.cephaas_full_notm}} offers cost-effective online storage of less frequently used data.

Typical workloads for this tier are backup workloads. The storage capacity can grow easily over time as more backups are written. The client pays only for what they need, while their data stays on-premises and IBM Site Reliability Engineering (SRE) team keeps the data available.

When committing to a certain capacity, the delivered hardware includes at least 30% extra capacity for optional excess usage.

This tier is offered in the following capacity options for the terms 3, 4, or 5 years:

- 800 TB
- 1600 TB
- 2400 TB
- 3200 TB

## Understanding your overall capacity and overage charges
{: #overall-capacity}

For each deployment, the hardware setup includes the committed monthly capacity along with an extra 30% burst capacity. Burst capacity allows you to temporarily expand your overall available capacity, if needed.

If you exceed your committed capacity and start using the burst capacity, overage fees are applied based on the extra capacity used.

Burst capacity is included by default in the deployment. However, you have the option to opt out.

Your overall available capacity consists of the committed capacity that is combined with the burst capacity.
