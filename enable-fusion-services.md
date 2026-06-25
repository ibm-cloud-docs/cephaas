---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-25"

keywords: enable Fusion services, cluster storage, cluster quota, IBM Fusion as a service storage

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Enabling Fusion services for a cluster
{: #enable-fusion-services}

Before you enable Fusion services, make sure that you meet the following requirements:

- You have administrator permissions for the deployment.
- The cluster is associated with the deployment.
- The deployment has available storage capacity.

## Understanding Fusion services
{: #about-fusion-services}

When you enable Fusion services for a cluster, you activate the following capabilities:

Fusion Data Foundation
:   Provides software-defined storage for the cluster.

Backup and restore
:   Enables backup and restore capabilities for cluster data protection.

Enabling Fusion services activates both FDF and BNR together. This action cannot be undone.

The enablement process typically takes a few minutes to complete. During this time, you may see temporary errors or experience issues with quota updates. These are expected and should resolve automatically once the enablement process completes.
{: note}

## Enabling Fusion services
{: #enable-fusion-steps}

1. Open your IBM Fusion as a service deployment.
2. In the left navigation, click **Clusters**.
3. In the cluster list, locate the cluster for which you want to enable Fusion services.
4. Click the cluster name to open the cluster details page.
5. In the cluster details page, click the **Manage storage** button or the overflow menu (⋯) and select **Manage storage**.

   The **Manage cluster storage** side panel opens.

6. Review the information in the side panel:

   **Enable Fusion Services to use storage, backup, and restore capabilities in this cluster.**

7. Toggle the **Enable Fusion services** switch to the on position.

8. Click **Save** to enable Fusion services, or click **Cancel** to close the side panel without making changes.

After you save, the enablement process begins. This process typically takes 5 to 10 minutes to complete.

## What to expect during enablement
{: #enablement-process}

While Fusion services are being enabled for your cluster:

- The process runs in the background and may take 5 to 10 minutes.
- You may see temporary errors in the UI during this time.
- Quota update operations may fail temporarily.
- These conditions are expected and should resolve automatically once enablement completes.

## Next steps
{: #enable-fusion-services-next}

After you enable Fusion services for a cluster, you can:

- [View cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status) to monitor storage usage and cluster status
- [Update the cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota) to adjust the allocated storage capacity
- [Edit the default cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota) to change the default quota for future clusters
- [Access the OpenShift console](/docs/cephaas?topic=cephaas-access-openshift-console) to manage workload-level storage tasks

If you encounter quota validation errors, see [Storage quota validation fails](/docs/cephaas?topic=cephaas-troubleshooting#troubleshoot-quota-validation).
