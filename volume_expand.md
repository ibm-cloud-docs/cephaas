---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-12"

keywords: sds, cephaas, block storage, volume, increase volume size for cephaas, manage volume, expand volume size, ceph as a service

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

1. In the **Volume** list view page, locate the volume and click the **options** icon at the end of the volume row to open a list of options.
3. Click **Expand volume**.
2. Enter a new **size**.

    You can increase the provisioned size. It cannot be reduced.
    {: note}

3. Click **Expand**.


### Increasing block volume size from details page
{: #expand-block-volume-size-from-details-page}
{: ui}

To increase the block volume-provisioned size from the Volume details page, complete the following steps.

1. In the **Volume** details page, you can click the **edit** icon next to the **Provisioned size** OR click **Actions** > **Expand volume**.
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

ibmcloud sds volume-update --volume-id r134-601e431b-22ab-47a1-b0c1-411049b432a0 --capacity 20 --url $sds_endpoint
...

Volume_ID     r134-601e431b-22ab-47a1-b0c1-411049b432a0
Volume_Name   grain-snooper-blank-gyration
Status        updating
Bandwidth     19
Capacity_GB   20
Created       2025-02-27T10:14:42.000Z
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
curl -X PATCH $sds_endpoint/volumes/r134-601e431b-22ab-47a1-b0c1-411049b432a0\
    -H 'accept: application/json'\
    -H "Authorization: Bearer $IAM_TOKEN"\
    -H 'IBM-API-Version: 2025-02-01'\
    --data '{
        "capacity": 100
    }'
```
{: pre}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

A successful response looks like this:

```json
{
  "id": "r134-601e431b-22ab-47a1-b0c1-411049b432a0",
  "name": "grain-snooper-blank-gyration",
  "capacity": 100,
  "iops": 300,
  "status": "updating",
  "created_at": "2025-02-27T10:14:42Z",
  "status_reasons": [],
  "bandwidth": 39,
  "resource_type": "volume",
  "href": "$sds_endpoint/volumes/r134-601e431b-22ab-47a1-b0c1-411049b432a0"
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
