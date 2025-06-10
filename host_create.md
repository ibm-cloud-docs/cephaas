---

copyright:
 years: 2024, 2025
lastupdated: "2025-06-10"

keywords: sds, cephaas, creating host, host nqn, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating a host
{: #creating-host}

Create a host by using the UI, CLI, API, or Terraform.
{: shortdesc}


Before creating a host, you must configure the NVME-oF initiator. This NVME-oF initiator is required for mapping volume to a host. See [Configuring NVMe-oF initiators](/docs/cephaas?topic=cephaas-about-volume-host-mappings#config-nvme-initiators). After configuring the NVME-oF initiator, make a note of the `host nqn`.
{: requirement}

## Creating host in the UI
{: #creating-host-ui}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create a host for a deployment.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link.
1. Click **Block Storage > Hosts**.
1. Click **Create host**.
1. Enter a unique **Host name** and enter the host identifier **Host NQN**.

    Host name must be unique in the entire deployment. For example, if you create two hosts that are in the same deployment, and have the same name, an error "Host name already exists" is displayed.


1. Click **Next**.
1. Select one or more volumes to map them to the host.
1. Click **Create**. The Host page refreshes and the new host appears at the beginning of the list of hosts.



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
ibmcloud software-defined-storage host-create --url "$sds_endpoint"\
 --nqn "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122"\
 --name "dummy-host"\
 --volume-mappings  '[{"volume": {"id": "r134-2ca809e8-3e63-44bc-916e-1eae49302aae"}}]'
...

Host_ID           r134-0dcd5d2d-07db-4457-ab0b-1fc3eef28c66
Host_Name         dummy-host
Host_NQN          nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002122
Created_At        2025-02-28T10:05:30.000Z
Volume_Mappings
                  Namespace_ID        -
                  Namespace_UUID      -
                  Status              pending
                  Subsystem_NQN       -
                  Volume_ID           r134-2ca809e8-3e63-44bc-916e-1eae49302aae
                  Volume_Mapping_ID   r134-95b99022-3cf7-42be-9c18-5b6e3fa30bfa
                  Volume_Name         dividend-abet-getting-presume

```
{: screen}

The maximum supported NQN length is 223 bytes.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstc` as an alternative to `host-create` for the CLI actions.
{: tip}


## Creating hosts with the API
{: #creating-host-with-api}
{: api}

You can create hosts by directly calling the Host REST APIs. For more information, see the [{{site.data.keyword.cephaas_full_notm}} API reference](/apidocs/block-storage){: external}.

Ensure that you have defined the variables for the IAM token and API endpoint. Also, ensure that you have the host `nqn` handy. The host `nqn` can be fetched from the NVMe initiator as described in [About volume host mappings](/docs/cephaas?topic=cephaas-about-volume-host-mappings).
{: requirement}

Make a `POST /hosts` request to create a host. Specify a host `name`, `nqn`, and an optional `volume_id`.

```sh
curl -X POST $sds_endpoint/hosts\
 -H "Authorization: $IAM_TOKEN" \
 -H "IBM-API-Version: 2025-02-01" \
 -d '{
 		"volume_mappings": [
 			{
 				"volume": {
 					"id": "r134-b05d91af-6393-4652-aada-13fd4fdbd065"
 					}
 			},
 			{
 				"volume": {
 					"id": "r134-601e431b-22ab-47a1-b0c1-411049b432a0"
 					}
 			}
 		],
 	"name": "host1",
  "psk": "NVMeTLSkey-1:01:5CBxDU8ejK+PrqIjTau0yDHnBV2CdfvP6hGmqnPdKhJ9tfi2:",
 	"nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002149"}'
```
{: pre}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hyphens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two hosts with the same name in the same deployment, an error `Host name already exists` is displayed.
{: tip}

A successful response looks like this:

```json
{
  "id": "r134-63b6133f-cb3b-4d0b-a5e8-90821a40d64d",
  "name": "host1",
  "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002149",
  "created_at": "2025-02-27T10:55:07Z",
  "href": "$sds_endpoint/hosts/r134-63b6133f-cb3b-4d0b-a5e8-90821a40d64d",
  "volume_mappings": [
    {
      "id": "r134-dfb2c915-4788-4cb3-b1d5-8e00ee09e780",
      "status": "pending",
      "href": "$sds_endpoint/hosts/r134-63b6133f-cb3b-4d0b-a5e8-90821a40d64d/volume_mappings/r134-dfb2c915-4788-4cb3-b1d5-8e00ee09e780",
      "volume": {
        "name": "seventy-banked-pry-punt",
        "id": "r134-b05d91af-6393-4652-aada-13fd4fdbd065"
      },
      "host": {
        "name": "host1",
        "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002149",
        "id": "r134-63b6133f-cb3b-4d0b-a5e8-90821a40d64d"
      }
    },
    {
      "id": "r134-b557c11f-6c90-48e5-93b3-deac047e815c",
      "status": "pending",
      "href": "$sds_endpoint/hosts/r134-63b6133f-cb3b-4d0b-a5e8-90821a40d64d/volume_mappings/r134-b557c11f-6c90-48e5-93b3-deac047e815c",
      "volume": {
        "name": "new-vol",
        "id": "r134-601e431b-22ab-47a1-b0c1-411049b432a0"
      },
      "host": {
        "name": "host1",
        "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002149",
        "id": "r134-63b6133f-cb3b-4d0b-a5e8-90821a40d64d"
        "psk_enabled": true
      }
    }
  ]
}

```
{: screen}


## Creating hosts using Terraform
{: #create-host-tf}
{: terraform}

To create host using Terraform, you must have the `host nqn` handy. For guidance on how to find the `host nqn`, see [Configuring NVMe-oF initiators](/docs/cephaas?topic=cephaas-about-volume-host-mappings&interface=ui#config-nvme-initiators).

1. Create a host instance in your `main.tf` file by using the `ibm_sds_host` resource argument. The host instance in the following example is named `sds_host_instance` respectively.

   ```terraform
    resource "ibm_sds_host" "sds_host_instance" {
      name = "demo-host"
      nqn = "<hostNQN>"
    }
   ```
   {: codeblock}


2. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

3. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```sh
      terraform apply
      ```
      {: pre}

4. Respond to "Do you want to perform these actions?" with "Yes" to proceed with creating the volume.

    See the example output for details.

    ```terraform
    ibm_sds_host.sds_host_instance: Creating...
    ibm_sds_host.sds_host_instance: Creation complete after 1s [id=r134-e8b82dc5-e081-422e-9709-a44ec63f56af]

    Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

    Outputs:

    ibm_sds_host = {
      "created_at" = "2025-03-10T14:58:33.000Z"
      "href" = "$sds_endpoint/hosts/r134-e8b82dc5-e081-422e-9709-a44ec63f56af"
      "id" = "r134-e8b82dc5-e081-422e-9709-a44ec63f56af"
      "name" = "demo-host"
      "nqn" = "nqn.2014-06.org:9345"
      "sds_endpoint" = tostring(null)
      "volume_mappings" = tolist([])
    }
    ```
    {: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`.

## Next steps
{: #next-step-creating-hosts}


* [Connect NVME-oF initiators](/docs/cephaas?topic=cephaas-connecting-nvme-initiators)

* Continue creating more host resources and then connect them to NVME-oF initiators.
