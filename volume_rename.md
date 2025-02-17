---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-17"

keywords: sds, cephaas Block Storage Volume, update volume for cephaas, manage volume

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Renaming a block volume
{: #renaming-block-volume}

Renaming volumes help to improve organization, clarity, and accessibility, contributing to more efficient and effective management. You can rename a block storage volume in the UI, from the CLI, using the API or terraform.
{: shortdesc}

## Renaming block volume in the UI
{: #renaming-block-volume-ui}
{: ui}

To manage your Block storage volumes, you can use the {{site.data.keyword.cloud_notm}} console.

### Renaming a volume from list view page
{: #renaming-block-volume-from-list-view-page-ui}
{: ui}

To rename a volume, complete the following steps.

1. Go to the list of all Block storage volumes.
2. Locate the volume and click the `options` icon at the end of the volume row to open a list of options.
3. From the options menu, click **Rename volume**.
4. Provide a valid volume name. Valid volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. The names must begin with a lowercase letter and must be unique. For example, if you create two volumes with the same name in the same service instance, an error <q>volume name exists</q> is displayed.
5. Click **Rename**.




## Renaming block volume from the CLI
{: #renaming-block-volume-cli}
{: cli}

To manage your Block storage volumes, you can use the `volume-update` command to rename the volumes.

Specify the volume ID, and new name of the volume along with the endpoint when runing the following command for updating the name of a volume.

```sh
ibmcloud software-defined-storage volume-update --volume-id VOLUME-ID --name NAME --url string
```
{: pre}

See the following example.

```bash
ibmcloud sds volume-update --volume-id r134-af4273d1-b1a2-4ba8-82aa-2285133e2682 --name new-demo3 --url $sds_endpoint
...

Volume_ID     r134-af4273d1-b1a2-4ba8-82aa-2285133e2682
Volume_Name   example1
Status        available
Bandwidth     19
Capacity_GB   10
Created       2025-02-11T19:08:21.000Z
IOPS          150
Hosts         -
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}


You can also use the alias `sds` as an alternative to `software-defined-storage` and `volu` as an alternative to `volume-update` for the CLI actions.
{: tip}


## Renaming block volume with the API
{: #renaming-block-volume-api}
{: api}

Make a `PATCH /volumes/{volume_id}` request to update or rename a volume.


PATCH operation to change more than one parameter value in the same command is not supported.
{: note}



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
