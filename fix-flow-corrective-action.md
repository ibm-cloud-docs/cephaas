---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: Fix flow, corrective action, cluster issues, Fusion as a Service troubleshooting

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Taking corrective action using the Fix flow
{: #fix-flow-corrective-action}

Use the Fix flow when the Fusion as a Service UI provides a guided action for resolving a cluster issue.
{: shortdesc}

## When to use the Fix flow
{: #about-fix-flow}

Use the Fix flow when a cluster warning or alert includes an available corrective action in the UI.

The Fix flow can help you do the following tasks:

- Review the issue that affects the cluster.
- Apply a guided action from the UI.
- Confirm that the selected action is complete.

## Open the Fix flow
{: #access-fix-flow}

1. Open your Fusion as a Service deployment.
2. Click the **Clusters** tab.
3. Open the cluster details page for a cluster that needs attention.
4. Review the warning or alert information.
5. Open the available **Fix** action, if the UI shows one.

## After you complete the Fix flow
{: #verification}

After you complete the Fix flow, review the cluster again to confirm the current status.

You might also need to do one of the following tasks:

- Review alerts and metrics again.
- Update the cluster quota.
- Open the OpenShift console for further investigation.

## Related tasks
{: #fix-flow-next}

- [Review alerts and usage metrics](/docs/sdsaas?topic=sdsaas-review-alerts-metrics)
- [Update a cluster's storage quota](/docs/sdsaas?topic=sdsaas-update-cluster-quota)
- [Identify cluster warnings and health states](/docs/sdsaas?topic=sdsaas-cluster-warnings-health)
- [View storage status for a cluster](/docs/sdsaas?topic=sdsaas-view-cluster-storage-status)
