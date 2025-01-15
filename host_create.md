---

copyright:
 years: 2024, 2025
lastupdated: "2025-01-15"

keywords: sds, cephaas host,

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating a host
{: #creating-host}

Create a host by using the UI, CLI, API or Terraform.
{: shortdesc}

Before creating a host, the NVME-oF initiator, which is required for mapping volume to a host, must be configured.
{: requirement}


## Creating host in the UI
{: #creating-host-ui}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create a host for a service instance.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to **Block storage > Hosts**.
2. Click **Create host**.
3. Enter a unique **Host name** and enter the host identifier **Host NQN**.

    Host name must be unique in the entire service instance. For example, if you create two hosts that are in the same service instance, and have the same name, an error "Host name already exists" is displayed.
    {: note}

4. Click **Next**.
5. [Optional] Select one or more volumes to map them to the host.
6. Click **Create**.


## Creating hosts from the CLI
{: #creating-hosts-from-cli}
{: cli}

You can create hosts by using the command-line interface (CLI).

Run the following command to create a new host from a host template object.

```sh
ibmcloud software-defined-storage host-create --nqn NQN [--name NAME] [--volume-mappings VOLUME-MAPPINGS | @VOLUME-MAPPINGS-FILE] --url string
```
{: pre}

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hyphens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two hosts with the same name in the same deployment, an error `Host name already exists` is displayed.
{: important}


See the following example.

```bash
ibmcloud software-defined-storage host-create \
  --nqn nqn.2014-06.org:9345 \
  --name my-host \
  --volume-mappings '[{"volume_id": "1a6b7274-678d-4dfb-8981-c71dd9d4daa5"}]' \
  --url $sds_endpoint
```
{: screen}

Maximum supported NQN length is 223 bytes.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstc` as an alternative to `host-create` for the CLI actions.
{: tip}


## Creating hosts with the API
{: #creating-host-with-api}
{: api}

You can create hosts by directly calling the Host REST APIs. For more information about the Host {{site.data.keyword.cephaas_short}} API, see the [{{site.data.keyword.cephaas_full_notm}} API reference](/apidocs/block-storage){: external}.

### Before you begin
{: #host-api-prereqs}

Define variables for the IAM token and API endpoint.


### Creating a host with the API
{: #creating-host-api}

Make a `POST /hosts` request to create a host, and define the host by using the `name` parameter. Specify a host `name`, `nqn`, and an optional `volume_id`.

The `nqn` must be fetched from the NVMe initiator as described in [About volume host mappings](/docs/cephaas?topic=cephaas-about-volume-host-mappings).
{: note}

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hyphens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same deployment, an error `Host name already exists` is displayed.
{: important}


```sh
curl -X 'POST' '$sds_api_endpoint/v1/hosts' -H 'accept: application/json' -H 'Content-Type: application/json' -d '{
  "name": "host1",
  "nqn": "nqn.2014-08.cloud.appdomain.cephaas:nvme:esx-dev-1-23",
  "volume_mappings": [
    {
      "volume_id": "r134-f02df74f-dcba-4a85-93cb-088d0ffc1ae5"
    }
  ]
}'
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



## Creating hosts using Terraform
{: #create-host-tf}
{: terraform}


1. Create a host instance by using the `ibm_sds_host` resource argument in your `main.tf` file. The host instance in the following example is named `sds_host_instance` respectively.

   ```terraform
    resource "ibm_sds_host" "sds_host_instance" {
      name = "demo-host"
      nqn = "<hostNQN>"
      volume_mappings {
        volume_id = ibm_sds_volume.sds_volume_instance.id
        volume_name = ibm_sds_volume.sds_volume_instance.id
        }
    }
   ```
   {: codeblock}


2. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://www.terraform.io/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

3. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://www.terraform.io/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

4. Respond to "Do you want to perform these actions?" with "Yes" to proceed with creating the volume.

    See the example output for details.

    ```terraform
    ibm_sds_volume = [
    {
      "bandwidth" = 19
      "capacity" = 10
      "created_at" = "2024-12-11T13:44:36Z"
      "host_mappings" = tolist([])
      "hostnqnstring" = "nqn.2014-06.org:9345"
      "id" = "r134-51ad673d-ccdb-4b9c-b557-3ec6ff046879"
      "iops" = 150
      "name" = "demo-volume-1"
      "resource_type" = "volume"
      "status" = "available"
      "status_reasons" = tolist([])
      },
    ]
    ```
    {: screen}







## Next steps
{: #next-step-creating-hosts}

When you refresh the Hosts page, the new host appears at the beginning of the list of hosts.
{: ui}

* [Connect NVME-oF initiators](/docs/cephaas?topic=cephaas-connecting-nvme-initiators)

* Continue creating more host resources and then connect them to NVME-oF initiators.
