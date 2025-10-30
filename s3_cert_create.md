---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-30"

keywords: cephaas settings, creating S3 Certificate, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating S3 certificate
{: #create-s3-certificate}

S3 TLS certificates are required to encrypt the S3 traffic and prevent **Man in the Middle (MITM)** attacks. You can create a new S3 SSL certificate by using the CLI or API.
{: shortdesc}

You must create a server-side certificate with one or more Subject Alternative Name(s) (SAN)(s) which match the configured S3 IP address and/or configured DNS hostname(s).

For secure traffic, S3 Clients must use the associated CA certificate.
{: note}

The following are the prerequisites for generating S3 TLS certificate.

* The TLS Certificate provided must be formatted as a `pem` file according to the RFC-7468 standard.
* It must contain at least one CERTIFICATE property for the related certificates, which should be the end-entity certificate at a minimum.
* It must contain one of the following properties for the respective private key: PRIVATE KEY, RSA PRIVATE KEY, or EC PRIVATE KEY.
* The private key must be consistent with the main/end-entity certificate.

If multiple certificate properties are included, the order of items in the `pem` file should be: end-entity certificate, intermediate certificate, root certificate, private key. For example: `cat tls.crt ca.crt tls.key > both.pem` is the correct order for the `pem` file to be used by {{site.data.keyword.cephaas_full_notm}}.
{:important:}

If any of these above prerequisites are not followed, the certificate `pem` file may be considered invalid and will not work with CephaaS.




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
ibmcloud sds cert-create --cert s3 --body file-name.pem

...
Name               s3
ValidCertificate   true
ValidKey           true
Trace              75cacd10-7918-44c0-9914-1723ebf74ee1
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_full_notm}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

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


An example of a response when a certificate is created:

```json
curl -X POST $sds_endpoint/certificates/s3 --data-binary "@both.pem" -H 'accept: application/json'  -H "Authorization: Bearer $IAM_TOKEN" -H 'IBM-API-Version: 2025-01-15'
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

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_full_notm}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

See [Setting up your API environment](/docs/cephaas?topic=cephaas-set-up-environment&interface=api) for instructions on how to set the `$IAM_TOKEN` variables.
{: note}


## Next steps
{: #next-step-creating-s3-certificate}

You can start creating and managing buckets and objects by using the AWS CLI. For guidance, see [Using AWS CLI](/docs/cephaas?topic=cephaas-aws-cli).
