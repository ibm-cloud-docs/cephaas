---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-17"

keywords: ceph as a service, cephaas, block storage, rename host

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Renaming hosts
{: #renaming-hosts}

You can update host name (rename) from the UI, CLI, and by using the API. 
{: shortdesc}

## Renaming hosts from the UI
{: #renaming-host-name-ui}
{: ui}

You can use the console to update the host name.

To rename a host, follow these steps:

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link.

2. Click **Block Storage > Hosts**.
3. Locate the Host **Name** and click the kebab menu at the end of the Host row to open a list of options.
4. From the options menu, click **Rename host**.
5. Provide a new valid **Host name**. Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter and must be unique. If you create two hosts with the same name in the same deployment, a duplicate host name error is displayed.
6. Click **Rename**.


## Renaming a host from details page in the UI
{: #renaming-sds-hosts-from-details-page-ui}
{: ui}

1. In the **Host** details page, click the **pen** icon next to the host name to modify the host name.
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
  --host-id r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66 \
  --name host-rename\
  --url $sds_endpoint
...

Host_ID           r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66
Host_Name         host-rename
Host_NQN          nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122
Created_At        2025-02-28T10:05:30.000Z
Volume_Mappings
                  Status              mapped
                  Volume_ID           r134-2ca809e8-3e63-44bc-916e-1eae49302aae
                  Volume_Mapping_ID   r134-95b99022-3cf7-42be-9c18-5b6e3fa30bfa
                  Volume_Name         dividend-abet-getting-presume
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstu` as an alternative to `host-update` for the CLI actions.
{: tip}


## Renaming host with the API
{: #renaming-hosts-api}
{: api}

To rename your host name by using the API, you can use the `PATCH /hosts/{id}` request to modify the host details. Specify the values for the parameter that you want to modify in the request to update the details.

Make a `PATCH /hosts/{id}` request to rename a host.

```sh
curl -X PATCH $sds_endpoint/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66\
 -H "Authorization: $IAM_TOKEN" \
 -d '{"name":"host-renamed"}' \
 --header 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response looks like this:

```json
{
  "id": "r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66",
  "name": "host-renamed",
  "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122",
  "created_at": "2025-02-28T10:05:30Z",
  "href": "$sds_endpoint/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66",
  "volume_mappings": [
    {
      "id": "r134-95b99022-3cf7-42be-9c18-5b6e3fa30bfa",
      "status": "mapped",
      "href": "$sds_endpoint/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings/r134-95b99022-3cf7-42be-9c18-5b6e3fa30bfa",
      "volume": {
        "name": "dividend-abet-getting-presume",
        "id": "r134-2ca809e8-3e63-44bc-916e-1eae49302aae"
      },
      "host": {
        "name": "host-renamed",
        "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122",
        "id": "r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66"
      },
      "subsystem_nqn": "nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f",
      "namespace": {
        "id": 1,
        "uuid": "89c7e458acdd59ce82b9d0d688289a50"
      },
      "gateways": [
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        },
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        },
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        },
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        }
      ]
    }
  ]
}
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
