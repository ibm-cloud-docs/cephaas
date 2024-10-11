---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-11"

keywords: sdsaas , delete service credential

subcollection: sdsaas

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

2. Select one service credential that you want to delete.

3. Click **Delete**.

All access granted to any resources using this credential will be lost once the credential is deleted.
{: note}

## Deleting multiple object storage credential in the UI
{: #deleting-mulitple-s3-credential-ui}
{: ui}

To delete multiple object storage S3 credential, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Credentials** tab.

2. Select one or more credentials that you want to delete.

3. Click **Delete selected credentials** > **Delete**.

All access granted to any resources using these credentials will be lost once the credentials are deleted.
{: note}


## Deleting an objects storage credential from the CLI
{: #deleting-s3-credential-cli}
{: cli}

Use the `cred-delete` command and provide the `INSTANCEID` of the deployment (service instance) along with the `ACCESS-KEY` for the credential that you want to delete and the endpoint url.

You will not be able to perform any s3 operations using the credentials after the delete process completes.
{: note}

Run the following command to delete a credential.

```sh
ibmcloud software-defined-storage cred-delete --instanceid INSTANCEID --access-key ACCESS-KEY --url string
```
{: pre}

See the following example where `sds_endpoint` is an environment variable that points to the endpoint that is provided to the user when `software-defined-storage (aliase: sds)` was configured and is in the for of a URL. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.

```bash
ibmcloud software-defined-storage cred-delete --instanceid exampleString --access-key exampleString --url $sds_endpoint
```
{: screen}

You can also use the aliase `sds` an alternative to `software-defined-storage` for the CLI actions.
{: tip}

## Deleting an object storage credential with the API
{: #deleting-s3-credential-api}
{: api}

You can delete a specific S3 credential using an access key.

```sh
curl -X 'DELETE' \
  '$sds_api_endpoint/v1/object/accounts/credentials?access-key=dsfdgdf2343435666' \
  -H 'accept: application/json' -H "Authorization: $token"
```
{: pre}

There is no response body for a successful delete operation. HTTP response code 200 is returned.


To verify that the credential is deleted, list the credential by making a `GET /account/credentials` call.
