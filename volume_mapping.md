---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-03"

keywords: sds, cephaas Block Storage Volume, update volume for cephaas, manage volume

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Mapping volume to a host
{: #mapping-volume-to-host}

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



## Mapping volume to a host from CLI
{: #mapping-volume-to-host-cli}
{: cli}

Use the `host-vol-update` command and specify the `HOST-ID`, `VOLUME-ID`, and `INSTANCEID` to create a volume mapping to the host ID.

Run the following command to map the volume to the host.

```sh
ibmcloud software-defined-storage host-vol-update --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud sds hstvidu --instanceid "abc123" --url "$sds_endpoint" --host-id "r134-0bb14043-73a1-47e0-b46c-a147fdacba25" --volume-id "r134-3bc5068a-2936-4f30-b277-968fad03da2d"
...

Created_At    2024-07-23T04:53:29Z
ID        r134-0bb14043-73a1-47e0-b46c-a147fdacba25
Name       host1
NQN        nqn.2014-08.org.nvmexpress:uuid:54821642-dc4b-47bd-9b54-02699cebac79
Volume_Mappings
         Status    pending
         Volume_ID   r134-3bc5068a-2936-4f30-b277-968fad03da2d
         Volume_Name  volume1
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}



## Next steps
{: #next-step-mapping-volume}

* You can continue creating more volumes or manage existing volumes.

* [Configure NVME-oF initiators](/docs/sdsaas?topic=sdsaas-connecting-from-nvme-of-initiators)
