---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-30"

keywords: list all volumes, view volume details

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# View block volumes
{: #view-sds-volume}

View details about a block storage volume or summary information about all volumes for the chosen service instance.
{: shortdesc}

## Viewing volume details in the UI
{: #viewvols}
{: ui}

You can view a summary of all volumes and view details for a single volume for the chosen deployment.

### Viewing summay information of all volumes in the UI
{: #viewvols-ui}

To view all the Block storage volumes, in the [console], navigate to **Block Storage > Volumes**.

By default, all SDSaaS volumes are displayed for the chosen service instance. In the list of all **Volumes**, you see the following information.

| Field | Description |
|-------|-------------|
| Name | Click the name of the volume to see individual volume details. |
| Status | Status of the volume |
| Provisioned size | Size of the volume you specified, in GBs.|
| Mapped hosts | Shows the count of number of hosts mapped to the volume. |
{: caption="Table 1. Details about all volumes" caption-side="bottom"}

By default, 10 volumes are shown in the list of all SDSaaS volumes. Change this default by clicking the Page Control down arrow and increase the list to 25, 50 or 100 volumes. Use the Page Control arrows after the list to go to the following page or return to the current page.



### Viewing details of a volume
{: #view-vol-details-ui}

To view details of a single volume, go to the list of all volumes and click on the volume name.

The volumes details page shows the details of the chosen volume and all its mapped hosts. Table 2 describes this information.

| Field | Description |
|-------|-------------|
| **Volume details** | |
| Name  | Name of the volume you specified when you created the volume. Click the pencil icon to edit the volume name. The volume name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. Volume names must be unique for the service instance. |
| Volume ID | System-generated volume ID. |
| Provisioned size | Size of the volume you specified, in GBs. |
| Created date | System-generated date when the volume was created.|
| Service instance | Name of the instance in the region.|
| IOPS | Current IOPS value for a predefined IOPS tier which is based on the default profile. |
| Throughput | The performance a disk can deliver, measured in Gigabytes/second (Gbps). Based on your volume profile, throughput is calculated as the amount of IOPS * 16 K block size.|
| Mapped hosts | Displays a list of all hosts present in the system.|
{: caption="Table 2. Volume details" caption-side="bottom"}


The Actions menu on the volume details page shows the actions that you can take.
Table 3 shows Actions menu options from the volume details page.

| Action | Description |
|--------|-------------|
| Expand volume | Allows you to increase the capacity of the volume. |
| Delete | Delete the volume. |
{: caption="Table 3. Actions menu options from the volume details page." caption-side="bottom"}

## Viewing volumes details from the CLI
{: #viewing-block-storage-cli}
{: cli}

View details about a SDSaaS volume or summary information about all volumes from the CLI.


### Viewing details of a single volume from the CLI
{: #viewvol-cli}

Run the following command to show volume details for a specific volume `ID` within the specific service `INSTANCEID`.

```sh
ibmcloud software-defined-storage volume --instanceid INSTANCEID --id ID
```
{: pre}


The following example uses the volume ID to show volume details.

```sh
$ ibmcloud sds volume --instanceid abc --url $sds_endpoint --id r134-3a7a8360-be78-4723-a341-356be350e683
Getting volume demo-volume-update...

ID             r134-3a7a8360-be78-4723-a341-356be350e683
Name           saved-sandblast-calcium-heftiness
Status         available
Mapped_Host    -
Capacity_GB    10
Created        2024-05-08T16:42:08Z

```
{: screen}





### Viewing list of all volumes from the CLI
{: #viewall-vol-cli}

Run this command to list summary information about all volumes:

```sh
ibmcloud software-defined-storage volumes [--instanceid INSTANCEID]
```
{: pre}

Specifying the service instance ID is required since it is used to filter the list of volumes that belong to the specified service instance.

The following example shows all volumes for the service instance specified in your availability zone.

```sh
ibmcloud software-defined-storage volumes --instanceid abc --url $sds_endpoint

ID                                          Name       Status      Capacity_GB   Mapped_Host
r134-2613272e-ff23-461e-94a3-3d3f77c13aa1   example2   available   10            -
r134-d75e1aeb-4bcf-4d41-8926-517198d55448   example1   available   10            -

```
{: screen}

For more information about available command options, run `ibmcloud sds volumes --help`.

## View all volumes with the API
{: #viewing-block-storage-api}
{: api}

You can list all volumes and view details for a specific volume within all storage workspaces that you have access to.

Before you begin, make sure that you [set up your API environment].

### Viewing all SDSaaS volumes with the API
{: #viewall-vol-api}

Make a `GET /volumes` call to list summary information about all volumes. See the following example.

```sh
curl -X GET "$sds_api_endpoint/v1/volumes --header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

A successful response looks like the following example. This example shows the first volume mapped to a host.

```json
{
  "first": {
    "href": "https://localhost:8000/hosts?limit=50"
  },
  "limit": 50,
  "total_count": 1,
  "volumes": [
    {
      "id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4800",
      "name": "vol1",
      "bandwidth": 300,
      "capacity": 10,
      "iops": 150,
      "created_at": "2024-06-21T07:22:15Z",
      "host_mappings": [
        {
          "host_id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921",
          "host_name": "host1",
          "host_nqn": "nqn.2014-08.cloud.appdomain.sdsaas:nvme:esx-dev-1-23"
        }
      ],
      "profile": {
        "name": "sds-general-purpose"
      },
      "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
      "storage_workspace_id": "default"
      "status": "available",
    }
  ]
}
```

### Viewing volume details with the API
{: #viewvol-details-api}

Make a `GET /volumes/{volume_id}` call to see details of a volume. See the following example.

```sh
curl -X GET "$sds_api_endpoint/v1/volumes/r134-04f0e415-3c70-43a8-a98d-a0160e50cc88 \
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

A successful response provides details of the volume, including capacity and IOPS, the volume status, and the host mapped to which the volume is mapped.

```json
    {
      "id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4800",
      "name": "vol1",
      "bandwidth": 300,
      "capacity": 10,
      "iops": 150,
      "created_at": "2024-06-21T07:22:15Z",
      "host_mappings": [
        {
          "host_id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921",
          "host_name": "host1",
          "host_nqn": "nqn.2014-08.cloud.appdomain.sdsaas:nvme:esx-dev-1-23"
        }
      ],
      "profile": {
        "name": "sds-general-purpose"
      },
      "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
      "storage_workspace_id": "default"
      "status": "available",
    }
```
{: codeblock}


## Next steps
{: #next-step-viewing-block-storage-volumes}

Create more volumes or manage your existing SDSaaS volumes.

* [Create a volume](/docs/sdsaas?topic=sdsaas-creating-sds-block-volume)

* [Manage volume](/docs/sdsaas?topic=sdsaas-managing-sds-block-volume)

* [Delete a volume](/docs/sdsaas?topic=sdsaas-deleting-sds-block-volume)
