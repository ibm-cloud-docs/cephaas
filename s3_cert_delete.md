---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-11"

keywords: cephaas, delete s3 certificate, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting S3 certificate
{: #deleting-s3-cert}

Delete S3 credential using the CLI, or API.
{: shortdesc}




## Deleting S3 certificate from the CLI
{: #deleting-s3-cert-cli}
{: cli}

To delete a certificate, you can run the `cert-delete` command from CLI. Provide the certificate type and the endpoint url.

```sh
ibmcloud software-defined-storage cert-delete --cert CERT --url string
```
{: pre}

Example of deleting a certificate.

```bash
ibmcloud software-defined-storage cert-delete --url $sds_endpoint --cert s3
Are you sure you want to delete?[y/n]> y
...
OK
```
{: screen}


The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crd` as an alternative to `cred-delete` for the CLI actions.
{: tip}

## Deleting S3 certificate with the API
{: #deleting-s3-cert-api}
{: api}

Make `DELETE /certificates/{cert_type}` request to delete a S3 certificate.

```sh
curl -X DELETE $sds_endpoint/certificates/s3 \
  -H 'accept: application/json' \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

There is no response body for a successful delete operation. HTTP response code 204 is returned.

To verify that the credential is deleted, list the credential by making a `GET /s3_credentials` request.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the`$IAM_TOKEN` variables.
