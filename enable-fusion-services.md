---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: enable Fusion services, cluster storage, cluster quota, Fusion as a Service storage

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Enabling Fusion services for a cluster
{: #enable-fusion-services}

Enable Fusion services for a cluster so that the cluster can use storage capacity from your Fusion as a Service deployment.
{: shortdesc}

## Before you begin
{: #enable-fusion-services-prereqs}

Before you enable Fusion services, make sure that you meet the following requirements:

- You have administrator permissions for the deployment.
- The cluster is associated with the deployment.
- The deployment has available storage capacity.

## Enable Fusion services
{: #enable-fusion-steps}

1. Open your Fusion as a Service deployment.
2. Click the **Clusters** tab.
3. In the cluster list, select the cluster that you want to manage.
4. Open the cluster details page.
5. Click the action to enable Fusion services.
6. Review the assigned quota, if the UI shows a quota value during the flow.
7. Confirm the action.

After the action completes, the cluster can use deployment storage based on the assigned quota.

## What happens after you enable Fusion services
{: #post-enablement}

After Fusion services are enabled, you can do the following tasks:

- Review the cluster storage quota.
- Review storage usage for the cluster.
- Open the OpenShift console to continue workload-level storage tasks.

## Related tasks
{: #enable-fusion-services-next}

- [Update a cluster's storage quota](/docs/sdsaas?topic=sdsaas-update-cluster-quota)
- [View storage status for a cluster](/docs/sdsaas?topic=sdsaas-view-cluster-storage-status)
- [Understand storage quota validation and error states](/docs/sdsaas?topic=sdsaas-storage-quota-validation)
