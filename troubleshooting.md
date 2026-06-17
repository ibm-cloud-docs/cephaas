---

copyright:
 years: 2024, 2026
lastupdated: "2026-06-17"

keywords: Block volume, data storage, troubleshooting, troubleshoot, cephaas, ceph as a service, object storage, low cost object, 

subcollection: cephaas

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting
{: #troubleshooting}

When you create or manage Block and Object Storage for {{site.data.keyword.cephaas_full_notm}}, you might encounter issues. Often, you can recover by following a few steps. Issues, symptoms, likely causes, and resolutions are described in the following sections.
{: shortdesc}

## Cannot retrieve a volume in a specified deployment
{: #troubleshoot-topic-1}
{: troubleshoot}
{: support}

Information about a Block Storage volume or volumes can't be retrieved for a deployment.
{: tsSymptoms}

Any of the following causes might apply:
{: tsCauses}

* The volume name and information is missing in either the UI or CLI.
* You might also be attempting to access a volume in a deployment other than your deployment.
* You might be trying to access an obsolete volume.

Verify that the volume was not deleted from a deployment. Search for the deployment where you last accessed the volume from the list of all deployments:
{: tsResolve}

1. In the [{{site.data.keyword.cloud_notm}} console](/login){: external}, click the **Navigation menu** icon ![menu icon](../icons/icon_hamburger.svg) **> Resource List > Storage**.

1. Select a deployment from the list of all deployments.

If the volume does not appear in the list of volumes, it was probably deleted. Because deleting a volume completely removes its data, it cannot be restored.

If you use the CLI, verify that you entered the correct command syntax for viewing volumes. See [Viewing all Block Storage volumes from the CLI](/docs/cephaas?topic=cephaas-view-volume&interface=cli#viewall-vol-cli).

## Cannot update a volume name by using the API or CLI
{: #troubleshoot-topic-2}
{: troubleshoot}
{: support}

You receive an error message when you attempt to rename an existing volume.
{: tsSymptoms}

This condition might appear in the API or CLI in the following scenarios.

* In the API, when you send a `PATCH` request to rename the volume.
* In the CLI, when you specify the `ibmcloud is volume-update` command.

You might be renaming the volume with an invalid volume name. In this case, you see a `400 - validation_invalid_name` error.
You might also be specifying a valid volume name, but one that is already in the {{site.data.keyword.cephaas_full_notm}}. For example, if you create two volumes from compute resources that are in the same deployment, and have the same name, you see a `400 - volume_name_duplicate` error.
{: tsCauses}

**Note:** The UI prevents you from entering an invalid volume name.

Follow these guidelines for valid volume names:
{: tsResolve}

* Volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters.
* Volume names must begin with a lowercase letter.
* Volume names must be unique across a deployment.

## Cannot delete a volume by name or ID
{: #troubleshoot-topic-3}
{: troubleshoot}
{: support}

You can't delete a Block Storage volume by name or ID.
{: tsSymptoms}

The volume name and ID are not accepted.
{: tsCauses}

Verify that the volume name or identifier is correct and that the volume is not mapped to a host. Also, verify that the volume is not in a _pending_ state.
{: tsResolve}


## Unable to create a s3 certificate
{: #troubleshoot-topic-4}
{: troubleshoot}
{: support}

You receive an error message when you attempt to create s3 certificate.
{: tsSymptoms}

This condition might appear in the API or CLI in the following scenarios.

* In API: when you make a `POST` request.
* In CLI: when you run the command `ibmcloud sds cert-create`.

Trying to create a s3 certificate when one already exists.
{: tsCauses}

Follow these guidelines to replace the existing certificate with the new one:
{: tsResolve}

* In API: Make a `PUT /certificates/{cert_type}` request to upload the new s3 certificate. See [Updating S3 certificate with the API](/docs/cephaas?topic=cephaas-uploading-s3-certificate&interface=api#uploading-s3-certificate-api).

* In CLI: Use the command `cert-update` to upload the new s3 certificate. See [Updating S3 certificate with the CLI](/docs/cephaas?topic=cephaas-uploading-s3-certificate&interface=cli#updating-s3-certificate-cli).

## Storage quota validation fails
{: #troubleshoot-quota-validation}
{: troubleshoot}
{: support}

You receive an error message when you attempt to set a default cluster quota, enable Fusion services for a cluster, or update a cluster's storage quota.
{: tsSymptoms}

IBM Fusion as a service validates quota values during the following tasks:
{: tsCauses}

- Setting the default cluster quota during onboarding or from the Settings page
- Enabling Fusion services for a cluster
- Updating a cluster storage quota

Validation can fail for the following common reasons:

- The requested quota is larger than the available deployment capacity.
- The requested value is not valid for the current action.
- The requested value does not align with the cluster's current storage usage.

If validation fails, follow these steps to resolve the issue:
{: tsResolve}

1. Review the error message displayed in the UI to understand the specific validation issue.

2. Check the deployment's available capacity:
   - Navigate to your deployment dashboard
   - Review the storage utilization chart
   - Verify how much storage capacity is currently available

3. If you are updating an existing cluster quota, check the cluster's current storage status and usage:
   - Open the cluster details page
   - Review the storage usage information
   - Ensure the new quota value is greater than the current usage

4. Enter a different quota value that meets the validation requirements:
   - For default cluster quota: Choose a value that fits within available deployment capacity
   - For cluster quota updates: Choose a value that is greater than current usage and within available capacity

5. Save the change again after adjusting the quota value.

For more information, see:
- [Onboarding to your IBM Fusion as a service deployment](/docs/cephaas?topic=cephaas-onboarding-fusionaas)
- [Editing the default cluster storage quota](/docs/cephaas?topic=cephaas-manage-cluster-quota)
- [Updating a cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota)
- [Viewing storage status for a cluster](/docs/cephaas?topic=cephaas-view-cluster-storage-status)

## Resolving cluster issues
{: #troubleshoot-cluster-issues}
{: troubleshoot}
{: support}

A cluster shows warnings, alerts, or other conditions that might require attention.
{: tsSymptoms}

You might see this condition in the following situations:
{: tsCauses}

- A warning or health indicator appears in the cluster list.
- The cluster status does not match the expected condition.
- Storage usage is close to the assigned quota.
- An alert or warning appears on the cluster details page.
- Changes in available deployment capacity affect cluster operations.

Use the following actions to investigate and resolve the issue:
{: tsResolve}

1. Identify the cluster or deployment condition that requires review.

2. Open the cluster details page to review warnings, alerts, and storage information.

3. Determine the appropriate next action based on the current condition:
   - If storage capacity is the issue, [update the cluster's storage quota](/docs/cephaas?topic=cephaas-update-cluster-quota).
   - If the UI provides guided remediation, [use the Fix flow](/docs/cephaas?topic=cephaas-fix-flow-corrective-action).
   - If you need to investigate cluster-level details, [open the OpenShift console](/docs/cephaas?topic=cephaas-access-openshift-console).
   - If you need more detail about storage consumption, [view storage status for the cluster](/docs/cephaas?topic=cephaas-view-cluster-storage-status).

4. Review the cluster again after you complete the action to confirm that the warning or alert is resolved.

For more information, see:
- [Monitoring cluster health and responding to alerts](/docs/cephaas?topic=cephaas-monitor-cluster-health)
- [Taking corrective action using the Fix flow](/docs/cephaas?topic=cephaas-fix-flow-corrective-action)
- [Understanding cluster health indicators](/docs/cephaas?topic=cephaas-cluster-health-indicators)
- [Viewing storage status for a cluster](/docs/cephaas?topic=cephaas-view-cluster-storage-status)

## Storage not reclaimed after cluster deletion
{: #storage-not-reclaimed}
{: troubleshoot}
{: support}

When you delete a cluster in IBM Fusion as a service, the associated storage resources are expected to be released and returned to the available capacity of your deployment. However, in some cases, storage might not be fully reclaimed immediately.
{: tsSymptoms}

This issue can occur if storage resources are still in use, not properly detached, or if cleanup operations are delayed or incomplete. As a result, you might continue to see consumed storage capacity even after the cluster is deleted.
{: tsCauses}

Follow these troubleshooting steps to identify why storage is not reclaimed and how to resolve the issue.
{: tsResolve}

- Ensure that you have access to your IBM Fusion as a service deployment and IBM Cloud console.
- Make sure that the cluster you deleted is no longer required.

### Verify cluster deletion status
{: #verify-cluster-deletion}

1. Go to the IBM Cloud console.
2. Confirm that the cluster is fully deleted.

Check that the cluster is not in an intermediate state such as:
- Deleting
- Cleanup in progress

Storage reclamation starts only after the cluster is completely deleted.

### Check storage usage in your deployment
{: #check-storage-usage}

1. Open your IBM Fusion as a service deployment dashboard.
2. Review the storage usage and allocation.

Look for:
- Storage still marked as in use
- Resources that are not released

If storage is still allocated, it might not have been deleted or detached correctly.

### Verify persistent volumes and claims
{: #verify-persistent-volumes}

If you have access to cluster logs or resources, check for remaining PersistentVolumeClaims (PVCs) and PersistentVolumes (PVs).

Using the CLI:

```sh
oc get pvc --all-namespaces
oc get pv
```
{: pre}

If PVCs or PVs still exist, they might be preventing storage from being reclaimed. You might need to manually delete these resources.

### Contact IBM Support
{: #contact-support-storage}

If storage is not reclaimed after following these steps, contact IBM Support for assistance. Provide the following information:

- Deployment ID
- Cluster name or ID
- Time when the cluster was deleted
- Current storage usage details

For more information, see [Getting help and support](/docs/cephaas?topic=cephaas-getting-help-and-support).

## Understanding empty states
{: #ui-empty-states}

Review the empty states in IBM Fusion as a service so that you understand why a page has no items to show and what you can do next.

### Empty states in the deployment UI
{: #empty-states-overview}

An empty state appears when the current page or section does not have data to display yet.

For example, you might see an empty state when:

- The deployment is newly created and you see a welcome modal explaining that the deployment is ready to use.
- No clusters are associated with the deployment yet.
- No cluster has Fusion services enabled.
- The cluster list is empty and displays a message "No cluster yet" with the explanation "Once clusters are created in ROKs, you will see them here."
- No storage information is available yet for the selected context.

### How to use empty states
{: #no-clusters-actions}

Use the message in the empty state to understand what is missing and which next step is available.

Depending on your role and the current page, the empty state might help you do one of the following tasks:

- For the welcome banner: Click **Set cluster quota** to configure the default storage quota, or click **View your clusters** to see the cluster list.
- For an empty cluster list: Create clusters in ROKs as indicated in the empty state message.
- Review the deployment or cluster setup.
- Open another page, such as the **Clusters** tab.
- Continue with an available configuration action.
- Ask an administrator to complete an action that is not available to your role.

### Empty states and permissions
{: #restricted-empty}

Some empty states are informational only. Others reflect that a setup task is still required.

If you do not have permission to complete the next action, the UI can indicate that the page is read-only or that an administrator must complete the task.

### Related tasks
{: #transition-from-empty}

- [Viewing the cluster list](/docs/cephaas?topic=cephaas-view-cluster-list)
- [Enabling Fusion services for a cluster](/docs/cephaas?topic=cephaas-enable-fusion-services)
- [Understanding warning and read-only states](/docs/cephaas?topic=cephaas-ui-warning-readonly-states)
