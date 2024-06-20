---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-20"

keywords: sdsaas settings, uploading S3 Certificate

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Uploading S3 certificate
{: #uploading-s3-certificate-sds}

Upload S3 certificate by using the UI, CLI, or API. S3 certificates are required to secure the S3 endpoint.
{: shortdesc}




## Uploading S3 certificate using the UI
{: #uploading-s3-certificate-using-ui}
{: ui}

To upload a S3 certificate, complete the following steps.

1. On the IBM Cloud console, navigate to **SDS as a Service > Settings**.

2. Click **Upload certificate**. Add new certificate panel is displayed.

Make sure that the file includes the root certificate, server certificate and server key that allows virtual hosted buckets for your S3 endpoint. The maximum file size allowed is 20kb and the supported file type is `.pem` only.
{: note}

3. Click **Upload** to choose the certificate from your computer.

4. Click **Save** to upload the file.


## Uploading S3 certificate from the CLI
{: #uploading-s3-certificate-cli}
{: cli}

Use the `cert-upload` command to update the S3 SSL Certificates or creates them if they do not exist.

Run the following command and ensure you have provided the request body containing the S3 TLS certificate in the command to update the certificate.


```sh
ibmcloud software-defined-storage cert-upload --body BODY
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cert-upload --body exampleString
```
{: screen}


## Uploading S3 certificate with the API
{: #uploading-s3-certificate-api}
{: api}




## Next steps
{: #next-step-uploading-s3-certificate-sds}
