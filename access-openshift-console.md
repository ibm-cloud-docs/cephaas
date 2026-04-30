---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-30"

keywords: OpenShift console, ROKS console, launch console, cluster console access, ROKS handoff, OpenShift operations, Fusion as a Service and OpenShift, cluster operations

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Accessing the OpenShift console
{: #access-openshift-console}

Open the OpenShift console from your Fusion as a Service deployment when you need to continue cluster and workload tasks in Red Hat OpenShift on IBM Cloud. Understanding when to use Fusion as a Service and when to use the OpenShift console helps you work efficiently across both environments.
{: shortdesc}

Before you launch the OpenShift console, make sure that you can access the cluster from the {{site.data.keyword.cloud_notm}} console.

## Launching the OpenShift console
{: #launch-console-steps}

1. Open your Fusion as a Service deployment.
2. Click the **Clusters** tab.
3. In the cluster list, click the cluster name.
4. On the cluster details page, click the action to open the OpenShift console.

The OpenShift console opens so that you can continue cluster-level and workload-level tasks.

## Understanding the division of responsibilities
{: #responsibility-division}

Fusion as a Service and OpenShift each manage different aspects of your cluster environment. Understanding this division helps you know where to perform specific tasks.

### What Fusion as a Service manages
{: #fusionaas-responsibilities}

Use Fusion as a Service for deployment-level and quota-related tasks, such as the following actions:

- Reviewing deployment capacity.
- Viewing clusters that are associated with the deployment.
- Enabling Fusion services for a cluster.
- Reviewing and updating cluster storage quotas.
- Reviewing cluster warnings, alerts, and storage status.
- Managing deployment-level settings.

### What OpenShift manages
{: #openshift-responsibilities}

Use the OpenShift console for cluster-level and workload-level tasks, such as the following actions:

- Working with applications and workloads in the cluster.
- Continuing storage-related tasks inside the cluster environment.
- Managing resources that are handled in OpenShift.
- Performing cluster-level operations and configurations.

## When to use the OpenShift console
{: #console-use-cases}

Use the OpenShift console for tasks that are managed in the cluster environment, such as workload and application operations.

You typically move to the OpenShift console after you finish the Fusion as a Service task that prepares the cluster for storage use.

For example, you might do the following tasks in order:

1. Open the deployment in Fusion as a Service.
2. Enable Fusion services for the cluster, if needed.
3. Review the cluster quota and storage status.
4. Open the OpenShift console to continue cluster-managed tasks.

## When to return to Fusion as a Service
{: #return-to-fusionaas}

Return to Fusion as a Service when you need to review or change deployment-managed settings, such as:

- Deployment capacity information.
- Cluster storage quotas.
- Deployment-level settings.
- Cluster warnings and alerts related to storage.

## Working across both environments
{: #cross-environment-workflow}

A typical workflow might involve moving between Fusion as a Service and OpenShift:

1. Start in Fusion as a Service to review capacity and enable services.
2. Move to OpenShift to deploy applications and configure workloads.
3. Return to Fusion as a Service to adjust quotas or review storage status.
4. Continue in OpenShift for ongoing application management.

## Next steps
{: #access-console-next}

After launching the OpenShift console, you can:

- [View cluster details](/docs/sdsaas?topic=sdsaas-view-cluster-details) in Fusion as a Service
- [Enable Fusion services for a cluster](/docs/sdsaas?topic=sdsaas-enable-fusion-services)
- [Update a cluster's storage quota](/docs/sdsaas?topic=sdsaas-update-cluster-quota)
- [Monitor cluster health](/docs/sdsaas?topic=sdsaas-monitor-cluster-health)
