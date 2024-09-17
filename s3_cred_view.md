---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-17"

keywords: sdsaas service credential view, list

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# View object storage S3 credential details
{: #view-s3-credential-sds}

View object storage S3 credential by using the UI, CLI and API.
{: shortdesc}


## View all S3 credential in the UI
{: #view-all-sds-s3-credential-ui}
{: ui}

To view all the S3 credentials, go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Credentials** tab.



## View credential details from the CLI
{: #retrieving-s3-credential-details-cli}
{: cli}

Use the `creds` command to view the list of access keys that are created for a service instance (deployment).

Run the following command and make sure that you have provided `INSTANCEID` of the credential whose details you want to view and the API endpoint.


```sh
ibmcloud software-defined-storage creds --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage creds --instanceid exampleString --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}



## Viewing an object storage credential with the API
{: #retrieving-s3-credential-api}
{: api}

You can retrieve and view single S3 credential using an access key.

```sh
curl -X 'GET /accounts/credentials' '$sds_api_endpoint/v1/object/accounts/credentials?access-key=dsfdgdf2343435666' -H 'accept: application/json' -H "Authorization: $token"
```
{: pre}


## Viewing all object storage credentials with the API
{: #retrieving-all-credentials-api}
{: api}

You can retrieve and list all the available S3 credential using an access key.

```sh
curl -X 'GET /accounts/credentials' '$sds_api_endpoint/v1/object/accounts/credentials' -H 'accept: application/json' -H "Authorization: $token"
```
{: pre}
