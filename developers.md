---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-09"

keywords: cephaas, developer, getting started, command line interface, cli

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# For developers
{: #gs-dev}

The powerful features of {{site.data.keyword.cephaas_full}} are available to a developer directly from the command line.
{: shortdesc}

First, ensure that you have the [{{site.data.keyword.cloud}} Platform CLI](https://cloud.ibm.com/docs/cli/index.html) and [IBM Developer Tools](https://cloud.ibm.com/docs/cloudnative/idt/index.html) installed.

## Create an {{site.data.keyword.cephaas_full_notm}} deployment
{: #gs-dev-provision}

1. First, make sure that you have an API key. Get it from [IBM Cloud Identity and Access Management](https://cloud.ibm.com/iam/apikeys).
2. Log in to {{site.data.keyword.cloud_notm}} Platform by using the CLI. It's also possible to store the API key in a file or set it as an environment variable.

    ```sh
    ibmcloud login --apikey <value>
    ```
    {: pre}

3. Next, create an {{site.data.keyword.cephaas_full_notm}} deployment by specifying the name for the deployment and the Standard plan (see [Choosing a plan and creating an instance](/docs/sdsaas?topic=sdsaas-provision)). Now you have a CRN for the instance.

    ```sh
    ibmcloud resource service-instance-create <instance-name> software-defined-storage <plan> global
    ```
    {: pre}

When trying to create a new instance, if you encounter the error `No resource group targeted`, it indicates that the default resource group is not available and that a resource group must be explicitly set. A list of available resource groups can be found using `ibmcloud resource groups` and the target can be set with `ibmcloud target -g <resource-group>`.
{: tip}

The [Getting Started guide](/docs/sdsaas?topic=sdsaas-getting-started) walks through the basic steps of creating deployment instances, volumes and objects, as well as inviting users and creating policies. A list of basic 'curl' commands can be found [here](/docs/sdsaas?topic=sdsaas-curl).

Learn more about using the {{site.data.keyword.cloud_notm}} CLI to create applications, manage Kubernetes clusters, and more [in the documentation](/docs/cli?topic=cli-ibmcloud_cli).

## Using the API
{: #gs-dev-api}

For managing data stored in {{site.data.keyword.cephaas_full_notm}}, you can use S3 API compatible tools like the [AWS CLI](/docs/sdsaas?topic=sdsaas-aws-cli) with HMAC credentials for compatibility.

## Using libraries and SDKs
{: #gs-dev-sdk}

{{site.data.keyword.cephaas_short}} SDKs are currently available only for [Go](/docs/sdsaas?topic=sdsaas-using-go). These libraries are forked and modified versions of the AWS S3 SDKs that support [IAM token-based authentication](/docs/sdsaas?topic=sdsaas-iam-overview), as well as support for [Key Protect](/docs/sdsaas?topic=sdsaas-encryption).
