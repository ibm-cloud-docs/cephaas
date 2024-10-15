---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-15"

keywords: cephaas, block storage, rename host

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Renaming hosts
{: #renaming-hosts}

You can update host name (rename) from the UI, CLI, or by using the API.
{: shortdesc}

## Renaming hosts from the UI
{: #renaming-host-name-ui}
{: ui}

You can use the console to update the host name.

To rename a host, follow these steps:

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), go to **{{site.data.keyword.cephaas_full_notm}} > Block storage > Hosts**.
2. Locate the Host **Name** and click the kebab menu at the end of the Host row to open a list of options.
3. From the options menu, click **Rename**.
4. Provide a new valid **Host name**. Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter and must be unique. If you create two hosts with the same name in the same service instance, a duplicate host name error is displayed.
5. Click **Rename**.


## Renaming a host from details page in the UI
{: #renaming-sds-hosts-from-details-page-ui}
{: ui}

1. In the **Host** details page, click the `pen` icon next to the host name to modify the host name.
2. Provide a new valid **Host name**. Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter and must be unique. If you create two hosts with the same name in the same service instance, a duplicate host name error is displayed.
3. Click **Rename**.



## Renaming hosts from the CLI
{: #renaming-hosts-cli}
{: cli}

To rename the host using CLI, use the `host-update` command to rename a specific host.

Run the following command to update the details of a specific host in a service instance.

```sh
ibmcloud software-defined-storage host-update --host-id HOST-ID --instanceid INSTANCEID [--host-patch HOST-PATCH] --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage host-update \
    --host-id exampleString \
    --instanceid exampleString \
    --name my-host
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` for the CLI actions.
{: tip}


## Renaming host with the API
{: #renaming-hosts-api}
{: api}

To update your host name with the API, you can make use of the `PATCH /hosts/{id}` request to modify the host details. Specify the values for the parameter that you want to modify in the request to update the details.

Make a `PATCH /hosts/{id}` request to update or rename a host.

```sh
{{curl -X PATCH '$sds_api_endpoint/v1/hosts/{host-name-1}' }}
{{--header 'Authorization: Bearer $IAM_TOKEN' }}
{{--header 'Content-Type: application/json' }}
--data '{
    "name": "sds-host-name-updated"
}'
```
{: pre}

A successful response looks like this:

```json
{
  "id": "r134-69d40d27-bb86-4f52-83f9-6d3acb8d74eb",
  "name": "sds-host-name-updated",
  "nqn": "nqn.2014-08.com.vmware:nvme:vm2-esx-host",
  "created_at": "2024-09-03T05:22:56Z",
  "service_instance_id": "9f158770-66a4-4746-a2aa-245a8e06f451",
  "storage_workspace_id": "default"
}

```
{: screen}
