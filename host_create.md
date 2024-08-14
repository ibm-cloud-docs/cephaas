---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-14"

keywords: sds, sdsaas host,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating hosts
{: #creating-hosts-sds}

Create a host by using the UI, CLI, or API.
{: shortdesc}


## Creating host in the UI
{: #creating-host-sds-ui}
{: ui}

Use the {{site.data.keyword.cloud_notm}} console to create a host for a service instance.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), go to **{{site.data.keyword.cephaas_full_notm}} > Block storage > Hosts**.
2. Click **Create host**.
3. Enter a unique **Host name** and enter the host identifier **Host NQN**.

    Host name must be unique in the entire service instance. For example, if you create two hosts that are in the same service instance, and have the same name, an error "Host name already exists" is displayed.
    {: note}

4. Click **Next**.
5. [Optional] Select one or more volumes to map them to the host.
6. Click **Create**.


## Creating hosts from the CLI
{: #creating-sds-hosts-from-cli}
{: cli}

You can create hosts by using the command-line interface (CLI).

### Before you begin
{: #before-creating-hosts-sds-cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the SDS CLI plug-in.

Log in to the IBM Cloud.

```sh
ibmcloud login --sso -a cloud.ibm.com
```
{: pre}

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After successful authentication, you are prompted to choose your account. If you have access to multiple accounts, select the account that you want to log in as. Respond to any remaining prompts to finish logging in.


### Creating hosts from the CLI
{: #create-host-sds-cli}
{: help}
{: support}

Run the following command to create a new host from a host template object.

```sh
ibmcloud software-defined-storage host-create --instanceid INSTANCEID --nqn NQN [--name NAME] [--volume-mappings VOLUME-MAPPINGS] --url string
```
{: pre}

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hyphens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two hosts with the same name in the same deployment, an error `Host name already exists` is displayed.
{: important}


See the following example.

```bash
  ibmcloud software-defined-storage host-create \
    --instanceid abcd123 \
    --nqn nqn.2014-08.org.nvmexpress:uuid:0f2f1642-79d0-ae96-9888-abe29c991235 \
    --name my-host-1 \
    --volume-mappings '[{"volume_id": "r134-d75e1aeb-4bcf-4d41-8926-517198d55448"}]' \
    --url $sds_endpoint
```
{: screen}

Maximum supported NQN length is 223 bytes.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}


## Creating hosts with the API
{: #sds-creating-host-with-api}
{: api}

You can create hosts by directly calling the Host REST APIs. For more information about the Host {{site.data.keyword.cephaas_short}} API, see the [{{site.data.keyword.cephaas_full_notm}} API reference](/apidocs/sds-block-storage).

### Before you begin
{: #sds-host-api-prereqs}

Define variables for the IAM token and API endpoint.


### Creating a host with the API
{: #creating-sds-host-api}

Make a `POST /hosts` request to create a host, and define the host by using the `name` parameter. Specify a host `name`, `nqn`, and an optional `volume_id`.

The `nqn` must be fetched from the NVMe initiator as described in [About volume host mappings](/docs/sdsaas?topic=sdsaas-sds-about-volume-host-mappings)
{: note}

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hyphens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same deployment, an error `Host name alaready exists` is displayed.
{: important}


```sh
curl -X 'POST'   '$sds_api_endpoint/v1/hosts'   -H 'accept: application/json'   -H 'Content-Type: application/json'   -d '{
  "name": "host1",
  "nqn": "nqn.2014-08.cloud.appdomain.sdsaas:nvme:esx-dev-1-23",
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
    "nqn": "nqn.2014-08.cloud.appdomain.sdsaas:nvme:esx-dev-1-23",
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




## Next steps
{: #next-step-creating-hosts-sds}

When you refresh the Hosts page, the new host appears at the beginning of the list of hosts.
{: ui}

You can continue creating more hosts or manage existing hosts.


