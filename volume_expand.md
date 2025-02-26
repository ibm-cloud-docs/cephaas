---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-26"

keywords: sds, cephaas Block Storage Volume, increase volume size for cephaas, manage volume, expand volume size

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Increasing block volume capacity
{: #expand-block-volume}

You can manage your Block Storage volume capacity in the UI, from the CLI, using the API or the terraform.
{: shortdesc}

## Increasing block volume capacity in the UI
{: #expanding-block-volume-ui}
{: ui}

Use the console to expand the volume capacity. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), you can complete the following actions.


### Increasing block volume size from list view page
{: #expand-block-volume-size-from-list-view-page}
{: ui}

To increase the block volume-provisioned size from the list view page, complete the following steps.

1. In the **Volume** list view page, locate the volume and click the `options` icon at the end of the volume row to open a list of options.
3. Click **Expand volume**.
2. Enter a new **size**.

    You can increase the provisioned size. It cannot be reduced.
    {: note}

3. Click **Expand**.


### Increasing block volume size from details page
{: #expand-block-volume-size-from-details-page}
{: ui}

To increase the block volume-provisioned size from the Volume details page, complete the following steps.

1. In the **Volume** details page, you can click the `edit` icon next to the **Provisioned size** OR click **Actions** > **Expand volume**.
2. Enter a new **size**.

    You can increase the provisioned size. It cannot be reduced.
    {: note}

3. Click **Expand**.



## Increasing block volume capacity from CLI
{: #expanding-volume-capacity-cli}
{: cli}

Use the `volume-update` command and specify the deployment ID, volume ID, capacity (in gigabytes), and endpoint to update the capacity of a volume.

```sh
ibmcloud software-defined-storage volume-update --volume-id VOLUME-ID --capacity CAPACITY --url string
```
{: pre}

See the following example.

```bash

ibmcloud sds volume-update --volume-id r134-af4273d1-b1a2-4ba8-82aa-2285133e2682 --capacity 20 --url $sds_endpoint
...

Volume_ID     r134-af4273d1-b1a2-4ba8-82aa-2285133e2682
Volume_Name   example1
Status        available
Bandwidth     19
Capacity_GB   20
Created       2025-02-11T19:08:21.000Z
IOPS          150
Hosts         -
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `volu` as an alternative to `volume-update` for the CLI actions.
{: tip}


## Increasing volume with the API
{: #expanding-volume-capacity-api}
{: api}

Make a `PATCH /volumes/{id}` request to update or expand the volume size to increase the current capacity.

Specify the capacity parameter with the new value that you want to modify for the existing volume in the request to update the volume details.

PATCH operation to change more than one parameter value in the same command is not supported.
{: note}


```sh
curl -X PATCH "$sds_endpoint/volumes/r134-36c119c1-22fa-42cc-b33b-cfdd1591d89c"  \
    -H 'accept: application/json'   \
    -H "Authorization: Bearer $IAM_TOKEN"   \
    -H 'IBM-API-Version: 2025-02-01'    \
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
    "status": "updating",
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
