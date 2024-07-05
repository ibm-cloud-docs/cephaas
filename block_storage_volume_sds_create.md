---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-05"

keywords: sds, sdsaas Block Storage Volume, provision Block Storage Volume for sdsaas,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating block volumes
{: #creating-sds-block-volume}

Create a SDSaaS volume by using the UI, CLI, or API.
{: shortdesc}


## Creating block volumes in the UI
{: #creating-sds-block-volume-ui}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create a SDSaaS block storage volume for a service instance.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), navigate to **SDS as a Service > Block storage > Volumes**.
2. Click **Create volume**.
3. Select **Service instance** where the volume will be located.
4. Specify a unique, meaningful **Name** for your volume. The volume name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. You can later edit the name if you want.

Volume names must be unique in the entire service instance. For example, if you create two volumes that are in the same service instance, and have the same name, a "volume name duplicate" error is triggered.
{: note}

5. Enter **Storage size** for the volume in GBs. Volume sizes can be between 10 GB and 32 TBs.
6. Click **Create**. During the new volume creation, the volume is in `Pending` state. The status changes to `Available` or `Failed` based on the actual state of the volume.


## Creating block volumes from the CLI
{: #creating-sds-block-volume-cli}
{: cli}

You can create SDSaaS volumes by using the command-line interface (CLI).

### Before you begin
{: #before-creating-block-volume-cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the SDS CLI plug-in.


{: requirement}

Log in to the IBM Cloud.

```sh
ibmcloud login --sso -a cloud.ibm.com
```
{: pre}

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After successful authentication, you are prompted to choose your account. If you have access to multiple accounts, select the account that you want to log in as. Respond to any remaining prompts to finish logging in.
{: pre}

### Creating a volume from the CLI
{: #create-volume-cli}
{: help}
{: support}

Run the following command to create a SDSaaS volume. Provide a volume name, profile name, and the name of the availability zone in your region.



Valid volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter. Volume names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same account and region, a `volume name duplicate` error is triggered.
{: important}

```sh
ibmcloud software-defined-storage volume-create [--capacity CAPACITY] [--name NAME] [--sdsaas-instance-id SDSAAS-INSTANCE-ID] [--hostnqnstring HOSTNQNSTRING]
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage volume-create --capacity 40 --name my-volume --sdsaas-instance-id exampleString --hostnqnstring exampleString
Creating volume my-volume in service instance exampleString...

```
{: screen}

Capacity, indicated in gigabytes, can range from minimumm 10 GBs to the maximum allocated capacity for block storage. If not specified, the default capacity is 100 GBs.

The volume name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. Volume names must be unique across the entire infrastructure.
{: requirement}


## Creating block volumes with the API
{: #creating-volume-api}
{: api}

You can create SDSaaS volumes by directly calling the Block Volume REST APIs. For more information about the file shares SDS API, see the SDSaaS API reference.

### Before you begin
{: #block-volume-api-prereqs}

Define variables for the IAM token and API endpoint.


### Creating a volume as part of instance provisioning with the API
{: #creating-volume-api}

Make a `POST /volumes` request to create a volume, and define the volume by using the `name` parameter. Specify a volume name, capacity, and profile.

Valid volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter. Volume names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same deployment, a `volume name duplicate` error is triggered.
{: important}


```sh
curl -X POST '$sds_api_endpoint/v1/volumes' \
--header 'Authorization: Bearer $IAM_TOKEN' \
--header 'Content-Type: application/json' \
--data '

{     "capacity": 10,     "name": "sds-vol" }
'
```
{: pre}

A successful response looks like this:

```json
{
    "id": "r134-36c119c1-22fa-42cc-b33b-cfdd1591d89c",
    "name": "sds-vol",
    "capacity": 10,
    "iops": 3000,
    "status": "pending",
    "profile":

{         "name": "sds-general-purpose"     }
,
    "created_at": "2024-06-19T06:22:51Z",
    "status_reasons": [],
    "bandwidth": 393,
    "resource_type": "volume",
    "service_instance_id": "f538f202-2907-4061-8463-6a40dbe6b69f",
    "storage_workspace_id": "default",
    "host_mappings": []
}
```
{: screen}




## Next steps
{: #next-step-creating-volume-sds}

When you refresh the Volumes page, the new volume appears at the beginning of the list of volumes. If the volume was created successfully, it shows status as `Available`.
{: ui}

You can continue creating more volumes or manage existing volumes.


* [View volume details](/docs/sdsaas?topic=sdsaas-viewing-block-storage)

* [Manage volume](/docs/sdsaas?topic=sdsaas-managing-sds-block-volume)

* [Delete a volume](/docs/sdsaas?topic=sdsaas-deleting-sds-block-volume)
