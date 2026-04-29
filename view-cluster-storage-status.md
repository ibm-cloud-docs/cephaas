---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: cluster storage status, storage usage, cluster quota, Fusion as a Service storage

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Viewing storage status for a cluster
{: #view-cluster-storage-status}

Review storage status for a cluster to understand its Fusion services state, assigned quota, and current storage usage.
{: shortdesc}

## Before you begin
{: #view-cluster-storage-status-prereqs}

Before you review cluster storage status, make sure that you can open the deployment in the {{site.data.keyword.cloud_notm}} console.

## Open cluster storage status
{: #access-storage-status}

1. Open your Fusion as a Service deployment.
2. Click the **Clusters** tab.
3. In the cluster list, click the cluster name.

On the cluster details page, review the storage-related information that is shown for the cluster.

## Information shown for cluster storage
{: #storage-status-info}

The cluster details page can show the following storage information:

- Whether Fusion services are enabled for the cluster.
- The assigned storage quota.
- The current storage usage.
- Warning or status indicators related to storage.

## Why to review cluster storage status
{: #understand-storage-metrics}

Review cluster storage status in the following situations:

- After you enable Fusion services for a cluster.
- After you change a cluster quota.
- When you investigate a warning or alert.
- When you want to compare current usage with the assigned quota.

## Related tasks
{: #view-cluster-storage-status-next}

- [Update a cluster's storage quota](/docs/sdsaas?topic=sdsaas-update-cluster-quota)
- [Understand storage quota validation and error states](/docs/sdsaas?topic=sdsaas-storage-quota-validation)
- [Identify clusters that need attention](/docs/sdsaas?topic=sdsaas-clusters-need-attention)
