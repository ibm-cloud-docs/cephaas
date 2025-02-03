---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-03"

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

    You can only increase the provisioned size and cannot reduce it.
    {: note}

3. Click **Expand**.


### Increasing block volume size from details page
{: #expand-block-volume-size-from-details-page}
{: ui}

To increase the block volume-provisioned size from the Volume details page, complete the following steps.

1. In the **Volume** details page, you can click the `edit` icon next to the **Provisioned size** OR click **Actions** > **Expand volume**.
2. Enter a new **size**.

    You can only increase the provisioned size and cannot reduce it.
    {: note}

3. Click **Expand**.



## Increasing block volume capacity from CLI
{: #expanding-volume-capacity-cli}
{: cli}

Use the `volume-update` command and specify the deployment ID, volume ID, capacity (in gigabytes), and enpoint to update the capacity of a volume.

```sh
ibmcloud software-defined-storage volume-update --volume-id VOLUME-ID --capacity CAPACITY --url string
```
{: pre}

See the following example.

```bash

ibmcloud sds volume-update --volume-id r134-7ef8c36e-5234-45c3-bbab-de08bd61855b --capacity 20 --url $sds_endpoint
...

ID            r134-7ef8c36e-5234-45c3-bbab-de08bd61855b
Name          new-demo3
Status        updating
Mapped_Host   -
Capacity_GB   20
Created       2024-06-21T21:08:51Z
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.{uuid}.software-defined-storage.appdomain.cloud:{port number}/v1`.
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `volu` as an alternative to `volume-update` for the CLI actions.
{: tip}


## Increasing volume with the API
{: #expanding-volume-capacity-api}
{: api}

Make a `PATCH /volumes/{volume_id}` request to update or expand the volume size to increase the current capacity.

Specify the capacity parameter with the new value that you want to modify for the existing volume in the request to update the volume details.

PATCH operation to change more than one parameter value in the same command is not supported.
{: note}


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


## Increasing block volume using Terraform
{: #expand-volume-tf}
{: terraform}

To expand the capacity of a volume, do the following steps:

1. Open your `main.tf` file and modify the `capacity` value in the `ibm_sds_volume` resource.

2. After editing and saving the file, run `terraform plan` and `terraform apply` to apply your changes.

You can modify only one parameter value at a time.
{: note}
