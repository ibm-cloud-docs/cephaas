---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-28"

keywords: sds, host, view host details, host summary list

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# View host mapping details
{: #view-host-mapping-details}

View details of a single host mapping to a one or more volumes or view a list of all host mappings for the deployment.
{: shortdesc}

Before you begin, make sure that you have [set up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment).
{: requirement}


## View all mapped volumes to a host in the UI
{: #view-all-mapped-vols-host-ui}
{: ui}

To view all mapped hosts to a volume, in the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link > **Block Storage > Hosts** and click on the single host name link.

All mapped volumes are displayed for the chosen host on the Mapped volume section of Host details page. In the list, you can see the following information.

| Field               | Description |
|---------------------|-------------|
| Name                | Volume name.                                             |
| Mapped status       | Shows the status of the volume that is mapped to the host. |
| Storage identifier  | Storage identification number.                             |
| Gateway IP          | IP address.                                              |
| Namespace ID        | Namespace identification number.                         |
| Namespace UUID      | Universal unique identification number of the namespace. |
{: caption="Details of all mapped volumes to a host." caption-side="bottom"}

By default, 10 hosts are shown from the list of all hosts. Change this default by clicking the Page Control down arrow and increase the list to 25, 50 or 100 hosts. Use the Page Control arrows after the list to go to the following page or return to the current page.

The row actions menu on the Hosts list page provides you with options to manage the single host information.

Table describes the kebab menu options.

| Action             | Description |
|--------------------|-------------|
| Unmap             | Remove the mapping between the volume and host. |
{: caption="Row actions menu options for mapped volumes to a host." caption-side="bottom"}




## View a list of all volume mapping for a host from the CLI
{: #view-all-host-mappings-cli}
{: cli}

Run this command to view the list of all volume mappings for a host.

```sh
ibmcloud software-defined-storage host-mappings --host-id HOST-ID --url string
```
{: pre}


The following example shows all volumes mapped to a host in your deployment.

```sh
ibmcloud software-defined-storage host-mappings\
  --host-id r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66\
  --url $sds_endpoint
...

Mapped_volumes
                 Gateways
                                     IP_Address   xx.xx.x.xx
                                     Port         8009

                                     IP_Address   xx.xx.x.xx
                                     Port         8009

                                     IP_Address   xx.xx.x.xx
                                     Port         8009

                                     IP_Address   xx.xx.x.xx
                                     Port         8009

                 Namespace_ID        1
                 Namespace_UUID      89c7e458acdd59ce82b9d0d688289a50
                 Status              mapped
                 Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                 Volume_ID           r134-2ca809e8-3e63-44bc-916e-1eae49302aae
                 Volume_Mapping_ID   r134-152a73a9-dee8-4475-ad7c-fe73494140dd
                 Volume_Name         dividend-abet-getting-presume
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstms` as an alternative to `host-mappings` for the CLI actions.
{: tip}


## Viewing details of a single volume to a host mapping from the CLI
{: #view-single-host-mapping-detail-cli}
{: cli}

Run the following command to show volume mapping details for a specific `HOST-ID` and `VOLUME_MAPPING_ID`.

```sh
ibmcloud software-defined-storage host-mapping --host-id HOST-ID --volume-mapping-id VOLUME-MAPPING-ID --url string
```
{: pre}


The following example uses the host ID to show volume mapping details of the host requested.

```sh
ibmcloud sds host-mapping --url "$sds_endpoint" \
--host-id r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66 \
--volume-mapping-id r134-152a73a9-dee8-4475-ad7c-fe73494140dd
...

Volume_ID           r134-2ca809e8-3e63-44bc-916e-1eae49302aae
Volume_Name         dividend-abet-getting-presume
Volume_Mapping_ID   r134-152a73a9-dee8-4475-ad7c-fe73494140dd
Status              mapped
Host_ID             r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66
Host_Name           my-host
Host_NQN            nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122
Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
Namespace_ID        1
Namespace_UUID      89c7e458acdd59ce82b9d0d688289a50
Gateways
                    IP_Address   xx.xx.x.xx
                    Port         8009

                    IP_Address   xx.xx.x.xx
                    Port         8009

                    IP_Address   xx.xx.x.xx
                    Port         8009

                    IP_Address   xx.xx.x.xx
                    Port         8009

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstm` as an alternative to `host-mapping` for the CLI actions.
{: tip}

For more information about available command options, run `ibmcloud sds hosts --help`.


## View a list of all volume mappings for a host with the API
{: #view-all-host-mappings-api}
{: api}

Make a `GET /hosts/{id}/volume_mappings` request to list all volume mappings for a host.

See the following example.

```sh
curl -X GET $sds_endpoint/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings\
 -H "Authorization: $IAM_TOKEN"\
 -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response displays a list all the volume mapping for the host.

```sh
{
  "volume_mappings": [
    {
      "id": "r134-152a73a9-dee8-4475-ad7c-fe73494140dd",
      "status": "mapped",
      "href": "https://sds-cephaas.scp-1b45e7473f4d.appdomain.cloud/v1/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings/r134-152a73a9-dee8-4475-ad7c-fe73494140dd",
      "volume": {
        "name": "dividend-abet-getting-presume",
        "id": "r134-2ca809e8-3e63-44bc-916e-1eae49302aae"
      },
      "host": {
        "name": "my-host",
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
  ],
  "first": {
    "href": "https://sds-cephaas.scp-1b45e7473f4d.appdomain.cloud/v1/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings?limit=1000"
  },
  "limit": 1000,
  "total_count": 1
}
```
{: screen}


The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


## View details of a single volume mapping for a host with the API
{: #view-single-host-mapping-details-api}
{: api}

Make a `GET /hosts/{id}/volume_mappings/{volume_mapping_id}` request to see details of a single volume mapping for a host. See the following example.

```sh
curl -X GET '$sds_endpoint/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings/r134-152a73a9-dee8-4475-ad7c-fe73494140dd'\
 -H "Authorization: $IAM_TOKEN" \
 -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response provides details of the host, such as the `host ID`, `host name`, `nqn`, and also includes mapped volume details.

```sh
{
  "id": "r134-152a73a9-dee8-4475-ad7c-fe73494140dd",
  "status": "mapped",
  "href": "https://sds-cephaas.scp-1b45e7473f4d.appdomain.cloud/v1/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings/r134-152a73a9-dee8-4475-ad7c-fe73494140dd",
  "volume": {
    "name": "dividend-abet-getting-presume",
    "id": "r134-2ca809e8-3e63-44bc-916e-1eae49302aae"
  },
  "host": {
    "name": "my-host",
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
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
