---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-18"

keywords: ceph as a service, cephaas, block Storage, volume, map volume to host, volume mapping, host mapping

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Create volume mapping for a host
{: #mapping-vol-to-host}

You can map one or more volumes to a host by using UI, CLI, API, and Terraform.

Make sure that there are one or more volumes available for mapping to a host.
{: requirement}

## Creating a volume mapping for a host from Volumes page in the UI
{: #mapping-volume-to-host-from-volume-ui}
{: ui}

To map a volume to a host from Volumes page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link.

2. Click **Block Storage > Volumes**.

3. Locate the Volume **Name** and click the kebab menu at the end of the row to open a list of options.
4. From the options menu, click **Map to host**.
5. Select an existing **Host** from the list or you can **Create new host** to map to the volume.
    1. If you choose to create a new host, then enter the new **Host name**, **Host NQN** and click **Create host**. The new Host is added to the beginning of the list.
    1. Select the newly created **Host** from the list.
6. Click **Map**. When mapping completes successfully, the number of hosts that are mapped to the volume is displayed in the **Mapped Hosts** column.


## Creating a volume mapping for a host from Hosts page in the UI
{: #mapping-volume-to-host-from-host-ui}
{: ui}

To map a volume to a host from Hosts page, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link.

2. Click **Block Storage > Hosts**.
3. Locate the host **Name** and click the kebab menu at the end of the row to open a list of options.
4. From the options menu, click **Map volumes**.
5. Select one or more volumes that you want to map to the host.

    Volumes in pending state and already mapped volumes are not listed in the table.
    {: note}

6. Click **Map**.



## Creating a volume mapping for a host from CLI
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
ibmcloud sds hstmc --url "$sds_endpoint"\
 --host-id r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66 \
 --volume-id r134-2ca809e8-3e63-44bc-916e-1eae49302aae
...

Volume_ID           r134-2ca809e8-3e63-44bc-916e-1eae49302aae
Volume_Name         dividend-abet-getting-presume
Volume_Mapping_ID   r134-152a73a9-dee8-4475-ad7c-fe73494140dd
Host
                    Host_ID     r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66
                    Host_NQN    nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122
                    Host_Name   my-host

Status              pending
Subsystem_NQN       -
Namespace_ID        -
Namespace_UUID      -
Gateways            -

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstmc` as an alternative to `host-mapping-create` for the CLI actions.
{: tip}


## Creating a volume mapping for a host with the API
{: #mapping-hosts-api}
{: api}

Make a `POST /hosts/{id}/volume_mappings` request to map the volume to a host.

```sh
curl -X POST $sds_endpoint/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings\
 -H "Authorization: $IAM_TOKEN"\
 -d '{"volume": {"id": "r134-2ca809e8-3e63-44bc-916e-1eae49302aae"}}'\
 -H "IBM-API-Version: 2025-02-01"
```
{: pre}

You can map only one volume at a time by using API command.
{: note}

A successful response looks like this:

```json
{
  "id": "r134-21d769dc-46ba-4d53-a1a0-8e598588d40c",
  "status": "pending",
  "href": "$sds_endpoint/hosts/r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66/volume_mappings/r134-21d769dc-46ba-4d53-a1a0-8e598588d40c",
  "volume": {
    "name": "dividend-abet-getting-presume",
    "id": "r134-2ca809e8-3e63-44bc-916e-1eae49302aae"
  },
  "host": {
    "name": "host-mapped-to-volume",
    "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122",
    "id": "r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66"
  }
}

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


## Mapping block volume by using Terraform
{: #mapping-host-to-volume-tf}
{: terraform}

To map one or more hosts to a volume, edit the `main.tf` file to add an `ibm_sds_volume_mapping` resource.

To map a host and a volume, a volume  and host must be created or already exist.

The following examples show how you can map a volume to a host using the `ibm_sds_volume_mapping` resource.

A `time_sleep` resource is also used because the `ibm_sds_volume_mapping` resource depends on the `ibm_sds_host` and `ibm_sds_volume` resources to be created first.

```terraform

resource "ibm_sds_volume" "sds_volume_instance" {
    capacity = 10
    name = "demo-volume"
}

// Provision sds_host resource instance
resource "ibm_sds_host" "sds_host_instance" {
    name = "demo-host"
    nqn = "<hostNQN>"
}

resource "ibm_sds_volume_mapping" "sds_vm" {

  depends_on = [time_sleep.wait_5_seconds]

  host_id = ibm_sds_host.sds_host_instance.id
  volume {
    id = ibm_sds_volume.sds_volume_instance.id
  }
}

// Use this sleep to allow the volume mappings to delete first before deleting the volumes and hosts
resource "time_sleep" "wait_5_seconds" {
  depends_on = [
    ibm_sds_volume.sds_volume_instance,
    ibm_sds_host.sds_host_instance
  ]
  destroy_duration = "5s"
}
```
{: screen}


To map multiple volumes to a host, create another volume, and then create another `ibm_sds_volume_mapping` resource

```terraform
resource "ibm_sds_volume" "sds_volume_instance_2" {
    capacity = 10
    name = "demo-volume-2"
}

resource "ibm_sds_volume_mapping" "sds_vm_2" {

  depends_on = [time_sleep.wait_5_seconds]

  host_id = ibm_sds_host.sds_host_instance.id
  volume {
    id = ibm_sds_volume.sds_volume_instance_2.id
  }
}

resource "time_sleep" "wait_5_seconds" {
  depends_on = [
    ibm_sds_volume.sds_volume_instance,
    ibm_sds_volume.sds_volume_instance_2,
    ibm_sds_host.sds_host_instance
  ]
  destroy_duration = "5s"
}
```
{: screen}


Using Terraform, you can map multiple volumes to a host at a time.
{: note}



## Next steps
{: #next-step-mapping-hosts}

* [Configure NVME-oF initiators](/docs/cephaas?topic=cephaas-connecting-nvme-initiators)

* You can continue with mapping and unmapping hosts.
