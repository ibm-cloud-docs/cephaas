---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-06"

keywords: cephaas settings, retrieve S3 Certificate details, S3 SSL certificate expiration date, status

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# View S3 certificate expiration date and status
{: #viewing-sds-s3-certificate-details-sds}

S3 TLS certificates are required to encrypt the S3 traffic and prevent `Man in the Middle` (MITM) attacks.

This section provides guidance on how to view the expiration date and status of the S3 SSL certificate.
{: shortdesc}


## View S3 certificate details by using the UI
{: #view-sds-s3-certificate-using-ui}
{: ui}

To view the expiration date and status of the S3 certificate, on the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Settings**.

Here, you can view the **S3 certificate** expiration date and status.


## Retrieving S3 certificate expiration date and status from the CLI
{: #retrieving-sds-s3-certificate-details-cli}
{: cli}

Use the `certificate` command to retrieve and view the S3 SSL Certificates expiration date and its status.

Run the following command and ensure that you have provided the endpoint url.

```sh
ibmcloud software-defined-storage cert --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cert --url $sds_endpoint
...

ExpirationDate  "2024-08-13T05:23:42Z"
Expired          false

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` for the CLI actions.
{: tip}

## Retrieve S3 certificate details with the API
{: #retrieve-sds-s3-certificate-api}
{: api}

Make a `GET /certificates/{cert_type}` to retrieve the S3 certificate expiration date and status.

```sh
curl -X GET "$sds_api_endpoint/v1/object/certificates" -H "accept: application/json" -H "IBM-API-Version: 2025-01-30"
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


Use this API call to detect when the S3 certificate is about to expire and update them before they expire so that it does not affect the I/O usage. You can automate the expiry notification process within your environment to prevent an outage.
{: tip}

See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$sds_api_endpoint` and `$iam_token` variables.
{: note}
