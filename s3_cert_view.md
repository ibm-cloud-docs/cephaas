---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-12"

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


## Retrieve configured certificates using the CLI
{: #retrieve-list-config-certs-cli}
{: cli}

You can retrieve the list of configured certificates by using the CLI command `cert-types`.

```sh
ibmcloud software-defined-storage cert-types --url string
```
{: pre}

See following command example.


```sh
ibmcloud software-defined-storage cert-types --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `crtt` as an alternative to `cred-types` for the CLI actions.
{: tip}



## Retrieving S3 certificate expiration date and status using the CLI
{: #retrieving-sds-s3-certificate-details-cli}
{: cli}

Use the `cert` command to retrieve and view the SSL Certificates expiration date and its status.

Run the following command and ensure that you have provided the endpoint url.

```sh
ibmcloud software-defined-storage cert --cert s3 --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage cert --cert s3 --url $sds_endpoint
...

Name             s3
ExpirationDate  "2024-08-13T05:23:42Z"
Expired          false

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` for the CLI actions.
{: tip}


## Retrieve configured certificates with the API
{: #list-config-certs-api}
{: api}

Make `Get /certificates` to retrieve the list of configured certificates.

```sh
curl -X GET "$sds_api_endpoint/v1/certificates" -H "accept: application/json" -H "Authorization: $iam_token" -H "IBM-API-Version: 2025-02-01"
```
{: pre}

Example of a successful response.

```sh
(sdsaas_env) ~ % curl -X GET "$sds_api_endpoint/v1/certificates" -H "accept: application/json" -H "Authorization: $iam_token" -H 'IBM-API-Version: 2025-01-15' | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    23  100    23    0     0      8      0  0:00:02  0:00:02 --:--:--     8
{
  "certificates": [
    "s3"
  ]
}
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$iam_token` variables.




## Retrieve S3 certificate details with the API
{: #retrieve-sds-s3-certificate-api}
{: api}

Make a `GET /certificates/{cert_type}` to retrieve the S3 certificate expiration date and status.

```sh
curl -X GET "$sds_api_endpoint/v1/certificates/s3" -H "accept: application/json" -H "IBM-API-Version: 2025-02-01"
```
{: pre}

A successful response looks like this:

```json
{
  "name": "s3",
  "expiration_date": "2035-02-04T08:33:04Z",
  "expired": false
}
```
{: screen}

Example of a response when there is no certificate available:
```sh
(sdsaas_env) ~ % curl -X GET "$sds_api_endpoint/v1/certificates/s3" -H 'accept: application/json'  -H "Authorization: Bearer $TOKEN" -H 'IBM-API-Version: 2025-01-15' | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    50  100    50    0     0     26      0  0:00:01  0:00:01 --:--:--    26
{
  "name": "s3",
  "expiration_date": "",
  "expired": false
}
```
{: screen}


Use this API call to learn when the S3 certificate is about to expire and update them before they expire, so that it does not affect the I/O usage. You can automate the expiry notification process within your environment to prevent an outage.
{: tip}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


See [Setting up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment) for instructions on how to set the `$iam_token` variables.
