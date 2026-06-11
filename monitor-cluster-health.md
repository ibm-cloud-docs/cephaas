---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-11"

keywords: clusters need attention, cluster alerts, cluster issues, Fusion as a Service monitoring, alerts, metrics, cluster monitoring, usage metrics

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring cluster health and responding to alerts
{: #monitor-cluster-health}

Use the cluster list and cluster details to identify clusters that have warnings, alerts, or other conditions that might require action. Review alerts and usage information to understand current cluster conditions and identify possible issues.
{: shortdesc}

## Where to monitor cluster health
{: #monitoring-locations}

You can identify clusters that need attention and review alerts and usage information in the following places:

- The deployment overview page, where you review deployment capacity.
- The **Clusters** tab, where the cluster list shows current cluster status and indicators.
- The cluster details page, where you can review more detailed warning, alert, and storage information.

## Signs that a cluster needs attention
{: #attention-indicators}

A cluster might need attention when you see one or more of the following conditions:

- A warning or health indicator in the cluster list.
- A status that does not match the expected cluster condition.
- Storage usage that appears close to the assigned quota.
- An alert or warning on the cluster details page.
- Changes in available deployment capacity that affect cluster operations.

## What to review
{: #review-alerts-metrics}

When you review alerts and metrics, focus on the following items:

- Warning or health indicators for the cluster.
- Storage quota and storage usage for clusters that use Fusion services.
- Changes in available deployment capacity.
- Any cluster condition that suggests the cluster might need attention.
- Detailed status information in cluster details.

## Responding to alerts and warnings
{: #response-workflow}

If a cluster needs attention, follow these steps:

1. Identify the cluster or deployment condition that requires review.
2. Open the cluster details page to get more information.
3. Review the available warnings, alerts, and storage information.
4. Decide whether you need to update the cluster quota, use the Fix flow, or continue investigation in the OpenShift console.

Use the information that you review to determine the appropriate next action based on the specific condition.

## Common scenarios requiring attention
{: #common-scenarios}

The following scenarios typically require review or action:

Storage quota approaching limit
:   When a cluster's storage usage is close to its assigned quota, you might need to increase the quota or investigate storage consumption.

Warning status
:   A warning status indicates a condition that should be reviewed, even if the cluster is still operational.

Unexpected status changes
:   If a cluster's status changes unexpectedly, review cluster details to understand the cause.

Capacity constraints
:   Changes in deployment capacity might affect your ability to allocate additional resources to clusters.

## Taking corrective action
{: #corrective-actions}

After identifying a cluster that needs attention, you can take the following actions:

- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota) if storage capacity is the issue.
- [Use the Fix flow](/docs/cephaas?topic=cephaas-fix-flow-corrective-action) for guided corrective actions.
- [Launch the OpenShift console](/docs/cephaas?topic=cephaas-access-openshift-console) to investigate cluster-level issues.
- [View storage status](/docs/cephaas?topic=cephaas-view-cluster-storage-status) for detailed storage information.

## Next steps
{: #monitor-health-next}

After monitoring cluster health and responding to alerts, you can:

- [View cluster details](/docs/cephaas?topic=cephaas-view-cluster-storage-status)
- [Understand cluster health indicators](/docs/cephaas?topic=cephaas-cluster-health-indicators)
- [Take corrective action using the Fix flow](/docs/cephaas?topic=cephaas-fix-flow-corrective-action)
- [Update a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota)
