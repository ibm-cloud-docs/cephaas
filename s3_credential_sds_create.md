---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-12"

keywords: how to create cephaas S3 credential for object storage

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating S3 credential
{: #creating-s3-credential-sds}

Create S3 credentials for object storage by using the UI, CLI, or API.
{: shortdesc}



## Creating S3 credential using the UI
{: #creating-s3-credential-using-ui}
{: ui}

To create s3 credential, complete the following steps.

1. On the IBM Cloud console, navigate to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Service credentials** tab.

2. Click **New credential**.

3. Enter S3 credential **Name** and click **Add**.


## Creating S3 credential from the CLI
{: #creating-object-s3-credential-cli}
{: cli}

You can create S3 credential by using the command-line interface (CLI).

### Before you begin
{: #before-creating-s3-credential-cli}

Before you can use the CLI, you must install the IBM Cloud CLI and the `SDS` CLI plug-in.



Log in to the IBM Cloud.

```sh
ibmcloud login --sso -a cloud.ibm.com
```
{: pre}

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After successful authentication, you are prompted to choose your account. If you have access to multiple accounts, select the account that you want to log in as. Respond to any remaining prompts to finish logging in.
{: pre}

### Creating S3 credential from the CLI
{: #creating-s3-credential-cli}
{: help}
{: support}

Run the following command with the `INSTANCEID`, `ACCESS-KEY` and API endpoint to create a new object storage S3 credential or update an existing credential for the storage deployment.

```sh
ibmcloud software-defined-storage cred-create --instanceid INSTANCEID --access-key ACCESS-KEY --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cred-create --instanceid exampleString --access-key exampleString --url $sds_endpoint

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}


## Creating S3 credential with the API
{: #creating-s3-credential-api}
{: api}

You can create a S3 credential for object storage by specifying the access key.

```sh
curl -X 'POST' \
  '$sds_api_endpoint/v1/object/accounts/credentials?access-key=dsfdgdf2343435666' \
  -H 'accept: application/json' \

```
{: pre}

A successful response looks like this:

```json
{
  "access_key": "dsfdgdf2343435666",
  "secret_key": "ZGAelVfLo7QAzWlIAsTPYVckXMl8gIcKzvdXaDtJ"
}
```
{: screen}


