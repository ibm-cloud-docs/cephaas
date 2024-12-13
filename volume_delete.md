---

copyright:
 years: 2024, 2024
lastupdated: "2024-12-13"

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

Use the `volume-delete` command to delete a single volume. Specify the volume ID with `--volume-id VOLUME-ID` and API endpoint url.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage volume-delete --volume-id VOLUME-ID --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage volume-delete \
    --volume-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `vold` as an alternative to `volume-delete` for the CLI actions.
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

## Deleting a block volume using terraform
{: #deleting-block-volume-tf}
{: terraform}


1. Run `terraform state list` to show the list of all volumes.

    ```terraform
    terraform state list
    ```
    {: pre}

2. Run `terraform destroy -target <volume_name>` to delete a single volume that is no longer needed.

    See example.

    ```terraform
    terraform destroy -target ibm_sds_volume.sds_volume_instance_2
    ```
    {: pre}

3. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

    ```terraform
    terraform plan
    ```
    {: pre}

4. Run `terraform apply` to modify the resources that are defined in the plan.

    ```terraform
    terraform apply
    ```
    {: pre}

5. Respond to "Do you really want to destroy all resouces?" with "Yes" to continue deleting the volume. A confirmation messages is displayed when the delete operation completes.

    ```terraform
    ibm_sds_volume.sds_volume_instance_2: Destroying... [id=r134-4e3f26c6-e8bf-4213-a523-33f2244fa286]
    ibm_sds_volume.sds_volume_instance_2: Destruction complete after 1s

    Destroy complete! Resources: 1 destroyed.
    ```
    {: screen}


## Sanitizing your data before you delete a volume
{: #sanitizing-your-data-before-you-delete-a-volume}

When you delete a Block Storage volume, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the volume means your data can't be restored.



## Next steps
{: #next-step-deleting-block-storage-volume}

You can continue creating more volumes or manage existing volumes.
