---

copyright:
  years: 2024
lastupdated: "2024-06-07"

keywords: list all volumes, view volume details

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Viewing block volumes
{: #viewing-block-storage}

View details about a block storage volume or summary information about all volumes.
{: shortdesc}

## Viewing information about block volumes in the UI
{: #viewvols}
{: ui}

List all block volumes and view details for a single volume. View attached SDSaaS block volume details in instance details.

### Viewing information about all volumes in the UI
{: #viewvols-ui}

To view all the Block storage volumes, in the [console], navigate to **Block Storage > Volumes**.

By default, SDSaaS block volumes display for all service instance in your region. In the list of all **Volumes**, you see the following information.

| Field | Description |
|-------|-------------|
| Name | Click the name of the volume to see individual volume details. |
| Status | Status of the volume, which functions as the default filter for all rows. |
| Provisioned size | Size of the volume you specified, in GBs.|
| Mapped hosts | |
{: caption="Table 1. Details about all volumes" caption-side="bottom"}

By default, 10 volumes are shown in the list of all SDSaaS volumes. Change this default by clicking the Page Control down arrow and increase the list to 20 or 50 volumes. Use the Page Control arrows after the list to go to the following page or return to the current page.

Actions menu on the Volume details page provides you with options to manage the volume information.

Table 2 describes the Actions menu options.

| Action | Description |
|--------|-------------|
| View volume details | Click to opens the detailed view of the Volume. |
| Rename volume | Click to change the volume name. |
| Map to host | Click to map the volume to a host. |
| Expand volume | |
| Delete | Delete the unattached volume. |
{: caption="Table 2. Actions menu options for volumes." caption-side="bottom"}

### Viewing details about a volume
{: #view-vol-details-ui}

To view details about a SDSaaS volume, go to the list of all SDSaaS volumes and click on the volume name whose details you want to view.

The Actions menu on the volume details page shows the actions that you can take.

The SDSaaS volumes details page shows volume details, attached virtual server instances, and backup policies. Table 3 describes this information.

| Field | Description |
|-------|-------------|
| **Volume details** | |
| Name  | Name of the volume you specified when you created the volume. Click the pencil icon to edit the volume name. The volume name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. Volume names must be unique for the account and for the region. |
| Volume ID | System-generated volume ID. |
| Created date | System-generated date when the volume was created.|
| Service instance | Name of the instance in your region.|
| IOPS | Current IOPS value for a predefined IOPS tier or the value you specified for custom IOPS. |
| Throughput | The performance a disk can deliver, measured in Gigabits/second (Gbps). Based on your volume profile, throughput is calculated as the amount of IOPS * 16 K block size.|
{: caption="Table 3. Volume details" caption-side="bottom"}

Table 4 shows Actions menu options from the volume details page.

| Action | Description |
|--------|-------------|
| Delete | Delete the volume. |
{: caption="Table 4. Actions menu options one the volume details page." caption-side="bottom"}

## Viewing SDSaaS volumes from the CLI
{: #viewing-block-storage-cli}
{: cli}

View details about a SDSaaS volume or summary information about all volumes from the CLI.

Before you can use the CLI, you must install the IBM Cloud CLI and the SDS CLI plug-in.
{: requirement}

1. Log in to the IBM Cloud.
   ```sh
   ibmcloud login --sso -a cloud.ibm.com
   ```
   {: pre}

   This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After successful authentication, you are prompted to choose your account. If you have access to multiple accounts, select the account that you want to log in as. Respond to any remaining prompts to finish logging in.


### Viewing details about a SDSaaS volume from the CLI
{: #viewvol-cli}

Specify this command to show details about a volume.

```sh
ibmcloud sds volume VOLUME_ID [--json]
```
{: pre}

The following example uses the volume ID to show volume details.

```sh
$ ibmcloud sds volume demo-volume-update
Getting volume demo-volume-update...

ID                                     r014-dee9736d-08ee-4992-ba8d-3b64a4f0baac
Name                                   demo-volume-update

<Waiting for example>
```
{: screen}





### Viewing all SDSaaS volumes from the CLI
{: #viewall-vol-cli}

Run this command to list summary information about all volumes:

```sh
ibmcloud sds volumes [--instanceid INSTANCEID]
```
{: pre}

Specifying the service instance ID filters the list to volumes that belong to the specified service instance. When you omit this argument, it defaults to all service instances.

By default, the first 25 volumes are displayed per page.

The following example shows all volumes for all service instances in your availability zone.

```sh
$ ibmcloud sds volumes

<waiting for example>

```
{: screen}

For more information about available command options, see [`ibmcloud sds volumes`](/docs/cli?topic=cli-sds-reference#volumes-list).

## View all volumes with the API
{: #viewing-block-storage-api}
{: api}

You can list all volumes and view details for a specific volume within all storage workspaces that you have access to.

Before you begin, make sure that you [set up your API environment].

### Viewing all SDSaaS volumes with the API
{: #viewall-vol-api}

Make a `GET /volumes` call to list summary information about all volumes. See the following example.

```sh
curl -X GET "$sds_api_endpoint/v1/volumes \
-H "Authorization: $iam_token"
```
{: pre}

A successful response looks like the following example. This example shows three data volumes. The first in the list is attached to an instance.

```json

Waiting for example

```

### Viewing volume details with the API
{: #viewvol-details-api}

Make a `GET /volumes/{volume_id}` call to see details of a volume. See the following example.

```sh
curl -X GET "$sds_api_endpoint/v1/volumes/ \
-H "Authorization: $iam_token"
```
{: pre}

A successful response provides details of the volume, including capacity and IOPS, the volume status, and whether the volume is mapped to a host.

```json
{
    "active": true,
    "bandwidth": 128,
    "busy": false,
    "capacity": 100,
    "created_at": "2019-01-29T06:26:17Z",
    "health_reasons": [],
    "health_state": "ok", // One of these values -[ degraded, faulted, inapplicable, ok ]
    "id": "ccbe6fe1-5680-4865-94d3-687076a38293",
    "iops": 1000,
    "name": "my-volume-1",
    "profile": {
        "name": "sds-general-purpose"
    },
    "resource_type": "volume",
    "status": "available", // one of these value- [ available, failed, pending, pending_deletion, unusable, updating ]
    "status_reasons": [],

    "service_instance_id": "xxxx",
    "storage_workspace_id": "yyyy",

   "host_mappings": [

          "host_nqn": "<host_nqn1>",
          "host_nqn": "<host_nqn2>"

    ]
}
```
{: codeblock}


## Next steps
{: #next-step-viewing-block-storage-volumes}

Create more volumes or manage your existing SDSaaS volumes.

* [Creating Block volumes]
* [Managing volumes]
