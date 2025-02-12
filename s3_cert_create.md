---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-12"

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

Use the `cert-create` command to create new SSL Certificates if they do not exist. Include the parameters `--body BODY` to specify the file name with extension `.pem` that contains the TLS certificate.

Run the following command to upload the certificate.

```sh
ibmcloud software-defined-storage cert-create --body BODY --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage cert-create \
  --cert s3 \
  --body tempdir/test-file.txt \
  --url exampleString
```
{: screen}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crtc` as an alternative to `cert-create` for the CLI actions.
{: tip}

## Creating S3 certificate with the API
{: #creating-s3-certificate-api}
{: api}

Make a `POST /certificate/{cert_type}` call to create the S3 SSL Certificates.

Ensure that you have the server-side certificate and key handy.
{: requirement}

```sh
curl -X POST \
  "$sds_api_enpoint/v1/certificates/s3" \
  -H "accept: application/json" \
  -H "Authorization: $iam_token"
  -H "Content-Type: text/plain" \
  -H "IBM-API-Version: 2025-02-01" \
  --data-binary "@<filename>.pem"
```
{: pre}


Example of a response when a certificate is created:

```json
(sdsaas_env) ~ % curl -X POST "$SDS_ENDPOINT/v1/certificates/s3" --data-binary "@both.pem" -H 'accept: application/json'  -H "Authorization: Bearer $TOKEN" -H 'IBM-API-Version: 2025-01-15' | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4677  100   102  100  4575     54   2423  0:00:01  0:00:01 --:--:--  2477
{
  "errors": [],
  "valid_certificate": true,
  "value_key": true
}
```
{: screen}

See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$sds_api_endpoint` and `$iam_token` variables.
{: note}


## Next steps
{: #next-step-creating-s3-certificate}

You can start creating and managing buckets and objects using the AWS CLI. For guidance, see [Using AWS CLI](/docs/cephaas?topic=cephaas-aws-cli).
