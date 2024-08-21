---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-21"

keywords: sds, cephaas Block Storage Volume, update volume for cephaas, manage volume

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Updating a block volume
{: #updating-block-volume}

You can manage your Block Storage volume in the UI, from the CLI, or with the API. You can rename a volume or increase the volume size.
{: shortdesc}

## Updating block volume in the UI
{: #updating-block-volume-ui}
{: ui}

Use the console to update the volume details. In the console, you can complete the following actions.

* Rename a Block Storage volume
* Expand volume to increase the capacity


### Renaming a volume from list view page
{: #renaming-block-volume-from-list-view-page-ui}
{: ui}

To rename a volume, complete the following steps.

1. Navigate to the list of all Block storage volumes.
2. Locate the volume and click the `options` icon at the end of the volume row to open a list of options.
3. From the options menu, click **Rename volume**.
4. Provide a valid volume name. Valid volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. The names must begin with a lowercase letter and must be unique. For example, if you create two volumes with the same name in the same service instance, an error "volume name exists" is displayed.
5. Click **Rename**.



### Expanding block volume size from list view page
{: #expand-block-volume-size-from-list-view-page}
{: ui}

To increase the block volume-provisioned size from the list view page, complete the following steps.

1. In the **Volume** list view page, locate the volume and click the `options` icon at the end of the volume row to open a list of options.
3. Click **Expand volume**.
2. Enter a new **size**.

    You can only increase the provisioned size and cannot reduce it.
    {: note}

3. Click **Expand**.


### Expanding block volume size from details page
{: #expand-block-volume-size-from-details-page}
{: ui}

To increase the block volume-provisioned size from the Volume details page, complete the following steps.

1. In the **Volume** details page, you can click the `edit` icon next to the **Provisioned size** OR click **Actions** > **Expand volume**.
2. Enter a new **size**.

    You can only increase the provisioned size and cannot reduce it.
    {: note}

3. Click **Expand**.



## Updating block volume from the CLI
{: #updating-block-volume-cli}
{: cli}

To manage your Block storage volume, you can use the `volume-update` command to modify the volume details.

Using CLI, you can complete the following actions.

* Rename a volume.
* Map a volume to a host.
* Update capacity to increase the current volume capacity.

Specify the information to modify the existing details of a volume and run the following command to update the volume details.

### Renaming block volume from CLI
{: #renaming-volume-cli}
{: cli}

Use the `volume-update` command and specify the deployment ID, volume ID, and new name of the volume along with the endpoint to rename or update the volume name.

Run the following command for updating the name of a volume.

```sh
ibmcloud software-defined-storage volume-update --instanceid INSTANCEID --id ID --name NAME --url string
```
{: pre}

```bash
ibmcloud sds volume-update --instanceid abc --id r134-7ef8c36e-5234-45c3-bbab-de08bd61855b --name new-demo3 --url $sds_endpoint
...

ID            r134-7ef8c36e-5234-45c3-bbab-de08bd61855b
Name          new-demo3
Status        available
Mapped_Host   -
Capacity_GB   15
Created       2024-06-21T21:08:51Z
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}




### Updating block volume capacity from CLI
{: #updating-volume-capacity-cli}
{: cli}

Use the `volume-update` command and specify the deployment ID, volume ID, capacity, and enpoint to update the capacity of a volume.

```sh
ibmcloud software-defined-storage volume-update --instanceid INSTANCEID --id ID --capacity CAPACITY --url string
```
{: pre}

See the following example for updating the capacity of a volume.

```bash

ibmcloud sds volume-update --instanceid abc --id r134-7ef8c36e-5234-45c3-bbab-de08bd61855b --capacity 20 --url $sds_endpoint
...

ID            r134-7ef8c36e-5234-45c3-bbab-de08bd61855b
Name          new-demo3
Status        updating
Mapped_Host   -
Capacity_GB   20
Created       2024-06-21T21:08:51Z
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}


## Updating block volume with the API
{: #updating-block-volume-api}
{: api}

To update your block storage volume with the API, you can use the `PATCH /volumes/{volume_id}` request to modify the volume details. Specify the values for the parameter that you want to modify for the existing volume in the request to update the volume details.

With the API, you can complete the following actions.

* Rename a volume.
* Expand volume to increase the current capacity.

PATCH operation to change more than one parameter value in the same command is not supported.
{: note}



### Renaming volume with the API
{: #renaming-volume-api}
{: api}

Make a `PATCH /volumes/{volume_id}` request to update or rename a volume.

```sh
curl -X PATCH '<endpoint_URL>/v1/volumes/r134-36c119c1-22fa-42cc-b33b-cfdd1591d89c' \
--header 'Authorization: Bearer $IAM_TOKEN' \
--header 'Content-Type: application/json' \
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
    "iops": 150,
    "status": "available",
    "profile": {
        "name": "sds-general-purpose"
    },
    "created_at": "2024-06-19T06:22:51Z",
    "status_reasons": [],
    "bandwidth": 19,
    "resource_type": "volume",
    "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
    "storage_workspace_id": "default",
    "host_mappings": []
}

```
{: screen}

### Updating volume with the API
{: #updating-volume-capacity-api}
{: api}

Make a `PATCH /volumes/{volume_id}` request to update or expand the volume to increase the current capacity.

```sh
curl -X PATCH '<endpoint_URL>/v1/volumes/r134-36c119c1-22fa-42cc-b33b-cfdd1591d89c' \
--header 'Authorization: Bearer $IAM_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
    "capacity": 100
}'
```
{: pre}

A successful response looks like this:

```json
{
    "id": "r134-36c119c1-22fa-42cc-b33b-cfdd1591d89c",
    "name": "sds-vol-updated",
    "capacity": 100,
    "iops": 150,
    "status": "available",
    "profile": {
        "name": "sds-general-purpose"
    },
    "created_at": "2024-06-19T06:22:51Z",
    "status_reasons": [],
    "bandwidth": 19,
    "resource_type": "volume",
    "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
    "storage_workspace_id": "default",
    "host_mappings": []
}

```
{: screen}



## Next steps
{: #next-step-updating-volume}

You can continue creating more volumes or manage existing volumes.
