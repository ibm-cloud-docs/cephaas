---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-14"

keywords: sds, cephaas Block Storage Volume, provision Block Storage Volume for cephaas,

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a block volume
{: #deleting-block-volume}

Delete a volume from a service instance by using the UI, CLI, or API.
{: shortdesc}

When you delete a Block Storage volume, that data immediately becomes inaccessible.


## Deleting block volumes in the UI
{: #deleting-block-volume-ui}
{: ui}

Deleting a block storage volume completely removes its data. The volume cannot be restored.

You cannot delete an active Block Storage volume. To delete a volume, first unmap it from the host.
{: note}

To delete a single volume, follow these steps:

1. On the {{site.data.keyword.cloud_notm}} console, go to **{{site.data.keyword.cephaas_full_notm}} > Block storage > Volumes**.

2. Locate the volume that you want to delete and then click the kebab menu at the end of the row to open a list of options.

3. From the options menu, click **Delete**.


## Deleting multiple block volumes in the UI
{: #deleting-multiple-volumes-ui}
{: ui}

Deleting a Block Storage volume completely removes its data. The volume cannot be restored.

You cannot delete an active Block Storage volume. To delete a volume, first unmap it from the host.
{: note}

To delete multiple volumes together, follow these steps:

1. On the {{site.data.keyword.cloud_notm}} console, go to **{{site.data.keyword.cephaas_full_notm}} > Block storage > Volumes**.

2. Select the volumes that you want to delete.

3. Click **Delete**.


## Deleting a block volume from the CLI
{: #deleting-block-volume-cli}
{: cli}

Use the `volume-delete` command to delete a single volume. Specify the volume ID with `--id ID`, deployment instance id `--instanceid INSTANCEID` and API endpoint url.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage volume-delete --id ID --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage volume-delete \
    --id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}

You can also use the aliase `sds` an alternative to `software-defined-storage` for the CLI actions.
{: tip}

## Deleting a block volume with the API
{: #deleting-block-volume-api}
{: api}

Make a `DELETE /volumes/{volume_id}` request to delete a volume. This operation cannot be reversed. For this request to succeed, the volume must not be mapped to any hosts.

```sh
curl -X DELETE '$sds_api_endpoint/v1/volumes/{volume-id}' \
--header 'Authorization: Bearer $IAM_TOKEN'

```
{: pre}

There is no response body for a successful delete operation. HTTP response code 202 is returned.


To verify that the volume is deleted, list the volumes by making a `GET /volumes` call.

## Sanitizing your data before you delete a volume
{: #sanitizing-your-data-before-you-delete-a-volume}

When you delete a Block Storage volume, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the volume means your data can't be restored.



## Next steps
{: #next-step-deleting-block-storage-volume}

You can continue creating more volumes or manage existing volumes.
