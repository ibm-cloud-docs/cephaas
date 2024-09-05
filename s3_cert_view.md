---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-05"

keywords: cephaas settings, retrieve S3 Certificate details, S3 SSL certificate expiration date, status

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# View S3 certificate expiration date and status
{: #viewing-sds-s3-certificate-details-sds}

S3 certificates are required to secure the S3 endpoint.

This section provides guidance on how to view the expiration date and status of the S3 SSL certificate.
{: shortdesc}


## View S3 certificate details using the UI
{: #view-sds-s3-certificate-using-ui}
{: ui}

To view the expiration date and status of the S3 certificate, on the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Settings**.

Here, you can view the **S3 certificate** expiration date and status if it exists in the system.


## Retrieving S3 certificate expiration date and status from the CLI
{: #retrieving-sds-s3-certificate-details-cli}
{: cli}

Use the `certificate` command to retrieve and view the S3 SSL Certificates expiration date and it's status.

Run the following command and ensure you have provided the `INSTANCEID` and endpoint url.

```sh
ibmcloud software-defined-storage cert --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage certificate --instanceid abc --url $sds_endpoint
...

ExpirationDate  "2024-08-13T05:23:42Z"
Expired          false

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}


## Retrieve S3 certificate details with the API
{: #retrieve-sds-s3-certificate-api}
{: api}

Make a `GET /s3tlscertstatus` to retrieve the S3 certficate expiration date and status.

```sh
curl -X 'GET' '$sds_api_endpoint/v1/object/s3tlscertstatus' -H 'accept: application/json'
```
{: pre}

A successful response looks like this:

```json
{
  "ExpirationDate": "2024-08-13T05:23:42Z",
  "Expired": false
}
```
{: screen}
