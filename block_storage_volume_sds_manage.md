---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-24"

keywords: sds, sdsaas Block Storage Volume, update volume for sdsaas, manage volume

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing a block storage volume
{: #managing-sds-block-volume}

You can manage your Block Storage volume in the UI, from the CLI, or with the API. You can delete a volume from a service instance. You can rename a volume or modify the volume size.
{: shortdesc}

## Managing Block Storage volume in the UI
{: #managing-sds-block-volume-ui}
{: ui}

Use the console to manage the volumes. In the console, you can complete the following actions.

* Rename a Block Storage volume
* Map a volume to a host
* Expand volume to increase the capacity
* Delete a volume




### Renaming a volume in the UI
{: #renaming-sds-block-volume-ui}
{: ui}

To rename a volume, complete the following steps.

1. Navigate to the list fo all Block storage volumes.
2. Locate the volume and click the `options` icon at the end of the volume row to open a list of options.
3. From the options menu, click **Rename volume**.
4. Provide a valid volume name. Valid volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter. Volume names must be unique. For example, if you create two volumes with the same name in the same service instance, a volume name duplicate error is triggered.
5. Click **Rename** to confirm renaming of the volume.


### Renaming a volume from details page in the UI
{: #renaming-sds-volume-from-details-page-ui}
{: ui}







## Managing block volume from the CLI
{: #managing-sds-block-volume-cli}
{: cli}

To manage your Block storage volume, you can use the `volume-update` command to modify the volume details.

Using CLI, you can complete the following actions.

* Rename a Block Storage volume.
* Map a volume to a host.
* Expand volume to increase the current capacity.

Specify the information in volume patch option to modify the existing details of a volume and run the following command to update the volume details.

### Updating block volume from CLI
{: #updating-sds-volume-cli}
{: cli}

Use the `volume-update` command and specify the information in volume patch to modify the existing details of a volume.

Run the following command to update the volume details.


```sh
ibmcloud software-defined-storage volume-update --instanceid INSTANCEID --id ID [--volume-patch VOLUME-PATCH] [--if-match IF-MATCH]
```
{: pre}

See the following example.

```bash

ibmcloud software-defined-storage volume-update \
    --instanceid exampleString \
    --id exampleString \
    --if-match exampleString \
    --capacity 38 \
    --name exampleString

```
{: screen}



## Managing block volume with the API
{: #managing-sds-block-volume-api}
{: api}

To manage your block storage volume with the API, you can make use of the `PATCH /volumes/{volume_id}` request to modify the volume details.

With the API, you can complete the following actions.

* Rename a Block Storage volume.
* Expand volume to increase the current capacity.

You can perform only one action at a time within the command.
{: note}

Specify the values for the parameter that you want to modify for the existing volume in the request to update the volume details.

### Updating volume details with the API
{: #updating-block-volume-api}
{: api}

Make a `PATCH /volumes/{volume_id}` request to update a volume.

```sh
{{curl -X PATCH '$sds_api_endpoint/v1/volumes/r134-36c119c1-22fa-42cc-b33b-cfdd1591d89c' }}
{{--header 'Authorization: Bearer $IAM_TOKEN' }}
{{--header 'Content-Type: application/json' }}
--data '{
    "name": "sds-vol-updated"
}'
```
{: pre}

A successful response looks like this:

```json
{
    "id": "r134-36c119c1-22fa-42cc-b33b-cfdd1591d89c",
    "name": "sds-vol-updated",
    "capacity": 10,
    "iops": 3000,
    "status": "available",
    "profile": {
        "name": "sds-general-purpose"
    },
    "created_at": "2024-06-19T06:22:51Z",
    "status_reasons": [],
    "bandwidth": 393,
    "resource_type": "volume",
    "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
    "storage_workspace_id": "default",
    "host_mappings": []
}

```
{: screen}


## Next steps
{: #next-step-updating-volume-sds}

You can continue creating more volumes or manage existing volumes.
