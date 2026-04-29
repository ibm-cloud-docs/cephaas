---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: default cluster quota, deployment settings, storage quota, Fusion as a Service admin tasks, edit default cluster quota

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing the default cluster storage quota
{: #manage-cluster-quota}

Set and edit the default storage quota that Fusion as a Service applies when you enable Fusion services for a cluster. The default quota provides a consistent starting point for cluster storage allocation.
{: shortdesc}

## About the default cluster quota
{: #about-default-quota}

The default cluster storage quota is the amount of storage capacity that is automatically allocated when you enable Fusion services for a cluster. This setting provides a consistent baseline for storage allocation across your deployment.

The default quota is used in the following situations:

- When an administrator enables Fusion services for a cluster and uses the default value.
- When a new cluster needs an initial storage allocation from the deployment.
- When administrators want a consistent starting quota across clusters.

The default quota affects only future enablement of Fusion services. It does not change existing cluster quotas or current storage usage.

## Before you begin
{: #manage-quota-prereqs}

Make sure that you meet the following requirements:

- You have administrator permissions for the deployment.
- You can open the deployment in the {{site.data.keyword.cloud_notm}} console.
- You know the quota value that you want to set in TB.

## Setting or editing the default cluster quota
{: #set-edit-quota-steps}

1. Open your Fusion as a Service deployment.
2. In the left navigation, click **Settings**.
3. In the **Storage** tile, click **Edit quota**.
4. In the **Set default cluster quota** side panel, enter or update the storage quota value in TB.
5. Click **Save**.

The updated default quota is applied to new clusters when Fusion services are enabled. Existing cluster quotas are not changed.

The side panel displays a message that explains: "This cluster quota will be the default amount of storage capacity allocated each time a cluster is created. This setting can be changed at a later time."

## Understanding the impact of quota changes
{: #quota-change-impact}

When you set or edit the default quota, keep the following considerations in mind:

- The value must fit within the available deployment storage capacity.
- A larger default quota reserves more storage capacity for future cluster use.
- The change affects only future cluster setup that uses the default value.

The change does not affect the following resources:

- Clusters that already have Fusion services enabled.
- Clusters that already use a custom quota.
- Current storage usage on existing clusters.

## Quota validation
{: #quota-validation}

When you set the default quota, the system validates that:

- The quota value is within acceptable limits.
- The deployment has sufficient available storage capacity.
- The value is appropriate for the deployment configuration.

If validation fails, review the error message and adjust the quota value accordingly.

## Next steps
{: #manage-quota-next}

After you set or edit the default quota, you can:

- [Enable Fusion services for a cluster](/docs/sdsaas?topic=sdsaas-enable-fusion-services) using the default quota
- [Update a cluster's storage quota](/docs/sdsaas?topic=sdsaas-update-cluster-quota) to customize individual cluster allocations
- [View deployment capacity](/docs/sdsaas?topic=sdsaas-view-deployment-capacity) to understand available resources
- [Understand admin vs non-admin permissions](/docs/sdsaas?topic=sdsaas-admin-permissions)
