---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-11"

keywords: cephaas, delete host, sds host-delete, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting hosts
{: #deleting-hosts}

Delete a host from a deployment by using the UI, CLI, API, or Terraform.
{: shortdesc}


## Deleting host from the UI
{: #deleting-single-host-ui}
{: ui}

To delete a host, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link.

2. Click **Block Storage > Hosts**.

3. Locate the Host **Name** that you want to delete and then click the kebab menu at the end of the row to open a list of options.

4. From the options menu, click **Delete**.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}

## Deleting multiple hosts from the UI
{: #deleting-multiple-hosts-ui}
{: ui}

To delete multiple hosts together, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link.

2. Click **Block Storage > Hosts**.

3. Select one or more Host **Names** that you want to delete.

4. Click **Delete**.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}




## Deleting host from the CLI
{: #deleting-hosts-cli}
{: cli}

Use the `host-delete` command and specify the `INSTANCEID` and endpoint url along with the `HOST-ID` to delete the host based on the host ID.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}

Run the following command to delete a host.

```sh
ibmcloud software-defined-storage host-delete --host-id HOST-ID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-delete \
  --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
  --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstd` as an alternative to `host-delete` for the CLI actions.
{: tip}


## Deleting a host with the API
{: #deleting-host-api}
{: api}

Make a `DELETE /hosts/{id}` request to delete a specific host.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}

```sh
curl -X DELETE '$sds_endpoint/hosts/r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e'\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

There is no response body for a successful delete operation.

To verify that the host is deleted, list the hosts by making a `GET /hosts` request.


## Deleting a host by using terraform
{: #deleting-host-tf}
{: terraform}

To delete a host by using terraform, run `terraform destroy -target <host_name>` where _<host_name>_ is the name of the host in the resource `ibm_sds_host` that is no longer needed.

Example of <host_name> used in the below command is `ibm_sds_host.sds_host_instance`.

First, show the list of terraform resources
```terraform
terraform state list
```
{: pre}

Then, target a specific resource to destroy
```terraform
terraform destroy -target ibm_sds_volume.sds_host_instance
```
{: pre}

If a volume is mapped to a host, you must unmap the volume from host before deletion using the CLI.
{: note}





## Sanitizing your data before you delete a host
{: #sanitizing-your-data-before-you-delete-a-host}

When you delete a host, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the host means your data can't be restored.
