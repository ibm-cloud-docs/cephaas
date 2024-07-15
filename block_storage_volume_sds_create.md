---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-15"

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
1. Click **Create volume**.
1. Select **Service instance** where the volume will be located.
1. Specify a unique, meaningful **Name** for your volume. The volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter and should not end with a hyphen. You can later edit the name if you want.

    Volume names must be unique in the entire service instance. For example, if you create two volumes that are in the same service instance, and have the same name, a "volume name duplicate" error is displayed.
    {: note}

1. Enter **Storage size** for the volume in GBs. Volume sizes can be between 10 GB and 32 TBs.
1. Click **Create**. During the new volume creation, the volume is in `Pending` state. The status changes to `Available` or `Failed` based on the actual state of the volume.


## Creating block volumes from the CLI
{: #creating-sds-block-volume-cli}
{: cli}

You can create SDSaaS volumes by using the command-line interface (CLI).

### Before you begin
{: #before-creating-block-volume-cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the SDS CLI plug-in.

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

Run the following command to create a SDSaaS volume. Provide the `CAPACITY` of the volume, `NAME` of the volume, and the `SDSAAS-INSTANCE-ID` where the volume will be created.

The volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter and should not end with a hyphen. For example, if you create two volumes with the same name in the same account and region, a `volume name duplicate` error is displayed.
{: requirement}

```sh
ibmcloud software-defined-storage volume-create [--capacity CAPACITY] [--name NAME] [--sdsaas-instance-id SDSAAS-INSTANCE-ID] [--hostnqnstring HOSTNQNSTRING]
```
{: pre}

See the following example.

```bash
ic sds volume-create --instanceid abc --capacity 10 --name example1 --url $rsos_api
...

ID             r134-d75e1aeb-4bcf-4d41-8926-517198d55448
Name           example1
Status         pending
Mapped_Host    -
Capacity_GB    10
Created        2024-07-09T06:24:49Z
Health_state   inapplicable
Active         false

```
{: screen}

Capacity, indicated in gigabytes, can range from minimumm 10 GBs to the maximum allocated capacity for block storage. If not specified, the default capacity is 100 GBs.



## Creating block volumes with the API
{: #creating-volume-api}
{: api}

You can create SDSaaS volumes by directly calling the Block Volume REST APIs.



### Before you begin
{: #block-volume-api-prereqs}

Define variables for the IAM token and API endpoint.


### Creating a new volume with the API
{: #creating-volume-api}

Make a `POST /volumes` request to create a new block volume. Specify an optional volume name and capacity.

The volume names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Volume names must begin with a lowercase letter and should not end with a hyphen. For example, if you create two volumes with the same name in the same account and region, a `volume name duplicate` error is displayed.
{: important}


```sh
curl -X POST '$sds_api_endpoint/v1/volumes' \
--header 'Authorization: Bearer $IAM_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
     "capacity": 10,
     "name": "sds-vol"
}'
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
    "profile":{
       "name": "sds-general-purpose"
     },
    "created_at": "2024-06-19T06:22:51Z",
    "bandwidth": 393,
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

* [Manage volume](/docs/sdsaas?topic=sdsaas-managing-sds-block-volume#managing-sds-block-volume-ui)

* [Delete a volume](/docs/sdsaas?topic=sdsaas-deleting-sds-block-volume)
