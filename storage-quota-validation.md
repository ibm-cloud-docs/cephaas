---

copyright:
  years: 2024, 2026
lastupdated: "2026-04-29"

keywords: storage quota validation, quota errors, cluster quota validation, Fusion as a Service quota rules

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding storage quota validation and error states
{: #storage-quota-validation}

Review how Fusion as a Service validates storage quota values when you set a default quota, enable Fusion services, or update a cluster quota.
{: shortdesc}

## When validation happens
{: #quota-validation-overview}

Fusion as a Service validates quota values during the following tasks:

- Setting the default cluster quota.
- Enabling Fusion services for a cluster.
- Updating a cluster storage quota.

## What is validated
{: #validation-rules}

When you enter or update a quota, the UI can validate the following conditions:

- Whether the deployment has enough available storage capacity.
- Whether the value is acceptable for the action that you are performing.
- Whether the value is suitable for the cluster's current state and usage.

## Common reasons that validation fails
{: #common-validation-errors}

Validation can fail for the following common reasons:

- The requested quota is larger than the available deployment capacity.
- The requested value is not valid for the current action.
- The requested value does not align with the cluster's current storage usage.

## What to do when validation fails
{: #troubleshoot-validation}

If validation fails, review the information that is shown in the UI and then do the following tasks:

1. Check the deployment's available capacity.
2. Check the cluster's current storage status and usage, if you are updating an existing cluster quota.
3. Enter a different quota value.
4. Save the change again after the validation issue is resolved.

## Related tasks
{: #storage-quota-validation-next}

- [Set the default cluster storage quota](/docs/sdsaas?topic=sdsaas-set-default-cluster-quota)
- [Update a cluster's storage quota](/docs/sdsaas?topic=sdsaas-update-cluster-quota)
- [View storage status for a cluster](/docs/sdsaas?topic=sdsaas-view-cluster-storage-status)
