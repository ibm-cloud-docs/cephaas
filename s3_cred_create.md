---

copyright:
 years: 2024, 2025
lastupdated: "2025-01-31"

keywords: how to create cephaas S3 credential for object storage

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating object storage S3 credential
{: #creating-s3-credential-sds}

A credential consist of an Access Key and Secret Key pair for use with S3-compatible tools and libraries that require authentication.
{: shortdesc}




Create S3 credentials for object storage by using the UI, CLI, or API.

To create a credential, you must be granted the Administrator platform role or a custom role. For more information, see the [IAM access documentation](/docs/cephaas?topic=cephaas-managing-iam).
{: requirement}

The secret key cannot be viewed after you create the credential. So you must save or download the key in a place from where you can retrieve when needed.
{: important}

## Creating S3 credential using the UI
{: #creating-s3-credential-using-ui}
{: ui}

To create s3 credential, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Credentials** tab.

2. Click **New credential**.

3. Enter S3 credential **Name** and click **Add**.

    Avoid using special characters when creating access keys with the exception of dashes `-` and underscores `_` symbols. All alphabets and numbers are allowed.
    {: important}

4. After the credential is created, **Copy** the credential or click **Download** to save the credential to your local system.

You will not be able to see the credential again after you close this message. Make sure to save or download the credential.
{: note}


## Creating S3 credential from the CLI
{: #creating-s3-credential-cli}
{: cli}

Run the `cred-create` command with the `ACCESS-KEY` and API endpoint to create a new object storage S3 credential for the storage deployment.

Avoid using special characters when creating access keys with the exception of dashes `-`, underscores `_`, and the equal sign `=` symbols. All alphabets and numbers are allowed.
{: important}

```sh
ibmcloud software-defined-storage cred-create --access-key ACCESS-KEY --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cred-create --access-key exampleString --url $sds_endpoint

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.{uuid}.software-defined-storage.appdomain.cloud:{port number}/v1`.
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crc` as an alternative to `cred-create` for the CLI actions.
{: tip}

## Creating S3 credential with the API
{: #creating-s3-credential-api}
{: api}

You can create a S3 credential for object storage by specifying the access key.

Avoid using special characters when creating access keys with the exception of dashes `-`, underscores `_`, and the equal sign `=` symbols. All alphabets and numbers are allowed.
{: important}

```sh
curl -X 'POST' \
  '$sds_api_endpoint/v1/object/accounts/credentials?access-key=dsfdgdf2343435666' \
  -H 'accept: application/json' \
  -H "Authorization: $iam_token"
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

See [Setting up your CLI and API environment](docs/cephaas?topic=cephaas-set-up-environment&interface=api) for instructions on how to set the `$sds_api_endpoint` and `$iam_token` variables.
{: note}
