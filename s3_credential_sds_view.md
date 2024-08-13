---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-13"

keywords: sdsaas service credential view, list

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# View S3 credential details
{: #view-s3-credential-sds}

View object storage S3 credential by using the UI and CLI.
{: shortdesc}


## View all S3 credential in the UI
{: #view-all-sds-s3-credential-ui}
{: ui}

To view all the S3 credentials, go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Service credentials** tab.


## View credential detail in the UI
{: #view-sds-s3-credential-detail-ui}
{: ui}

To view S3 credential details,

1. Go to **{{site.data.keyword.cephaas_full_notm}} > Object Storage > Service credentials** tab.

2. Click the credential name. The row expands downwards to display the details.


## View credential details from the CLI
{: #retrieving-s3-credential-details-cli}
{: cli}

Use the `credentials` command to view the list of access keys that are created for a service instance (deployment).

Run the following command and make sure that you have provided `INSTANCEID` of the credential whose details you want to view and the API endpoint.


```sh
ibmcloud software-defined-storage credentials --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage credentials --instanceid exampleString --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}
