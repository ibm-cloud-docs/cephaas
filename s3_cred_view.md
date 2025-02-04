---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-04"

keywords: cephaas service credential view, list

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# View object storage S3 credential details
{: #view-s3-credential}

View object storage S3 credential by using the UI, CLI and API.
{: shortdesc}


## View all S3 credential in the UI
{: #view-all-s3-credential-ui}
{: ui}

To view all the S3 credentials, go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Credentials** tab.



## View credential details from the CLI
{: #retrieving-s3-credential-details-cli}
{: cli}

Use the `creds` command to view the list of access keys that are created for a service instance (deployment).

Run the following command to retreive the credential details for the API endpoint.


```sh
ibmcloud software-defined-storage creds --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage creds --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.{uuid}.software-defined-storage.appdomain.cloud:{port number}/v1`.
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crl` as an alternative to `creds` for the CLI actions.
{: tip}

## Viewing an object storage credential with the API
{: #retrieving-s3-credential-api}
{: api}

Make the 'GET /accounts/credentials' request to retrieve and view one or all S3 credentials.

```sh
curl -X GET "$sds_api_endpoint/v1/object/accounts/credentials" -H "accept: application/json" -H "Authorization: $iam_token" -H "IBM-API-Version: 2025-01-30"
```
{: pre}

See [Setting up your CLI and API environment](docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$sds_api_endpoint` and `$iam_token` variables.
{: note}
