---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-28"

keywords: cephaas settings, creating S3 Certificate

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating S3 certificate
{: #create-s3-certificate}

S3 TLS certificates are required to encrypt the S3 traffic and prevent `Man in the Middle` (MITM) attacks. You can create a new S3 SSL certificate by using the CLI or API.
{: shortdesc}

You must create a server-side certificate with Subject Alternative Name (SAN) and the S3 DNS endpoint.

For secure traffic, S3 Clients must use the associated CA certificate.
{: note}




## Creating S3 certificate from the CLI
{: #creating-s3-certificate-cli}
{: cli}

Use the `cert-create` command to create new SSL Certificates if they do not exist. You must include the parameters `--cert CERT` to specify the certifcate type to be used, and `--body BODY` to specify the file name with extension `.pem` that contains the TLS certificate.

Run the following command to upload the certificate.

```sh
ibmcloud software-defined-storage cert-create --cert CERT --body BODY --url string
```
{: pre}

See the following example.

```sh
ibmcloud sds cert-create --cert s3 --url $sds_endpoint --body file-name.pem

...
Name               s3
ValidCertificate   true
ValidKey           true
Trace              75cacd10-7918-44c0-9914-1723ebf74ee1
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crtc` as an alternative to `cert-create` for the CLI actions.
{: tip}

## Creating S3 certificate with the API
{: #creating-s3-certificate-api}
{: api}

Make a `POST /certificate/{cert_type}` request to create the S3 SSL Certificates.

Ensure that you have the server-side certificate and key handy.
{: requirement}

```sh
curl -X POST $sds_endpoint/certificates/s3 \
  -H "accept: application/json" \
  -H "Authorization: Bearer $IAM_TOKEN"
  -H "Content-Type: text/plain" \
  -H "IBM-API-Version: 2025-02-01" \
  --data-binary "@<filename>.pem"
```
{: pre}


Example of a response when a certificate is created:

```json
curl -X POST $sds_endpoint/certificates/s3 --data-binary "@both.pem" -H 'accept: application/json'  -H "Authorization: Bearer $TOKEN" -H 'IBM-API-Version: 2025-01-15'
...

{
  "name": "s3",
  "valid_certificate": true,
  "valid_key": true,
  "trace": "d0313b8e-adce-4232-96b4-627587bc0982",
  "errors": null
}
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

See [Setting up your API environment](/docs/cephaas?topic=cephaas-set-up-environment&interface=api) for instructions on how to set the `$IAM_TOKEN` variables.
{: note}


## Next steps
{: #next-step-creating-s3-certificate}

You can start creating and managing buckets and objects using the AWS CLI. For guidance, see [Using AWS CLI](/docs/cephaas?topic=cephaas-aws-cli).
