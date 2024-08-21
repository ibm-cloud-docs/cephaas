---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-21"

keywords: sds, sdsaas Block Storage Volume, update volume for sdsaas, manage volume

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Mapping volume to a hosts
{: #mapping-vol-to-host}


## Mapping volumes to a host in the UI
{: #mapping-volume-to-host-ui}
{: ui}

To map a volume to a host from Hosts page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), go to **{{site.data.keyword.cephaas_full_notm}} > Block storage > Hosts**.
2. Locate the host **Name** and click the `options` icon at the end of the row to open a list of options.
3. From the options menu, click **Map volumes**.
4. Select one or more volumes that you want to map to the host.

    Volumes in pending state and already mapped volumes will not be listed in the table.
    {: note}

5. Click **Map**.



## Mapping volume to a host from CLI
{: #mapping-hosts-cli}
{: cli}

Use the `host-vol-update` command and specify the `HOST-ID`, `VOLUME-ID` and `INSTANCEID` to create a volume mapping to the given host ID.

Run the following command to map the volume to the given host.

```sh
ibmcloud software-defined-storage host-vol-update --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-vol-update \
    --host-id exampleString \
    --volume-id exampleString \
    --instanceid exampleString
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}


## Mapping volume to a host with the API
{: #mapping-hosts-api}
{: api}

Make a `PUT /hosts/{id}/volumes/{vol_id}` request to map the volume to a given host.

```sh
curl -X PUT '$sds_api_endpoint/v1/hosts/{host-id}/volumes/{volume-id}'
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

A successful response looks like this:

```json
{
  "created_at": "string",
  "id": "string",
  "name": "string",
  "nqn": "string",
  "service_instance_id": "string",
  "storage_workspace_id": "string",
  "volume_mappings": [
    {
      "status": "string",
      "volume_id": "string",
      "volume_name": "string"
    }
  ]
}

```
{: screen}


## Next steps
{: #next-step-mapping-hosts}

* [Configure NVME-oF initiators](/docs/sdsaas?topic=sdsaas-connecting-from-nvme-of-initiators)

* You can continue with mapping and unmapping hosts.
