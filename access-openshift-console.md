---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-17"

keywords: OpenShift console, ROKS console, launch console, cluster console access, ROKS handoff, OpenShift operations, IBM Fusion as a service and OpenShift, cluster operations

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Accessing the Red Hat OpenShift console
{: #access-openshift-console}

Open the Red Hat OpenShift console from your IBM Fusion as a service deployment when you need to continue cluster and workload tasks in Red Hat OpenShift on IBM Cloud Satellite. Understanding when to use IBM Fusion as a service and when to use the Red Hat OpenShift console helps you work efficiently across both environments.
{: shortdesc}

Before you launch the OpenShift console, make sure that you can access the cluster from the {{site.data.keyword.cloud_notm}} console.

## Launching the Red Hat OpenShift console
{: #launch-console-steps}

1. Open your IBM Fusion as a service deployment.
2. Click the **Clusters** tab.
3. In the cluster list, click the cluster name.
4. On the cluster details page, click the link to open the Red Hat OpenShift console.

The Red Hat OpenShift console opens so that you can continue cluster-level and workload-level tasks.

## Understanding the division of responsibilities
{: #responsibility-division}

IBM Fusion as a service and Red Hat OpenShift each manage different aspects of your cluster environment. Understanding this division helps you know where to perform specific tasks.

### What IBM Fusion as a service manages
{: #fusionaas-responsibilities}

Use IBM Fusion as a service for deployment-level and quota-related tasks, such as the following actions:

- Reviewing and managing deployments.
- Viewing clusters that are associated with the deployment.
- Enabling Fusion services for clusters.
- Reviewing and updating cluster storage quotas.
- Reviewing cluster warnings, alerts, and storage status.

### What Red Hat OpenShift manages
{: #openshift-responsibilities}

Use the Red Hat OpenShift console for cluster-level and workload-level tasks, such as the following actions:

- Creating clusters.
- Performing cluster-level compute configurations.

## When to use the Red Hat OpenShift console
{: #console-use-cases}

Use the Red Hat OpenShift console for tasks that are managed in the cluster environment, such as workload and application operations.

You typically move to the Red Hat OpenShift console after you finish the IBM Fusion as a service task that prepares the cluster for storage use.

For example, you might do the following tasks in order:

1. Open the deployment in IBM Fusion as a service.
2. Enable Fusion services for the cluster, if needed.
3. Review the cluster quota and storage status.
4. Open the Red Hat OpenShift console to continue cluster-managed tasks.

## When to return to IBM Fusion as a service
{: #return-to-fusionaas}

Return to IBM Fusion as a service when you need to review or change deployment-managed settings, such as:

- Deployment capacity information.
- Cluster storage quotas.
- Deployment-level settings.
- Cluster warnings and alerts related to storage.

## Working across both environments
{: #cross-environment-workflow}

A typical workflow might involve moving between IBM Fusion as a service and Red Hat OpenShift:

1. Start in IBM Fusion as a service to review capacity and enable services.
2. Move to Red Hat OpenShift to create clusters and configure workloads.
3. Return to IBM Fusion as a service to adjust quotas or review storage status.

## Next steps
{: #access-console-next}

After launching the Red Hat OpenShift console, you can:

- [View cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status) in IBM Fusion as a service
- [Enable Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services)
- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota)
- [Monitor cluster health](/docs/cephaas?topic=cephaas-monitor-cluster-health)
