---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-18"

keywords: cephaas, developer, getting started, command-line interface, cli, developer tools, ceph as a service

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}


# For developers
{: #gs-dev}

The powerful features of {{site.data.keyword.cephaas_full}} are available to a developer directly from the command-line.
{: shortdesc}

First, ensure that you have the [{{site.data.keyword.cloud}} Platform CLI](/docs/cli), [IBM Developer Tools](/docs/sdk-handbook?topic=sdk-handbook-devtools) and [Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#tf_installation_step) installed.



## Using the API
{: #gs-dev-api}

For managing the data stored in {{site.data.keyword.cephaas_full_notm}}, you can use the following S3 API compatible tools:

* [Block storage management API](/apidocs/block-storage)

* [Object storage administration API](/apidocs/object-storage)

* For Object storage S3 API, see [AWS CLI](/docs/cephaas?topic=cephaas-aws-cli) with HMAC credentials for compatibility


## Using the SDK
{: #gs-dev-sdk}

{{site.data.keyword.cephaas_short}} SDK is currently available only for [Go](/docs/cephaas?topic=cephaas-using-go). These libraries are forked and modified versions of the AWS S3 SDKs that support [IAM token-based authentication](/docs/cephaas?topic=cephaas-iam-overview).
