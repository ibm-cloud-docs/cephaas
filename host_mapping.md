---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-03"

keywords: cephaas, block Storage, volume, map volume to host, volume mapping, host mapping

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Mapping volume to a hosts
{: #mapping-vol-to-host}

You can map one or more volume to a host by using UI, CLI and APIs.

## Mapping volumes to a host from Volumes page in the UI
{: #mapping-volume-to-host-ui}
{: ui}

To map a volume to a host from Volumes page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), navigate to **Resource list > Storage > Deployment > Block Storage > Volumes**.
2. Locate the Volume **Name** and click the `options` icon at the end of the row to open a list of options.
3. From the options menu, click **Map to host**.
4. Select an existing **Host** from the list or you can **Create new host** to map to the volume.
    1. If you choose to create a new host, then enter the new **Host name**, **Host NQN** and click **Create host**. The new Host is added to the beginning of the list.
    1. Select the newly created **Host** from the list.
5. Click **Map**. When mapping completes successfully, the number of hosts that are mapped to the volume is displayed in the **Mapped Hosts** column.


## Mapping volumes to a host from Hosts page in the UI
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
    "id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921",
    "name": "host1",
    "nqn": "nqn.2014-08.cloud.appdomain.sdsaas:nvme:esx-dev-1-23",
    "created_at": "2024-06-21T07:22:15Z",
    "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
    "storage_workspace_id": "default",
    "volume_mappings": [
        {
            "volume_name": "vol1",
            "volume_id": "r134-f02df74f-dcba-4a85-93cb-088d0ffc1ae5",
            "status": "pending"
        }
    ]
}

```
{: screen}


## Next steps
{: #next-step-mapping-hosts}

* [Configure NVME-oF initiators](/docs/sdsaas?topic=sdsaas-connecting-from-nvme-of-initiators)

* You can continue with mapping and unmapping hosts.
