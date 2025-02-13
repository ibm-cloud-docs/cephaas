---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-13"

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

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crl` as an alternative to `creds` for the CLI actions.
{: tip}

## Viewing an object storage credential with the API
{: #retrieving-s3-credential-api}
{: api}

Make the `GET /s3_credentials` request to retrieve and view one or all S3 credentials.

```sh
curl -X GET "$sds_api_endpoint/v1/s3_credentials" -H "accept: application/json" -H "Authorization: $iam_token" -H "IBM-API-Version: 2025-02-01"
```
{: pre}

```json
{
  "s3_credentials": [
    "test-key-1",
    "test-key-2"
  ]
}
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment&interface=api) for instructions on how to set the `$iam_token` variables.
