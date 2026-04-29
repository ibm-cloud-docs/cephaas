---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: empty states, no clusters, no storage enabled, Fusion as a Service UI states

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding empty states
{: #ui-empty-states}

Review the empty states in Fusion as a Service so that you understand why a page has no items to show and what you can do next.
{: shortdesc}

## Empty states in the deployment UI
{: #empty-states-overview}

An empty state appears when the current page or section does not have data to display yet.

For example, you might see an empty state when:

- The deployment is newly created and you see a welcome modal explaining that the deployment is ready to use.
- No clusters are associated with the deployment yet.
- No cluster has Fusion services enabled.
- The cluster list is empty and displays a message such as "There are no clusters available" with instructions to create clusters through the ROKS Satellite portal.
- No storage information is available yet for the selected context.

## How to use empty states
{: #no-clusters-actions}

Use the message in the empty state to understand what is missing and which next step is available.

Depending on your role and the current page, the empty state might help you do one of the following tasks:

- For the welcome modal: Click **Set cluster quota** to configure the default storage quota, or click **View your clusters** to see the cluster list.
- For an empty cluster list: Create clusters through the ROKS Satellite portal as indicated in the empty state message.
- Review the deployment or cluster setup.
- Open another page, such as the **Clusters** tab.
- Continue with an available configuration action.
- Ask an administrator to complete an action that is not available to your role.

## Empty states and permissions
{: #restricted-empty}

Some empty states are informational only. Others reflect that a setup task is still required.

If you do not have permission to complete the next action, the UI can indicate that the page is read-only or that an administrator must complete the task.

## Related tasks
{: #transition-from-empty}

- [Viewing the cluster list](/docs/sdsaas?topic=sdsaas-view-cluster-list)
- [Enabling Fusion services for a cluster](/docs/sdsaas?topic=sdsaas-enable-fusion-services)
- [Understanding warning and read-only states](/docs/sdsaas?topic=sdsaas-ui-warning-readonly-states)
