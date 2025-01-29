---

copyright:
 years: 2024, 2025
lastupdated: "2025-01-29"

keywords: sds, cephaas Block Storage Volume, update volume for cephaas, manage volume

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Mapping volume to a host
{: #mapping-volume-to-host}

You can map one or more volume to a host by using UI, CLI, API and Terraform.

## Mapping volumes to a host from Volumes page in the UI
{: #mapping-volume-to-host-ui}
{: ui}

To map a volume to a host from Volumes page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to **Block Storage > Volumes**.
2. Locate the Volume **Name** and click the kebab menu at the end of the row to open a list of options.
3. From the options menu, click **Map to host**.
4. Select an existing **Host** from the list or you can **Create new host** to map to the volume.

    1. If you choose to create a new host, then enter the new **Host name**, **Host NQN** and click **Create host**. The new Host is added to the beginning of the list.

    1. Select the newly created **Host** from the list.

5. Click **Map**. When mapping completes successfully, the number of hosts that are mapped to the volume is displayed in the **Mapped Hosts** column.


## Mapping volume to a host from Volume details page in the UI
{: #map-vol-host-voldetails-ui}
{: ui}

1. In the Volume details page, go to **Mapped host** section and click **Map host +**.

1. Select an existing **Host** from the list or you can **Create new host** to map to the volume.

    1. If you choose to create a new host, then enter the new **Host name**, **Host NQN** and click **Create host**. The new Host is added to the beginning of the list.
    1. Select the newly created **Host** from the list.

5. Click **Map**. When mapping completes successfully, the new host and the storage identifier is displayed in the **Mapped Hosts** column.


## Mapping volume to a host from CLI
{: #mapping-volume-to-host-cli}
{: cli}

Use the `host-vol-update` command and specify the `HOST-ID`, `VOLUME-ID` and endpoint url to create a volume mapping to the host ID.

Run the following command to map the volume to the host.

```sh
ibmcloud software-defined-storage host-vol-update --host-id HOST-ID --volume-id VOLUME-ID --url string
```
{: pre}

See the following example.

```bash
ibmcloud sds hstvidu --url "$sds_endpoint" --host-id "r134-0bb14043-73a1-47e0-b46c-a147fdacba25" --volume-id "r134-3bc5068a-2936-4f30-b277-968fad03da2d"
...

Created_At    2024-07-23T04:53:29Z
ID        r134-0bb14043-73a1-47e0-b46c-a147fdacba25
Name       host1
NQN        nqn.2014-08.org.nvmexpress:uuid:54821642-dc4b-47bd-9b54-02699cebac79
Volumes
         Status    pending
         Volume_ID   r134-3bc5068a-2936-4f30-b277-968fad03da2d
         Volume_Name  volume1
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstvidu` as an alternative to `host-vol-update` for the CLI actions.
{: tip}


## Mapping volume to a host with the API
{: #mapping-vol-to-hosts-api}
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

You can map only one volume at a time by using API command.
{: note}


## Mapping block volume using Terraform
{: #mapping-volume-tf}
{: terraform}

To map a volume to a host, a host must already exist or be created. Edit or add the `ibm_sds_host` resource in the `main.tf` file and add the `volumes` block which will map a volume to a host

The following examples show how you can map the volume created in the `Creating block volumes` section, to a host.

```terraform
// Provision sds_host resource instance
resource "ibm_sds_host" "sds_host_instance" {

  name = "demo-host"
  nqn = "<hostNQN>"
  volumes {
    volume_id = ibm_sds_volume.sds_volume_instance.id
    volume_name = ibm_sds_volume.sds_volume_instance.name
  }
}
```
{: screen}

You can map mulitple volumes to a host at a time.
{: note}


## Next steps
{: #next-step-mapping-volume}

* [Configure NVME-oF initiators](/docs/cephaas?topic=cephaas-about-volume-host-mappings#config-nvme-initiators)

* You can continue creating more volumes or manage existing volumes.
