---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-26"

keywords: cephaas, block storage, rename host

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Renaming hosts
{: #renaming-hosts}

You can update host name (rename) from the UI, CLI, by using the API or Terraform.
{: shortdesc}

## Renaming hosts from the UI
{: #renaming-host-name-ui}
{: ui}

You can use the console to update the host name.

To rename a host, follow these steps:

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to **Block storage > Hosts**.
2. Locate the Host **Name** and click the kebab menu at the end of the Host row to open a list of options.
3. From the options menu, click **Rename host**.
4. Provide a new valid **Host name**. Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter and must be unique. If you create two hosts with the same name in the same deployment, a duplicate host name error is displayed.
5. Click **Rename**.


## Renaming a host from details page in the UI
{: #renaming-sds-hosts-from-details-page-ui}
{: ui}

1. In the **Host** details page, click the `pen` icon next to the host name to modify the host name.
2. Provide a new valid **Host name**. Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter and must be unique. If you create two hosts with the same name in the same deployment, a duplicate host name error is displayed.
3. Click **Rename host**.



## Renaming hosts from the CLI
{: #renaming-hosts-cli}
{: cli}

To rename the host from the CLI, use the `host-update` command to rename a specific host.

Run the following command to update the name of a specific host.

```sh
ibmcloud software-defined-storage host-update --host-id HOST-ID [--host-patch HOST-PATCH | @HOST-PATCH-FILE] --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage host-update \
  --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
  --name mytesthost
  --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstu` as an alternative to `host-update` for the CLI actions.
{: tip}


## Renaming host with the API
{: #renaming-hosts-api}
{: api}

To update your host name by using the API, you can use the `PATCH /hosts/{id}` request to modify the host details. Specify the values for the parameter that you want to modify in the request to update the details.

Make a `PATCH /hosts/{id}` request to update or rename a host.

```sh
curl -X PATCH '$sds_endpoint/hosts/{host-name-1}' \
  --header 'Authorization: Bearer $IAM_TOKEN' \
  --header 'Content-Type: application/json' \
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

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
