---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-12"

keywords: Block volume, data storage, troubleshooting, troubleshoot

subcollection: sdsaas

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting {{site.data.keyword.cephaas_short}}
{: #troubleshooting-block-storage}

When you create or manage Block and Object Storage for {{site.data.keyword.cephaas_short}}, you might encounter issues. Often, you can recover by following a few steps. Issues, symptoms, likely causes, and resolutions are described in the following sections.
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

If you use the CLI, verify that you entered the correct command syntax for viewing volumes. See [Viewing all Block Storage volumes from the CLI](/docs/sdsaas?topic=sdsaas-view-sds-volume&interface=cli#viewall-vol-cli).

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
You might also be specifying a valid volume name, but one that is already in the CephaaS. For example, if you create two volumes from compute resources that are in the same deployment, and have the same name, you see a `400 - volume_name_duplicate` error.
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


