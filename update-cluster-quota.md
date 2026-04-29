---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: update cluster quota, cluster storage quota, Fusion as a Service quota, storage settings

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Updating a cluster's storage quota
{: #update-cluster-quota}

Change the storage quota for a cluster that uses Fusion services in your Fusion as a Service deployment.
{: shortdesc}

## Before you begin
{: #update-cluster-quota-prereqs}

Before you update a cluster quota, make sure that you meet the following requirements:

- You have administrator permissions for the deployment.
- Fusion services are enabled for the cluster.
- The deployment has enough available storage capacity for the new value, if you are increasing the quota.

## Update the cluster quota
{: #update-quota-steps}

1. Open your Fusion as a Service deployment.
2. Click the **Clusters** tab.
3. In the cluster list, click the cluster name.
4. On the cluster details page, open the storage management action for the cluster.
5. Enter the updated quota value.
6. Save the change.

The new value is applied to the cluster after the update completes.

## Things to check before you change the quota
{: #quota-validation-update}

Review the following points before you save the new value:

- If you increase the quota, make sure that the deployment has enough available storage capacity.
- If you reduce the quota, make sure that the new value still supports the cluster's current usage.
- Review the cluster storage status after the update.

## Related tasks
{: #update-cluster-quota-next}

- [View storage status for a cluster](/docs/sdsaas?topic=sdsaas-view-cluster-storage-status)
- [View deployment capacity and resource usage](/docs/sdsaas?topic=sdsaas-view-deployment-capacity)
- [Understand storage quota validation and error states](/docs/sdsaas?topic=sdsaas-storage-quota-validation)
