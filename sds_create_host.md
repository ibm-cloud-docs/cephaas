---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-08"

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

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/sds), navigate to **SDS as a Service > Block storage > Hosts**.
2. Click **Create host**.
3. Enter a unique **Host name** and enter the host identifier **Host NQN**.

    Host name must be unique in the entire service instance. For example, if you create two hosts that are in the same service instance, and have the same name, a "Duplicate host name" error is displayed.
    {: note}

4. Select one or more volumes to map them to the host.
5. Click **Create**.


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
{: pre}

### Creating hosts from the CLI
{: #create-host-sds-cli}
{: help}
{: support}

Run the following command to create a new host from a host template object. Provide a unique host name and the name of the availability zone in your region.

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hypens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same deployment, a `Duplicae host name` error is displayed.
{: important}

```sh
ibmcloud software-defined-storage host-create --instanceid INSTANCEID --nqn NQN [--name NAME] [--volume-mappings VOLUME-MAPPINGS]
```
{: pre}

See the following example.

```bash
  ibmcloud software-defined-storage host-create \
    --instanceid exampleString \
    --nqn nqn.abc.1234 \
    --name my-host \
    --volume-mappings '[{"volume_id": "exampleString"}]'

```
{: screen}


## Creating host with the API
{: #creating-sds-host-api}
{: api}

You can create hosts by directly calling the Volume REST APIs. For more information about the file shares SDS API, see the SDSaaS API reference.

### Before you begin
{: #sds-host-api-prereqs}

Define variables for the IAM token and API endpoint.


### Creating a host as part of instance provisioning with the API
{: #creating-sds-host-api}

Make a `POST /hosts` request to create a host, and define the host by using the `name` parameter. Specify a host `name`, `nqn`, and `volume_id`.

Valid host names can include a combination of lowercase alpha-numeric characters (a-z, 0-9) and the hyphen (-), up to 63 characters. Host names must begin with a lowercase letter. Hypens cannot be used to start or end the name. Host names must be unique across the entire infrastructure. For example, if you create two volumes with the same name in the same deployment, a `Duplicae host name` error is displayed.
{: important}


```sh
curl -X 'POST' \
  '$sds_api_endpoint/v1/hosts' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "string",
  "nqn": "string",
  "volume_mappings": [
    {
      "volume_id": "string"
    }
  ]
}'
```
{: pre}

A successful response looks like this:

```json

COMING SOON

```
{: screen}




## Next steps
{: #next-step-creating-hosts-sds}

When you refresh the Hosts page, the new host appears at the beginning of the list of hosts.
{: ui}

You can continue creating more hosts or manage existing hosts.


