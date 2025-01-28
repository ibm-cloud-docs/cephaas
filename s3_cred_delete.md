---

copyright:
 years: 2024, 2025
lastupdated: "2025-01-28"

keywords: cephaas , delete service credential

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting object storage S3 credential
{: #deleting-s3-credential}

Delete an object storage S3 credential using the UI, CLI, or API.
{: shortdesc}


## Deleting an object storage credential in the UI
{: #deleting-s3-credential-ui}
{: ui}

To delete an object storage S3 credential, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Credentials** tab.

2. Select one or more service credential that you want to delete.

3. Click **Delete selected credentials** > **Delete**.

You will not be able to perform any s3 operations using the credentials after the delete process completes.
{: note}



## Deleting an objects storage credential from the CLI
{: #deleting-s3-credential-cli}
{: cli}

Use the `cred-delete` command and provide the `ACCESS-KEY` for the credential that you want to delete and the endpoint url.

You will not be able to perform any s3 operations using the credentials after the delete process completes.
{: note}

Run the following command to delete a credential.

```sh
ibmcloud software-defined-storage cred-delete --access-key ACCESS-KEY --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cred-delete --access-key exampleString --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}`.
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crd` as an alternative to `cred-delete` for the CLI actions.
{: tip}

## Deleting an object storage credential with the API
{: #deleting-s3-credential-api}
{: api}

You can delete a specific S3 credential using an access key.

```sh
curl -X 'DELETE' \
  '$sds_api_endpoint/v1/object/accounts/credentials?access-key=dsfdgdf2343435666' \
  -H 'accept: application/json' -H "Authorization: Bearer $token"
```
{: pre}

There is no response body for a successful delete operation. HTTP response code 200 is returned.


To verify that the credential is deleted, list the credential by making a `GET /account/credentials` call.
