---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-04"

keywords: cephaas settings, uploading S3 Certificate

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Uploading S3 certificate
{: #uploading-s3-certificate}

S3 TLS certificates are required to encrypt the S3 traffic and prevent `Man in the Middle` (MITM) attacks. You can upload a certificate file to add a new S3 SSL certificate or modify the existing certificate by using the UI, CLI or API.
{: shortdesc}

Before you can upload the certificate file, you must create a server-side certificate with Subject Alternative Name (SAN) and the S3 DNS endpoint. Upload the server-side certificate along with the Key by using the UI, CLI, or API.

For secure traffic, S3 Clients must use the associated CA certificate.
{: note}



## Uploading S3 certificate by using the UI
{: #uploading-s3-certificate-using-ui}
{: ui}

To upload a S3 certificate, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Settings**.

2. Click **Upload certificate**.

    Make sure that the file includes the root certificate, server certificate, and server key. The maximum file size that is allowed is 20 kb and the supported file type is `.pem` only.
    {: note}

3. Click **Upload** to choose the certificate from your computer.

4. Click **Save** to upload the file.


## Uploading S3 certificate from the CLI
{: #uploading-s3-certificate-cli}
{: cli}

Use the `cert-upload` command to update the S3 SSL Certificates or create them if they do not exist. Include the parameters `--body BODY` to specify the file name with extension `.pem` that contains the S3 TLS certificate.

Run the following command to upload the certificate.

```sh
ibmcloud software-defined-storage cert-upload --body BODY --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage cert-upload \
    --body tempdir/cert-file.pem \
    --url $sds_endpoint
```
{: screen}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crtu` as an alternative to `cred-upload` for the CLI actions.
{: tip}

## Uploading S3 certificate with the API
{: #uploading-s3-certificate-api}
{: api}

Make a `POST /certificate/s3` call to update the S3 SSL Certificates or upload a new one if it does not exist.

Ensure that the file you are uploading have the server-side certificate and key.
{: requirement}

```sh
curl -X POST \
  "$sds_api_enpoint/v1/object/certificate/s3" \
  -H "accept: application/json" \
  -H "Authorization: $iam_token"
  -H "Content-Type: text/plain" \
  -H "IBM-API-Version: 2025-01-30" \
  --data-binary "@<filename>"
```
{: pre}

A successful response looks like this:

```json
{ "ValidCertificate": true, "ValidKey": true, "Error": null }

```
{: screen}

See [Setting up your CLI and API environment](docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$sds_api_endpoint` and `$iam_token` variables.
{: note}


## Next steps
{: #next-step-uploading-s3-certificate-sds}

You can start creating and managing buckets and objects using the AWS CLI. For guidance, see [Using AWS CLI](/docs/cephaas?topic=cephaas-aws-cli).
