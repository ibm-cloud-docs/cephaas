---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-20"

keywords: how to create cephaas S3 credential for object storage

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating object storage S3 credential
{: #creating-s3-credential-sds}

A credential provides the information required to provide authentication for applications.
{: shortdesc}

The credentials are always associated with a Service ID, and new Service IDs can be created along with a new credential.

Create S3 credentials for object storage by using the UI, CLI, or API.

To create a credential, you must be granted the Administrator platform role or a custom role. For more information, see the [IAM access documentation](/docs/sdsaas?topic=sdsaas-managing-iam).
{: important}

## Creating S3 credential using the UI
{: #creating-s3-credential-using-ui}
{: ui}

To create s3 credential, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Credentials** tab.

2. Click **New credential**.

3. Enter S3 credential **Name** and click **Add**.

4. After the credential is created, **Copy** the credential or click **Download** to save the credential to your local system.

You will not be able to see the credentials again after you close this message. Make sure to save the credentials.
{: note}


## Creating S3 credential from the CLI
{: #creating-s3-credential-cli}
{: cli}

Run the `cred-create` command with the `ACCESS-KEY` and API endpoint to create a new object storage S3 credential for the storage deployment.

```sh
ibmcloud software-defined-storage cred-create --access-key ACCESS-KEY --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cred-create --access-key exampleString --url $sds_endpoint

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
  -H "Authorization: $token"
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
