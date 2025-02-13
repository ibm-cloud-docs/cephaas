---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-13"

keywords: sds, cephaas host, host nqn

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating a host
{: #creating-host}

Create a host by using the UI, CLI, API or Terraform.
{: shortdesc}


Before creating a host, you must configure the NVME-oF initiator. This is required for mapping volume to a host. See [Configuring NVMe-oF initiators](/docs/cephaas?topic=cephaas-about-volume-host-mappings#config-nvme-initiators). After configuring the NVME-oF initiator, make a note of the `host nqn`.
{: requirement}


## Creating host in the UI
{: #creating-host-ui}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create a host for a service instance.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to **Block storage > Hosts**.
2. Click **Create host**.
3. Enter a unique **Host name** and enter the host identifier **Host NQN**.

    Host name must be unique in the entire service instance. For example, if you create two hosts that are in the same service instance, and have the same name, an error "Host name already exists" is displayed.

4. Click **Next**.
5. [Optional] Select one or more volumes to map them to the host.
6. Click **Create**.


## Creating hosts from the CLI
{: #creating-hosts-from-cli}
{: cli}

To create hosts by using the command-line interface (CLI) from a host template object, run the following command.

```sh
ibmcloud software-defined-storage host-create --name NAME --nqn NQN [--volume-mappings VOLUME-MAPPINGS | @VOLUME-MAPPINGS-FILE] --url string
```
{: pre}

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hyphens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two hosts with the same name in the same deployment, an error `Host name already exists` is displayed.

See the following example.

```bash
ibmcloud software-defined-storage host-create \
  --nqn nqn.2014-06.org:9345 \
  --name my-host \
  --volume-mappings '[{"volume": {"id": "r134-af4273d1-b1a2-4ba8-82aa-2285133e2682"}}]' \
  --url $sds_endpoint
```
{: screen}

Maximum supported NQN length is 223 bytes.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstc` as an alternative to `host-create` for the CLI actions.
{: tip}


## Creating hosts with the API
{: #creating-host-with-api}
{: api}

You can create hosts by directly calling the Host REST APIs. For more information, see the [{{site.data.keyword.cephaas_full_notm}} API reference](/apidocs/block-storage){: external}.

Make a `POST /hosts` request to create a host. Specify a host `name`, `nqn`, and an optional `volume_id`.

Ensure that you have defined the variables for the IAM token and API endpoint. Also, ensure that you have the host `nqn` handy. The host `nqn` can be fetched from the NVMe initiator as described in [About volume host mappings](/docs/cephaas?topic=cephaas-about-volume-host-mappings).
{: requirement}


```sh
curl -X 'POST' '$sds_api_endpoint/v1/hosts' -H 'accept: application/json' -H 'Content-Type: application/json' -d '{
  "name": "host1",
  "nqn": "nqn.2014-08.cloud.appdomain.cephaas:nvme:esx-dev-1-23",
  "volumes": [
    {
      "volume_id": "r134-f02df74f-dcba-4a85-93cb-088d0ffc1ae5"
    }
  ]
}'
```
{: pre}

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hyphens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same deployment, an error `Host name already exists` is displayed.
{: tip}

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




## Next steps
{: #next-step-creating-hosts}

When you refresh the Hosts page, the new host appears at the beginning of the list of hosts.
{: ui}

* [Connect NVME-oF initiators](/docs/cephaas?topic=cephaas-connecting-nvme-initiators)

* Continue creating more host resources and then connect them to NVME-oF initiators.
