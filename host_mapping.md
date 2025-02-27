---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-27"

keywords: cephaas, block Storage, volume, map volume to host, volume mapping, host mapping

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Mapping volume to a host
{: #mapping-vol-to-host}

You can map one or more volumes to a host by using UI, CLI, API, and Terraform.

Make sure that there are one or more volumes available for mapping to a host.
{: requirement}

## Mapping volumes to a host from Volumes page in the UI
{: #mapping-volume-to-host-from-volume-ui}
{: ui}

To map a volume to a host from Volumes page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to **Block Storage > Volumes**.
2. Locate the Volume **Name** and click the kebab menu at the end of the row to open a list of options.
3. From the options menu, click **Map to host**.
4. Select an existing **Host** from the list or you can **Create new host** to map to the volume.
    1. If you choose to create a new host, then enter the new **Host name**, **Host NQN** and click **Create host**. The new Host is added to the beginning of the list.
    1. Select the newly created **Host** from the list.
5. Click **Map**. When mapping completes successfully, the number of hosts that are mapped to the volume is displayed in the **Mapped Hosts** column.


## Mapping volumes to a host from Hosts page in the UI
{: #mapping-volume-to-host-from-host-ui}
{: ui}

To map a volume to a host from Hosts page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to **Block storage > Hosts**.
2. Locate the host **Name** and click the kebab menu at the end of the row to open a list of options.
3. From the options menu, click **Map volumes**.
4. Select one or more volumes that you want to map to the host.

    Volumes in pending state and already mapped volumes are not listed in the table.
    {: note}

5. Click **Map**.



## Mapping volume to a host from CLI
{: #mapping-hosts-cli}
{: cli}

Use the `host-mapping-create` command and specify the `HOST-ID`, and the volume information, along with the endpoint url to create a volume mapping to the host ID.

Run the following command to map the volume to the host.

```sh
ibmcloud software-defined-storage host-mapping-create --host-id HOST-ID [--volume (VOLUME | @VOLUME-FILE) | --volume-id VOLUME-ID]
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-mapping-create \
    --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
    --volume '{"id": "r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39"}' \
    --url exampleString
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstmc` as an alternative to `host-mapping-create` for the CLI actions.
{: tip}


## Mapping volume to a host with the API
{: #mapping-hosts-api}
{: api}

Make a `PUT /hosts/{id}/volumes/{vol_id}` request to map the volume to a host.

```sh
curl -X PUT $sds_endpoint/hosts/{host-id}/volumes/{volume-id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

You can map only one volume at a time by using API command.
{: note}

A successful response looks like this:

```json
{
    "id": "r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921",
    "name": "host1",
    "nqn": "nqn.2014-08.cloud.appdomain.cephaas:nvme:esx-dev-1-23",
    "created_at": "2024-06-21T07:22:15Z",
    "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
    "storage_workspace_id": "default",
    "volumes": [
        {
            "volume_name": "vol1",
            "volume_id": "r134-f02df74f-dcba-4a85-93cb-088d0ffc1ae5",
            "status": "pending"
        }
    ]
}

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).



## Next steps
{: #next-step-mapping-hosts}

* [Configure NVME-oF initiators](/docs/cephaas?topic=cephaas-connecting-nvme-initiators)

* You can continue with mapping and unmapping hosts.
