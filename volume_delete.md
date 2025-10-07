---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-07"

keywords: sds, cephaas, block storage, volume, delete Block Storage Volume for cephaas, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a block volume
{: #deleting-block-volume}

Delete a volume from a service instance by using the UI, CLI, API or Terraform.
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

You can choose a maximum of 10 volumes only for deletion at one time.
{: note}

## Deleting a block volume from the CLI
{: #deleting-block-volume-cli}
{: cli}

Use the `volume-delete` command to delete a single volume. Specify the volume ID with `--volume-id VOLUME-ID` and API endpoint url.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage volume-delete --volume-id VOLUME-ID --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage volume-delete --volume-id r134-af4273d1-b1a2-4ba8-82aa-2285133e2682
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `vold` as an alternative to `volume-delete` for the CLI actions.
{: tip}

## Deleting a block volume with the API
{: #deleting-block-volume-api}
{: api}

Make a `DELETE /volumes/{volume_id}` request to delete a volume. This operation cannot be reversed. For this request to succeed, the volume must not be mapped to any hosts.

```sh
curl -X DELETE $sds_endpoint/volumes/${id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

There is no response body for a successful delete operation.


To verify that the volume is deleted, list the volumes by making a `GET /volumes` request.


## Deleting a block volume using Terraform
{: #deleting-block-volume-tf}
{: terraform}

To delete a resource using Terraform, you can run `terraform destroy -target <resource_type>.<resource_name>` where _<resource_name>_ is the name of the resource that is no longer needed.

Example of _<resource_type>.<resource_name>_: `ibm_sds_volume.sds_volume_instance`.

First, show the list of Terraform resources
```terraform
terraform state list
```
{: pre}

Then, target a specific resource to destroy
```terraform
terraform destroy -target ibm_sds_volume.sds_volume_instance
```
{: pre}

If a volume is mapped to a host, you must unmap the volume from host before deletion using the CLI.
{: note}



## Sanitizing your data before you delete a volume
{: #sanitizing-your-data-before-you-delete-a-volume}

When you delete a Block Storage volume, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the volume means your data can't be restored.



## Next steps
{: #next-step-deleting-block-storage-volume}

You can continue creating more volumes or manage existing volumes.
