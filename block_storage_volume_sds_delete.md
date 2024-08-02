---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-02"

keywords: sds, sdsaas Block Storage Volume, provision Block Storage Volume for sdsaas,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a block volume
{: #deleting-sds-block-volume}

Delete a volume from a service instance by using the UI, CLI, or API.
{: shortdesc}

When you delete a Block Storage volume, that data immediately becomes inaccessible.


## Deleting block volumes in the UI
{: #deleting-sds-block-volume-ui}
{: ui}

Deleting a Block Storage volume completely removes its data. The volume cannot be restored.

You cannot delete an active Block Storage volume. To delete a volume, first unmap it from the host.
{: note}

To delete a single volume, complete the following steps.

1. On the {{site.data.keyword.cloud_notm}} console, click the **hamburger menu** > **Resource list** and then expand **Storage**.

2. Click **Deployment name** link and go to **Block Storage > Volumes**.

3. Locate the volume that you want to delete and then click the **Options** menu at the end of the row to open a list of options.

3. From the options menu, click **Delete**.


## Deleting multiple block volumes in the UI
{: #deleting-sds-multiple-volumes-ui}
{: ui}

Deleting a Block Storage volume completely removes its data. The volume cannot be restored.

You cannot delete an active Block Storage volume. To delete a volume, first unmap it from the host.
{: note}

To delete multiple volumes together, complete the following steps.

1. On the {{site.data.keyword.cloud_notm}} console, click the **hamburger menu > Resource list** and then expand **Storage**.

2. Click **Deployment name** link and go to **Block Storage > Volumes**.

2. Select the volumes that you want to delete.

3. Click **Delete**.


## Deleting a block volume from the CLI
{: #deleting-sds-block-volume-cli}
{: cli}

Use the `volume-delete` command to delete a single volume. Specify the volume id with `--id ID`, deployment instance id `--instanceid INSTANCEID` and API endpoint url.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage volume-delete --instanceid INSTANCEID --id ID [--if-match IF-MATCH] --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage volume-delete --instanceid exampleString --id exampleString --if-match exampleString --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}

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
{: #next-step-deleting-block-storage-volume-sds}

You can continue creating more volumes or manage existing volumes.

* [Create a volume](/docs/sdsaas?topic=sdsaas-creating-sds-block-volume)

* [View volume details](/docs/sdsaas?topic=sdsaas-view-sds-volume)

* [Manage volume](/docs/sdsaas?topic=sdsaas-managing-sds-block-volume)
