---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-18"

keywords: sds, sdsaas Block Storage Volume, provision Block Storage Volume for sdsaas,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating SDS block volumes
{: #creating-sds-block-volume}

Create a SDSaaS volume by using the UI, CLI, or API.
{: shortdesc}


{: important}

## Creating SDSaaS block volumes in the UI
{: #creating-sds-block-volume-ui}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create a SDSaaS block storage volume for a service instance.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), navigate to **SDS as a Service > Block storage > Volumes**.
2. Click **Create volume**.
3. Select **Service instance** where the volume will be located.
4. Specify a unique, meaningful **Name** for your volume. The volume name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. You can later edit the name if you want.

    <br>
    **Note:** Volume names must be unique in the entire service instance. For example, if you create two volumes that are in the same service instance, and have the same name, a "volume name duplicate" error is triggered. </br>
5. Enter **Storage size** for the volume in GBs. Volume sizes can be between 10 GB and 32 TBs.
6. Click **Create**. During the new volume creation, the volume is in `Pending` state. The status changes to Available or Failed based on the actual state of the volume.


## Creating SDSaaS block volumes from the CLI
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

### Creating a SDSaaS volume from the CLI
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
$ ibmcloud software-defined-storage volume-create --capacity 40 --name my-volume --sdsaas-instance-id exampleString --hostnqnstring exampleString
Creating volume my-volume in service instance exampleString...

<Need example>

```
{: screen}

Capacity, indicated in megabytes, can range from 10 - 16,000 GBs. If not specified, the default capacity is 100 GBs. IOPS values can be 100 - 48,000 IOPS, depending on the profile and volume size. If not specified, the IOPS value defaults to the valid configuration per volume profile.

The volume name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. Volume names must be unique across the entire infrastructure.
{: requirement}


## Creating SDSaaS block volumes with the API
{: #creating-volume-api}
{: api}

You can create SDSaaS volumes by directly calling the [Block Volume REST APIs](/apidocs/sdsaas){: external}. For more information about the file shares SDS API, see the [SDSaaS API reference](/apidocs/sdsaas).

### Before you begin
{: #block-storage-api-prereqs}

Define variables for the IAM token, API endpoint, and API version.

### Creating a volume as part of instance provisioning with the API
{: #creating-volume-api}

Make a `POST /volumes` request to create a volume, and define the volume by using the `name` parameter. Specify a volume name, capacity, and profile.

Valid volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter. Volume names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same account and region, a `volume name duplicate` error is triggered.
{: important}


```sh
curl -X 'POST' \
  '$sds_api_endpoint' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "capacity": 0,
  "name": "string",
  "profile": {
    "name": "string"
  },
  "sdsaas_instance_id": "string"
}'

```
{: pre}

A successful response looks like this:

```json
{
    "bandwidth": 128,
    "capacity": 50,
    "created_at": "2019-03-28T23:16:53.000Z",

    "adjustable_iops_supported": false,
    "health_reasons": [],
    "health_state": "ok", // One of these values -[ degraded, faulted, inapplicable, ok ]
    "id": "2d1bb5a8-40a8-447a-acf7-0eadc8aeb054",
    "iops": 100,
    "name": "my-volume-4",
    "profile": {
        "name": "sdp-general-purpose"
    },
    "resource_type": "volume",
    "status": "available", // one of these value- [ available, failed, pending, pending_deletion, unusable, updating ]
    "status_reasons": [],

    "sdsaas_instance_id": "xxxx", // mandatory for SDSaaS.
    "storage_workspace_id": "yyyy" // not required for MVP.

}
```
{: screen}




## Next steps
{: #next-step-creating-volume-sds}

When you refresh the Volumes page, the new volume appears at the beginning of the list of volumes. If the volume was created successfully, it shows a status of Available.

You can continue creating more volumes or manage existing volumes.


