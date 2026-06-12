---

copyright:
 years: 2024, 2026
lastupdated: "2026-06-12"

keywords: administration, billing, platform, ceph as a service, cephaas, fusion as a service, fusionaas, invoices, storage tiers, performance tier, capacity tier, compute billing, subscription terms

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Billing
{: #billing}

In Fusion as a Service, you can select the type of infrastructure you want to include in your deployment:

Compute
:   For managing compute resources such as vCPUs, memory, GPUs, and cluster deployments. Enables you to provision and manage Red Hat OpenShift on IBM Cloud Satellite clusters in your on-premises environment with fully managed IBM SRE support, self-service cluster provisioning, automated lifecycle management, and GPU support for AI and data-intensive workloads.

Storage
:   For managing block, file, and object storage capacity across your workloads. Provides access to IBM Storage Ceph as a Service with performance tiers optimized for your specific requirements, supporting multiple protocols and self-provisioning capabilities.

You can select both Compute and Storage options to create a complete on-premises cloud platform with integrated management and unified billing.

### Subscription terms
{: #subscription-terms}

Both {{site.data.keyword.cephaas_full_notm}} and Fusion as a Service offer flexible subscription terms:

- **3 years**: Standard subscription term
- **4 years**: Extended subscription with cost savings
- **5 years**: Maximum subscription term with optimal cost savings

Longer subscription terms provide better pricing and help you plan your infrastructure costs over an extended period, eliminating large upfront capital expenditures while providing predictable operational expenses.

### Invoices
{: #billing-invoices}

To find your invoices, on the {{site.data.keyword.cloud_notm}} console, from the navigation menu, go to **Manage > Billing and Usage > Invoices**.

## Storage billing
{: #storage-billing}

Storage billing applies to the Storage component of Fusion as a Service. IBM offers two storage tiers optimized for different workload requirements.

### Storage tiers
{: #billing-request-classes}

#### Performance tier
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

#### Capacity tier
{: #capacity-tier}

The Capacity tier of {{site.data.keyword.cephaas_full_notm}} offers cost-effective online storage of less frequently used data.

Typical workloads for this tier are backup workloads. The storage capacity can grow easily over time as more backups are written. The client pays only for what they need, while their data stays on-premises and IBM Site Reliability Engineering (SRE) team keeps the data available.

When committing to a certain capacity, the delivered hardware includes at least 30% extra capacity for optional excess usage.

This tier is offered in the following capacity options for the terms 3, 4, or 5 years:

- 800 TB
- 1600 TB
- 2400 TB
- 3200 TB

### Understanding your overall capacity and overage charges
{: #overall-capacity}

For each deployment, the hardware setup includes the committed monthly capacity along with an extra 30% burst capacity. Burst capacity allows you to temporarily expand your overall available capacity, if needed.

If you exceed your committed capacity and start using the burst capacity, overage fees are applied based on the extra capacity used.

Burst capacity is included by default in the deployment. However, you have the option to opt out.

Your overall available capacity consists of the committed capacity that is combined with the burst capacity.

## Compute billing
{: #compute-billing}

Fusion as a Service (FusionaaS) offers flexible billing options for compute resources. You can select either Compute or Storage infrastructure, or both, depending on your needs.


### Compute pricing model
{: #compute-pricing-model}

FusionaaS Compute provides cloud consumption pricing with a pay-for-what-you-use model. You provision Red Hat OpenShift clusters through the {{site.data.keyword.cloud_notm}} console and pay only for the resources you consume, with flexible monthly commitments and no large upfront capital expenditures.

### Compute billing components
{: #compute-billing-components}

FusionaaS Compute billing is based on the following resource types:

vCPUs
:   Virtual CPU resources allocated to your Red Hat OpenShift clusters. Billing is based on the number of vCPUs provisioned across all your clusters.

Memory
:   Memory capacity allocated to your clusters. Billing is based on the total memory (in GB or TB) provisioned across all your clusters.

GPUs
:   GPU resources for AI, machine learning, and high-performance computing workloads. Billing is based on the number and type of GPUs allocated to your clusters (if configured).

Storage quota
:   Storage capacity allocated to clusters when Fusion services are enabled. This represents the amount of storage from your deployment that clusters can consume. Billing for storage follows the storage tier pricing described in the Storage tiers section.

### How Compute billing works
{: #how-compute-billing-works}

When you create a Red Hat OpenShift cluster in your FusionaaS deployment:

1. You specify the cluster configuration including number of worker nodes, vCPUs per node, memory per node, and optional GPU resources.
2. The system allocates the requested resources from your deployment's available capacity.
3. You are billed for the allocated resources based on your subscription term and usage.
4. If you enable Fusion services for the cluster, you assign a storage quota that determines how much storage capacity the cluster can consume.
5. Storage usage is billed separately based on the storage tier and capacity consumed.

### Viewing Compute usage
{: #viewing-compute-usage}

You can view your Compute resource usage in the FusionaaS deployment dashboard:

- **vCPUs**: Number of virtual CPUs currently in use across all clusters
- **Memory**: Memory usage in TB format (used capacity of total available)
- **Storage**: Storage capacity in TB format (allocated storage of total available)
- **GPUs**: Number of GPUs in use (if configured)

These capacity tiles help you understand resource consumption and plan for future capacity needs.

### Compute capacity management
{: #compute-capacity-management}

FusionaaS provides flexible capacity management:

- **Self-service provisioning**: Create and delete clusters on-demand through the {{site.data.keyword.cloud_notm}} console
- **Elastic scaling**: Scale cluster resources up or down based on workload requirements
- **Capacity monitoring**: Track resource usage and available capacity in real-time
- **Capacity expansion**: Work with IBM to add compute, storage, or GPU capacity as your needs grow

If your deployment approaches its capacity limit, you may not be able to create additional clusters or increase existing cluster resources. Review deployment capacity regularly and contact your IBM representative to plan capacity expansions if needed.
