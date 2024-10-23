---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-23"

keywords: cephaas, developer, getting started, command-line interface, cli

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}


# For developers
{: #gs-dev}

The powerful features of {{site.data.keyword.cephaas_full}} are available to a developer directly from the command-line.
{: shortdesc}

First, ensure that you have the [{{site.data.keyword.cloud}} Platform CLI](/docs/cli) and [IBM Developer Tools](https://cloud.ibm.com/docs/cloudnative/idt/index.html) installed.



## Using the API
{: #gs-dev-api}

For managing data stored in {{site.data.keyword.cephaas_full_notm}}, you can use S3 API compatible tools like the [AWS CLI](/docs/cephaas?topic=cephaas-aws-cli) with HMAC credentials for compatibility.

## Using libraries and SDKs
{: #gs-dev-sdk}

{{site.data.keyword.cephaas_short}} SDKs are currently available only for [Go](/docs/cephaas?topic=cephaas-using-go). These libraries are forked and modified versions of the AWS S3 SDKs that support [IAM token-based authentication](/docs/cephaas?topic=cephaas-iam-overview), as well as support for [Key Protect](/docs/cephaas?topic=cephaas-encryption).
