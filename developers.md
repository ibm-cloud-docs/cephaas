---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-29"

keywords: cephaas, developer, getting started, command line interface, cli

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# For developers
{: #gs-dev}

The powerful features of {{site.data.keyword.cephaas_full}} are available to a developer directly from the command line.
{: shortdesc}

First, ensure that you have the [{{site.data.keyword.cloud}} Platform CLI](https://cloud.ibm.com/docs/cli/index.html) and [IBM Developer Tools](https://cloud.ibm.com/docs/cloudnative/idt/index.html) installed.

## Create an instance of {{site.data.keyword.cephaas_full_notm}}
{: #gs-dev-provision}

1. First, make sure that you have an API key. Get it from [IBM Cloud Identity and Access Management](https://cloud.ibm.com/iam/apikeys).
2. Log in to {{site.data.keyword.cloud_notm}} Platform by using the CLI. It's also possible to store the API key in a file or set it as an environment variable.

    ```sh
    ibmcloud login --apikey <value>
    ```
    {: pre}

3. Next, create an instance of {{site.data.keyword.cephaas_full_notm}} specifying the name for the instance and the Standard plan (see [Choosing a plan and creating an instance](/docs/sdsaas?topic=sdsaas-provision)). Now you have a CRN for the instance.

    ```sh
    ibmcloud resource service-instance-create <instance-name> cloud-object-storage <plan> global
    ```
    {: pre}

When trying to create a new instance, if you encounter the error `No resource group targeted`, it indicates that the default resource group is not available and that a resource group must be explicitly set. A list of available resource groups can be found using `ibmcloud resource groups` and the target can be set with `ibmcloud target -g <resource-group>`.
{: tip}

The [Getting Started guide](/docs/sdsaas?topic=sdsaas-getting-started) walks through the basic steps of creating buckets and objects, as well as inviting users and creating policies. A list of basic 'curl' commands can be found [here](/docs/sdsaas?topic=sdsaas-curl).

Learn more about using the {{site.data.keyword.cloud_notm}} CLI to create applications, manage Kubernetes clusters, and more [in the documentation](/docs/cli?topic=cli-ibmcloud_cli).

## Using the API
{: #gs-dev-api}

For managing data stored in {{site.data.keyword.cephaas_short}}, you can use S3 API compatible tools like the [AWS CLI](/docs/sdsaas?topic=sdsaas-aws-cli) with [HMAC credentials](/docs/sdsaas?topic=sdsaas-hmac-credentials-main) for compatibility. As IAM tokens are relatively easy to work with, `curl` is a good choice for basic testing and interaction with your storage. More information can be found in the [`curl`](/docs/sdsaas?topic=sdsaas-curl) and the [API](/docs/sdsaas?topic=sdsaas-compatibility-api) documentation.

## Using libraries and SDKs
{: #gs-dev-sdk}

{{site.data.keyword.cephaas_short}} SDKs are available for [Python](/docs/sdsaas?topic=sdsaas-python), [Java](/docs/sdsaas?topic=sdsaas-java), [Go](/docs/sdsaas?topic=sdsaas-using-go), and [Node.js](/docs/sdsaas?topic=sdsaas-node). These libraries are forked and modified versions of the AWS S3 SDKs that support [IAM token-based authentication](/docs/sdsaas?topic=sdsaas-iam-overview), as well as support for [Key Protect](/docs/sdsaas?topic=sdsaas-encryption).

## Building applications on IBM Cloud
{: #gs-dev-apps}

{{site.data.keyword.cloud}} provides flexibility to developers in choosing the right architectural and deployment options for a given application. Run your code on [bare metal](https://cloud.ibm.com/catalog/infrastructure/bare-metal), in [virtual machines](https://cloud.ibm.com/catalog/infrastructure/virtual-server-group), in [containers](https://cloud.ibm.com/kubernetes/catalog/cluster), or by using a [serverless framework](/docs/solution-tutorials?topic=solution-tutorials-serverless-webapp).

The [Cloud Native Computing Foundation](https://www.cncf.io) fostered [Kubernetes](https://kubernetes.io) container orchestration framework, which forms the foundation for the {{site.data.keyword.cloud}} Kubernetes Service. Developers who want to use Object Storage for persistent storage in their Kubernetes applications can learn more at the following links:

 * [Choosing a storage solution](/docs/containers?topic=containers-storage-plan)
 * [Comparison table for persistent storage options](/docs/containers?topic=containers-storage-plan)
 * [Main IBM Cephaas page](/docs/sdsaas?topic=sdsaas-getting-started)
 * [Installing IBM Cephaas]
 * [Creating IBM Cephaas service instance]
 * [Decide on the configuration](/docs/containers?topic=containers-storage_cos_install#configure_cos)
 * [Creating an IBM Cephaas Kubernetes secret]
 * [Kubernetes back up and restore information](/docs/containers?topic=containers-storage_br)
 * [Kubernetes Storage Class reference](/docs/containers?topic=containers-storage_cos_reference)
