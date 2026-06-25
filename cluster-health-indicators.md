---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-25"

keywords: cluster indicators, cluster status, cluster warnings, cluster health, capacity indicators, IBM Fusion as a service alerts

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding cluster health indicators
{: #cluster-health-indicators}

Review the indicators in the cluster list and cluster details to understand cluster status, Fusion services state, and whether a cluster needs attention.
{: shortdesc}

## Where indicators appear
{: #indicator-locations}

You can review cluster health and status indicators in the following places:

- The cluster list in the **Clusters** tab.
- The cluster details page for an individual cluster.

## Indicators in the cluster list
{: #cluster-list-indicators}

The cluster list table displays several types of information that help you understand the current cluster state.

Status
:   Shows the operational status of the cluster, such as "Available", "Warning", or "Error". Status values are derived from Red Hat OpenShift on IBM Cloud cluster health.

vCPU
:   Displays the number of virtual CPUs allocated to the cluster.

Memory
:   Shows the amount of memory allocated to the cluster.

Storage
:   Displays the storage quota and current usage when Fusion services are enabled for the cluster. This column shows values in TB format (for example, "5 TB of 10 TB").

Warning and health indicators
:   Visual indicators such as warning icons or status badges that appear when a cluster has conditions that might require attention.

## Understanding warnings and health states
{: #cluster-health-states}

Cluster status values reflect the health status from Red Hat OpenShift on IBM Cloud (ROKS). Warnings and health indicators help you identify the following conditions:

- A cluster that is operating normally (Available status).
- A cluster that has a warning condition (Warning status).
- A cluster that has an error or another condition that might require action (Error status).
- A cluster that should be reviewed in more detail.
- Clusters that already have Fusion services enabled (shown in the Storage column).
- Clusters that might be approaching their storage quota limit.
- Clusters with specific resource allocations (vCPU and memory values).

For detailed cluster diagnostics and troubleshooting beyond what is shown in the IBM Fusion as a service UI, refer to the [Red Hat OpenShift on IBM Cloud documentation](/docs/openshift).
{: note}

## When to open cluster details
{: #when-to-review-details}

Open cluster details when the cluster list shows one of the following conditions:

- A warning or health indicator.
- A status that does not match the expected cluster condition.
- A storage usage value that looks close to the assigned quota.
- A Fusion services status that is not the expected state.
- A cluster that you want to review in more detail.

## Reviewing cluster details
{: #review-cluster-details}

When you open cluster details, review the available alert, warning, or storage information to understand the current condition of the cluster.

In cluster details, you can:

- View detailed status information (status comes from ROKS cluster health).
- Review storage quota and usage metrics.
- Check for alerts or warnings that require action.
- Access the OpenShift console for cluster-level operations.

For cluster-level diagnostics, health checks, and troubleshooting that go beyond storage and quota management, use the Red Hat OpenShift on IBM Cloud console and documentation.
{: tip}

## Next steps
{: #cluster-health-next}

After reviewing cluster health indicators, you can:

- [View cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status)
- [Identify clusters that need attention](/docs/cephaas?topic=cephaas-monitor-cluster-health)
- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota)
- [Take corrective action using the Fix flow](/docs/cephaas?topic=cephaas-fix-flow-corrective-action)
