---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-03"

keywords: cephaas, delete host, sds host-delete,

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

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

2. Locate the Host **Name** that you want to delete and then click the kebab menu at the end of the row to open a list of options.

3. From the options menu, click **Delete**.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}

## Deleting multiple hosts from the UI
{: #deleting-multiple-hosts-ui}
{: ui}

To delete multiple hosts together, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

2. Select one or more Host **Names** that you want to delete.

3. Click **Delete**.

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

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.{uuid}.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstd` as an alternative to `host-delete` for the CLI actions.
{: tip}


## Deleting a host with the API
{: #deleting-host-api}
{: api}

Make a `DELETE /hosts/{id}` request to delete a specific host.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}

```sh
curl -X DELETE '$sds_api_endpoint/v1/hosts/{id}' \
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

There is no response body for a successful delete operation. HTTP response code 204 is returned.

To verify that the host is deleted, list the hosts by making a `GET /hosts` call.


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
