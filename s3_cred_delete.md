---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-25"

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

```sh
ibmcloud software-defined-storage cred-delete --access-key test-key1 --url $sds_endpoint
Are you sure you want to delete?[y/n]> y
...
OK
```
{: screen}


The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crd` as an alternative to `cred-delete` for the CLI actions.
{: tip}

## Deleting an object storage credential with the API
{: #deleting-s3-credential-api}
{: api}

You can delete a specific S3 credential using an access key.

```sh
curl -X DELETE "$sds_api_endpoint/v1/s3_credentials/{access-key}" \
  -H "accept: application/json" \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "IBM-API-Version: 2025-02-01"
```
{: pre}

See example of a delete request.

```sh
curl -X DELETE "$sds_api_endpoint/v1/s3_credentials/dsfdgdf2343435666" \
  -H "accept: application/json" \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H "IBM-API-Version: 2025-02-01"
```
{: screen}

There is no response body for a successful delete operation. HTTP response code 204 is returned.

To verify that the credential is deleted, list the credential by making a `GET /s3_credentials` request.


The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$IAM_TOKEN` variables.
