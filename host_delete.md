---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-15"

keywords: cephaas, delete host, sds host-delete,

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting hosts
{: #deleting-hosts}

Delete a host from a deployment by using the UI, CLI, or API.
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

## Deleting multiple host from the UI
{: #deleting-multiple-hosts-ui}
{: ui}

To delete a host, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

2. Select one or more Host **Name** that you want to delete.

3. Click **Delete**.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}




## Deleting host from the CLI
{: #deleting-hosts-cli}
{: cli}

Use the `host-delete` command and specify the `INSTANCEID` and endpoint url along with the `HOST-ID` to delete the host based on the host id.

A host cannot be deleted if it has one or more volumes that are mapped to it. Unmap all associated volumes first to delete the host.
{: note}

Run the following command to delete a host.

```sh
ibmcloud software-defined-storage host-delete --host-id HOST-ID --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
  ibmcloud software-defined-storage host-delete \
    --host-id exampleString \
    --instanceid exampleString \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` for the CLI actions.
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
