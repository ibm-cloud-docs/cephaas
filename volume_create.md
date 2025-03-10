---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-10"

keywords: sds, cephaas Block Storage Volume, provision Block Storage Volume for cephaas,

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating block volumes
{: #creating-block-volume}

Create a block storage volume by using the UI, CLI, API or terraform.
{: shortdesc}


## Creating block volumes in the UI
{: #creating-block-volume-ui}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create a volume for a deployment.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), access your deployment and then go to **Block storage > Volumes**.
1. Click **Create volume**.
1. Select **Deployment** where the volume will be created.
1. Specify a unique, meaningful **Name** for your volume. The volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter. It must not begin with a hypen or a number nor end with a hyphen. You can later edit the name if you want.

    Volume names must be unique in the entire deployment. If you create two volumes that are in the same deployment, and have the same name, a <q>volume name duplicate</q> error is displayed.
    {: note}

1. Enter the **Storage size** for the volume in GBs. Volume sizes can be between 1 GB and 32 TBs.
1. Select one or more hosts to map. This is an optional step.

    1. If you choose to create a new host, then enter the new **Host name**, **Host NQN** and click **Create host**. The new Host is added to the beginning of the list. For guidance on how to find the `host nqn`, see [Configuring NVMe-oF initiators](/docs/cephaas?topic=cephaas-about-volume-host-mappings&interface=ui#config-nvme-initiators).
    1. Select the newly created **Host** from the list.

1. Click **Create**. Once the volume creation is successful, you will be redirectred to the volumes main page where you can see the status of the newly created volume under the volume table.

During the new volume creation, the volume is in `Pending` state. The status changes to `Available` or `Failed` based on the actual state of the volume.
{: note}

## Creating block volumes from the CLI
{: #creating-block-volume-cli}
{: cli}

To create volumes by using the command-line interface (CLI), run the following command.

```sh
ibmcloud software-defined-storage volume-create --capacity CAPACITY [--name NAME] --url string
```
{: pre}

Provide the `CAPACITY` of the volume, `NAME` of the volume and endpoint url.

The volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter. It must not begin with a hypen or a number nor end with a hyphen. If you create two volumes with the same name in the same deployment and region, a `volume name duplicate` error is displayed.

See the following example.

```bash
ibmcloud sds volume-create \
   --capacity 10 \
   --name my-volume \
   --url $sds_endpoint
...

Volume_ID     r134-279863d6-c37b-4601-b586-80f6dac215c2
Volume_Name   my-volume
Status        pending
Capacity_GB   10
Created       2025-02-27T10:21:05.000Z
Bandwidth     19
IOPS          150
Hosts         -

```
{: screen}

Capacity, indicated in gigabytes, can range from minimum 1 GB to the maximum allocated capacity for block storage.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

You can also use the alias `sds` as an alternative to `software-defined-storage` and `volc` as an alternative to `volume-create` for the CLI actions.
{: tip}

## Creating block volumes with the API
{: #creating-volume-api}
{: api}

You can create volumes by directly calling the Block storage REST API.

Define variables for the IAM token and API endpoint. For instructions, see [Setting up your API and CLI environment](/docs/cephaas?topic=cephaas-set-up-environment&interface=api).
{: requirement}


Make a `POST /volumes` request to create a new block volume. Specify capacity and volume name. Volume name is optional.

```sh
curl -X POST $sds_endpoint/volumes\
   -H "accept: application/json"\
   -H "Authorization: Bearer $IAM_TOKEN"\
   -H "IBM-API-Version: 2025-02-01"\
   --data '{
     "capacity": 10,
     "name": "sandbox-stability-pasta-stroller"
}'
```
{: pre}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


The volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter. It must not begin with a hypen or a number nor end with a hyphen. If you create two volumes with the same name in the same deployment and region, a `volume name duplicate` error is displayed.
{: tip}

A successful response looks like this:

```json
{
  "id": "r134-8cdec173-1bcb-4b85-ada9-a6374a4f5906",
  "name": "sandbox-stability-pasta-stroller",
  "capacity": 10,
  "iops": 150,
  "status": "pending",
  "created_at": "2025-02-27T10:18:01Z",
  "status_reasons": [],
  "bandwidth": 19,
  "resource_type": "volume",
  "href": "$sds_endpoint/volumes/r134-8cdec173-1bcb-4b85-ada9-a6374a4f5906"
}
```
{: screen}



## Creating block volumes using Terraform
{: #create-volume-tf}
{: terraform}


1. Create a volume instance by using the `ibm_sds_volume` resource argument in your `main.tf` file. The volume instance in the following example is named `sds_volume_instance` respectively.

   ```terraform
   resource "ibm_sds_volume" "sds_volume_instance" {
     hostnqnstring = "<hostNQN>"
     capacity = 10
     name = "demo-volume"
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
   # ibm_sds_volume.sds_volume_instance will be created
   + resource "ibm_sds_volume" "sds_volume_instance" {
         + bandwidth      = (known after apply)
         + capacity       = 10
         + created_at     = (known after apply)
         + hostnqnstring  = "nqn.2014-06.org:9345"
         + hosts          = (known after apply)
         + id             = (known after apply)
         + iops           = (known after apply)
         + name           = "demo-volume-2"
         + resource_type  = (known after apply)
         + sds_endpoint   = "https://c-01.private.us-south.link.satellite.cloud.ibm.com:33029/v1"
         + status         = (known after apply)
         + status_reasons = (known after apply)

      }
    ```
    {: screen}


For more information about the arguments and attributes, see [ibm_is_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/is_instance){: external}.


## Next steps
{: #next-step-creating-volume}

Refresh the Volumes page. The new volume appears at the beginning of the list of volumes. If the volume was created successfully, it shows status as `Available`.
{: ui}

You can continue creating more volumes, map volume to hosts or manage existing volumes.
