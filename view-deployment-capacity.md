---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: Fusion as a Service deployment, deployment capacity, compute capacity, memory capacity, storage capacity, GPU capacity

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Viewing deployment capacity and resource usage
{: #view-deployment-capacity}

Review the capacity tiles on your Fusion as a Service deployment so that you can understand the available compute, memory, storage, and GPU resources.
{: shortdesc}

## Before you begin
{: #view-deployment-capacity-prereqs}

Before you review deployment capacity, make sure that you can access the deployment in the {{site.data.keyword.cloud_notm}} console.

## View deployment capacity
{: #view-capacity-info}

1. Open your Fusion as a Service deployment.
2. Review the capacity tiles on the deployment overview page.

The overview page displays the following capacity tiles:

vCPUs
:   Shows the number of virtual CPUs currently in use. This tile displays compute capacity available for cluster workloads.

Memory
:   Shows memory usage in TB format, displaying both used capacity and total available capacity (for example, "0 TB of 12 TB"). This helps you monitor memory allocation across clusters.

Storage
:   Shows storage capacity in TB format, displaying both allocated storage and total available storage (for example, "0 TB of 300 TB"). This capacity represents storage that can be assigned to clusters that use Fusion services.

GPUs
:   Shows the number of GPUs available (for example, "10"). This tile appears only when GPU resources are configured for the deployment.

## How to use the capacity tiles
{: #understand-capacity-metrics}

Use the capacity tiles to help you make deployment and cluster management decisions.

- Review **vCPUs** to understand compute capacity available for cluster workloads.
- Review **Memory** to see how much memory is allocated versus total available capacity before provisioning new clusters.
- Review **Storage** before you enable Fusion services or increase a cluster quota to ensure sufficient capacity is available.
- Review **GPUs** if your workloads depend on GPU-enabled capacity.
- Monitor the tiles regularly to identify changes in available resources and plan capacity accordingly.

## When to review deployment capacity
{: #monitor-usage-trends}

Review deployment capacity in the following situations:

- Before you enable Fusion services for a cluster.
- Before you set or change the default cluster quota.
- Before you increase a cluster storage quota.
- When you investigate capacity warnings or clusters that need attention.

## Related tasks
{: #view-deployment-capacity-next}

- [Set the default cluster storage quota](/docs/sdsaas?topic=sdsaas-set-default-cluster-quota)
- [Edit the default cluster quota](/docs/sdsaas?topic=sdsaas-edit-default-cluster-quota)
- [View the cluster list](/docs/sdsaas?topic=sdsaas-view-cluster-list)
