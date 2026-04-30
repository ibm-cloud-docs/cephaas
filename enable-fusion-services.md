---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-30"

keywords: enable Fusion services, cluster storage, cluster quota, Fusion as a Service storage

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Enabling Fusion services for a cluster
{: #enable-fusion-services}

Enable Fusion services for a cluster so that the cluster's workloads can access block, file, and object storage from your Fusion as a Service deployment.
{: shortdesc}

Before you enable Fusion services, make sure that you meet the following requirements:

- You have administrator permissions for the deployment.
- The cluster is associated with the deployment.
- The deployment has available storage capacity.

## Understanding Fusion services
{: #about-fusion-services}

When you enable Fusion services for a cluster, you grant the cluster permission to use storage in the deployment. This action cannot be undone.

After Fusion services are enabled, the cluster can access block, file and object storage.

## Enabling Fusion services
{: #enable-fusion-steps}

1. Open your Fusion as a Service deployment.
2. In the left navigation, click **Clusters**.
3. In the cluster list, locate the cluster for which you want to enable Fusion services.
4. Click the cluster name to open the cluster details page.
5. In the cluster details page, click the **Manage storage** button or the overflow menu (⋯) and select **Manage storage**.

   The **Manage cluster storage** side panel opens.

6. Review the information in the side panel:

   **For this cluster to begin using deployment storage, Fusion services must be enabled. This allows workloads to access block, file, and object storage.**

   **Grants this cluster permission to use storage in this deployment. This action cannot be undone.**

7. Toggle the **Enable Fusion services** switch to the on position.

8. Click **Save** to enable Fusion services, or click **Cancel** to close the side panel without making changes.

After you save, Fusion services are enabled for the cluster. The cluster can now use deployment storage based on the assigned quota.

## What happens after you enable Fusion services
{: #post-enablement}

After Fusion services are enabled, you can do the following tasks:

- Review the cluster storage quota.
- Review storage usage for the cluster.
- Open the OpenShift console to continue workload-level storage tasks.

## Next steps
{: #enable-fusion-services-next}

After you enable Fusion services for a cluster, you can:

- [Update the cluster's storage quota](/docs/sdsaas?topic=sdsaas-update-cluster-quota) to adjust the allocated storage capacity
- [View storage status for the cluster](/docs/sdsaas?topic=sdsaas-view-cluster-storage-status) to monitor storage usage
- [Access the OpenShift console](/docs/sdsaas?topic=sdsaas-access-openshift-console) to manage workload-level storage tasks

If you encounter quota validation errors, see [Troubleshooting](/docs/sdsaas?topic=sdsaas-troubleshooting#troubleshoot-quota-validation).
