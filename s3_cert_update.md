---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-07"

keywords: cephaas settings, uploading S3 Certificate, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Uploading S3 certificate
{: #uploading-s3-certificate}

S3 TLS certificates are required to encrypt the S3 traffic and prevent `Man in the Middle` (MITM) attacks. You can upload a certificate file to add a new S3 SSL certificate or modify the existing certificate by using the UI, CLI or API.
{: shortdesc}

Before you can update or replace the certificate file, you need to upload the following by using UI, CLI, or API.
- Server side certificate (with the site's S3 endpoint FQDN in the SAN)
-  Key
-  Any intermediate CA Certificates
- CA (root) Certificate (for full chain)

For secure traffic, S3 Clients must use the associated CA certificate.
{: note}


## Uploading S3 certificate by using the UI
{: #updating-s3-certificate-using-ui}
{: ui}

To upload a S3 certificate, complete the following steps.

1. In the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), access your deployment and then go to **Settings**.

2. Click **Upload certificate**.

    Make sure that the file includes the root certificate, server certificate, and server key. The maximum file size that is allowed is 20 kb and the supported file type is `.pem` only.
    {: note}

3. Click **Upload** to choose the certificate from your computer.

4. Click **Save** to upload the file.


## Uploading S3 certificate from the CLI
{: #updating-s3-certificate-cli}
{: cli}

Use the `cert-update` command to update or replace existing SSL Certificates. You must include the parameters `--cert CERT` to specify the certifcate type to be used, and `--body BODY` to specify the file name with extension `.pem` that contains the TLS certificate.

Run the following command to upload the certificate.

```sh
ibmcloud software-defined-storage cert-update --cert CERT --body BODY --url string
```
{: pre}


See the following example.

```sh
ibmcloud sds cert-update --cert s3 --body file-name.pem

...
Name               s3
ValidCertificate   true
ValidKey           true
Trace              75cacd10-7918-44c0-9914-1723ebf74ee1
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crtu` as an alternative to `cert-update` for the CLI actions.
{: tip}

## Uploading S3 certificate with the API
{: #uploading-s3-certificate-api}
{: api}

Make a `PUT /certificates/{cert_type}` request to replace the S3 SSL Certificates or upload a new PEM formatted file if it does not exist.

Ensure that the replacement file that you are uploading has the server-side certificate and key.
{: requirement}

```sh
curl -X PUT $sds_endpoint/certificates/s3 \
  -H "accept: application/json" \
  -H "Authorization: Bearer $IAM_TOKEN"
  -H "Content-Type: text/plain" \
  -H "IBM-API-Version: 2025-02-01" \
  --data-binary "@<filename>.pem"
```
{: pre}


Example of a response when a certificate already exits in the system:

```json
curl -X PUT $sds_endpoint/certificates/s3 --data-binary "@both.pem" -H 'accept: application/json'  -H "Authorization: Bearer $IAM_TOKEN" -H 'IBM-API-Version: 2025-02-01'
...
{
  "name": "s3",
  "valid_certificate": true,
  "valid_key": true,
  "trace": "0d40c604-13f7-4181-be4b-b7621ed4d453",
  "errors": null
}
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$IAM_TOKEN` variables.


## Next steps
{: #next-step-updating-s3-certificate}

You can start creating and managing buckets and objects using the AWS CLI. For guidance, see [Using AWS CLI](/docs/cephaas?topic=cephaas-aws-cli).
