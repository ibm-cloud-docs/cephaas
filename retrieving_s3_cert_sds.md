---

copyright:
 years: 2024, 2024
lastupdated: "2024-06-20"

keywords: sdsaas settings, retrieve S3 Certificate details, S3 SSL certificate expiration date, status

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Retrieving S3 certificate expiration date and status
{: #retrieving-s3-certificate-details-sds}

Retrieve and view the expiration date and status of the S3 SSL certificate by using CLI. S3 certificates are required to secure the S3 endpoint.
{: shortdesc}



## Retrieving S3 certificate expiration date and status from the CLI
{: #retrieving-s3-certificate-details-cli}
{: cli}

Use the `certificate` command to retrieve and view the S3 SSL Certificates expiration date and it's status.

Run the following command and ensure you have provided the request body containing the S3 TLS certificate in the command to update the certificate.


```sh
ibmcloud software-defined-storage certificate
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage certificate
```
{: screen}





## Next steps
{: #next-step-retrieving-s3-certificate-details-sds}
