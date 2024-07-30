---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-30"

keywords: sdsaas , delete service credential

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Delete service credential
{: #deleting-sds-service-credential}

Delete a service credential using the UI, CLI, or API.
{: shortdesc}


## Deleteing a service credential in the UI
{: #deleting-sds-service-credential-ui}
{: ui}

To delete a service credential, complete the following steps.

1. On the IBM Cloud console, navigate to **SDS as a Service > Object Storage > Service credentials** tab.

2. Select the service credential that you wish to delete.

3. Click **Delete** to confirm deletion.

All access granted to any resources using this credential will be lost once the credential is deleted.
{: note}

## Deleting a service credential from the CLI
{: #deleting-sds-service-credential-cli}
{: cli}

Use the `cred-delete` command and provide the `INSTANCEID` of the SDSaaS instance along with the `ACCESS-KEY` for the credential that you want to delete.

You will not be able to perform any s3 operations using the credentials after the delete process completes.
{: note}

Run the following command to delete a credential.

```sh
ibmcloud software-defined-storage cred-delete --instanceid INSTANCEID --access-key ACCESS-KEY
```
{: pre}

See the following example where `sds_endpoint` is an environment variable that points to the endpoint that is provided to the user when `software-defined-storage (aliase: sds)` was configured and is in the for of a URL. For example, `https://<on-prem>.endpoint.com:<port number>/v1`.

```bash
ibmcloud software-defined-storage cred-delete --instanceid exampleString --access-key exampleString --url $sds_endpoint
```
{: screen}


## Deleting a service credential with the API
{: #creating-service-credential-api}
{: api}

You can delete a specific credential for the "default" storage account using an access key.

```sh
curl -X 'DELETE' \
  '$sds_api_endpoint/v1/object/accounts/credentials?access-key=dsfdgdf2343435666' \
  -H 'accept: application/json'

```
{: pre}

There is no response body for a successful delete operation. HTTP response code 200 is returned along with message "OK - Storage account credentials were deleted successfully".


To verify that the credential is deleted, list the credential by making a `GET /account/credentials` call.

## Next steps
{: #next-step-delete-service-creds-sds}
