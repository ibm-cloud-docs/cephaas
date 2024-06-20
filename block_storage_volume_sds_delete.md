---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-20"

keywords: sds, sdsaas Block Storage Volume, provision Block Storage Volume for sdsaas,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a block volume
{: #deleting-sds-block-volume}

Delete a volume from a service instance by using the UI, CLI, or API.
{: shortdesc}

When you delete a Block Storage volume, that data immediately becomes inaccessible.


## Deleting SDSaaS block volumes in the UI
{: #deleting-sds-block-volume-ui}
{: ui}

Deleting a Block Storage volume completely removes its data. The volume cannot be restored.

You cannot delete an active Block Storage volume. To delete a volume, first unmap it from the host.

To delete a volume, complete the following steps.

1. On the IBM Cloud console, navigate to **SDS as a Service > Block Storage > Volumes**.

2. Locate the volume that you want to delete and then click the **Options** menu at the end of the row to open a list of options.

3. From the options menu, click **Delete**.

4. Confirm the deletion.


## Deleting a block volume from the CLI
{: #deleting-sds-block-volume-cli}
{: cli}

Use the `volume-delete` command and specify the `INSTANCEID` to delete a single volume based on the instance id.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage volume-delete --instanceid INSTANCEID --id ID [--if-match IF-MATCH]
```
{: pre}

See the following example.

```bash
$ ibmcloud software-defined-storage volume-delete --instanceid exampleString --id exampleString --if-match exampleString
```
{: screen}


## Deleting a block volume with the API
{: #deleting-block-volume-api}
{: api}

Make a `DELETE /volumes/{volume_id}` request to delete a volume. This operation cannot be reversed. For this request to succeed, the volume must not be attached to any hosts.

```sh
curl -X DELETE '$sds_api_endpoint \
--header 'Authorization: Bearer $IAM_TOKEN'

```
{: pre}

There is no response body for a successful delete operation. HTTP response code 204 is returned.


To verify that the volume is deleted, list the volumes by making a `GET /volumes` call.

## Sanitizing your data before you delete a volume
{: #sanitizing-your-data-before-you-delete-a-volume}

When you delete a Block Storage volume, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the volume means your data can't be restored.



## Next steps
{: #next-step-deleting-block-storage-volume-sds}

You can continue creating more volumes or manage existing volumes.

* [Create a volume](/docs/sdsaas?topic=sdsaas-creating-sds-block-volume)

* [View volume details](/docs/sdsaas?topic=sdsaas-viewing-block-storage)

* [Manage volume](/docs/sdsaas?topic=sdsaas-managing-sds-block-volume)
