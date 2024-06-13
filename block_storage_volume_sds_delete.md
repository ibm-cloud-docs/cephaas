---

copyright:
  years: 2024
lastupdated: "2024-06-07"

keywords: sds, sdsaas Block Storage Volume, provision Block Storage Volume for sdsaas,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a block volume
{: #deleting-sds-block-volume}

Delete a volume from a service instance by using the UI, CLI, or API.
{: shortdesc}

When you delete a Block Storage volume, that data immediately becomes inaccessible. All pointers to the data on the physical disk are removed. If you later create a volume in the same or another account, a new set of pointers is assigned. The account can't access any data that was on the physical storage because those pointers are deleted. When new data is written to the disk, any inaccessible data from the deleted volume is overwritten.

IBM guarantees that data deleted cannot be accessed and that deleted data is eventually overwritten and eradicated. Further, when you delete a Block Storage volume, those blocks must be overwritten before that Block Storage volume is made available again, either to you or to another customer.

Further, when IBM decommissions a physical drive, the drive is destroyed before disposal. Decommissioned drives are unusable and any data on them is inaccessible.


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
{: #creating-sds-block-volume-cli}
{: cli}

Use the `volume-delete` command and specify the volume ID to delete a Block Storage volume.

Run the following command to delete a volume.

```sh
ibmcloud sds volume-delete --id ID [--instanceid INSTANCEID] [--if-match IF-MATCH]
```
{: pre}

See the following example.

```bash
$ ibmcloud sds volume-delete --id demovolume1
This will delete volume demovolume1 and cannot be undone. Continue [y/N] ?> y
Deleting volume demovolume1 ...
OK
Volume demovolume1 is deleted.
```
{: screen}


## Deleting a block volume with the API
{: #deleting-block-volume-api}
{: api}

Make a `DELETE /volumes/{volume_id}` request to delete a volume. This operation cannot be reversed. For this request to succeed, the volume must not be attached to any instances.

```sh
curl -X DELETE "$sds_api_endpoint/v1/volumes/$volume_id" -H "Authorization: $iam_token"

```
{: pre}

A successful response looks like this:

```json

This method does not specify any sample responses.

```
{: screen}

To verify that the volume is deleted, list the volumes by making a `GET /volumes` call.

## Sanitizing your data before you delete a volume
{: #sanitizing-your-data-before-you-delete-a-volume}

When you delete a Block Storage volume, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the volume means your data can't be restored.



## Next steps
{: #next-step-deleting-block-storage-volume-sds}

When you refresh the Volumes page, the new volume appears at the beginning of the list of volumes. If the volume was created successfully, it shows a status of Available.

You can continue creating more volumes or manage existing volumes.


