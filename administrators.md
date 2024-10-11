---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-11"

keywords: cephaas, administrator, object storage, access, iam

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# For administrators
{: #administrators}

Storage and system administrators familiar with {{site.data.keyword.cephaas_full}} can easily manage users, create API keys, and grant roles to users and services.
{: shortdesc}

If you haven't already, go ahead and read through the [getting started tutorial](/docs/sdsaas?topic=sdsaas-getting-started) to familiarize yourself with the core concepts of buckets, objects, and users.

## Setting up your storage
{: #administrators-setup}

First, you need to have at least one {{site.data.keyword.cephaas_full_notm}} resource instance, and some volumes to store the data in. How do you want to segment access to your data? Where do you want your data to physically reside? How often will the data be accessed?

### Segmenting access
{: #administrators-access}

You can segment access at two levels: at the resource instance level and at the bucket level.

Perhaps you want to make sure that your developers can only access a particular storage volume. Or, if you want to ensure that only the application your team is making can edit the data that is stored. You might want your developers with access to the cloud platform to only be able to read data for troubleshooting reasons, but not change anything. These are examples of service-level policies.

Now what if the development team, or any individual user, who has viewer access to a storage instance, but should be able to directly edit data in one or more buckets? You can use bucket level policies to elevate the level of access that is granted to users within your account. For instance, a user might not be able to create new buckets, but can create and delete objects within existing buckets.

## Managing access
{: #administrators-manage-access}

IAM is based on a fundamental concept: A _subject_ is granted a _role_ on a _resource_.

There are two basic types of subjects: a _user_ and a _service ID_.

There is another concept, a _service credential_. A service credential is a collection of important information that is needed to connect to a deployment of {{site.data.keyword.cephaas_full}}. It gives a user an identifier for the deployment of {{site.data.keyword.cephaas_full_notm}} (that is, the Resource Instance ID), service and authorization endpoints, and a means of associating the subject with an API key (that is, Service ID). When you create the service credential you have the option of either associating it with an existing service ID, or creating a new service ID.

You might want your development team to be able to use the console to view Object Storage instances and Kubernetes clusters. They would need `Viewer` roles on the Object Storage resources and `Administrator` roles on the Container Service. The `Viewer` role allows for the user to see that the deployment exists, and to view existing credentials, but **not** to modify the deployments. When the credentials are created, they are associated with a service ID. This service ID would need to have the `Operator` or `Editor` role on the deployment to be able to create and delete volumes and hosts.

For more information on IAM roles and permissions, see [the {{site.data.keyword.cloud_notm}} IAM overview](/docs/sdsaas?topic=sdsaas-iam-overview).




## Create an {{site.data.keyword.cephaas_full_notm}} deployment
{: #gs-dev-provision}

1. First, make sure that you have an API key. Get it from [IBM Cloud Identity and Access Management](https://cloud.ibm.com/iam/apikeys).

2. Log in to {{site.data.keyword.cloud_notm}} Platform by using the CLI. It's also possible to store the API key in a file or set it as an environment variable.

    ```sh
    ibmcloud login --apikey <value>
    ```
    {: pre}

3. Next, create an {{site.data.keyword.cephaas_full_notm}} deployment by specifying the name for the deployment and the Subscription plan. Now you have a CRN for the instance.

    ```sh
    ibmcloud resource service-instance-create <instance-name> software-defined-storage <plan> global
    ```
    {: pre}

When trying to create a new instance, if you encounter the error `No resource group targeted`, it indicates that the default resource group is not available and that a resource group must be explicitly set. A list of available resource groups can be found using `ibmcloud resource groups` and the target can be set with `ibmcloud target -g <resource-group>`.
{: tip}

The [Getting Started guide](/docs/sdsaas?topic=sdsaas-getting-started) walks through the basic steps of creating deployment instances, volumes and objects, as well as inviting users and creating policies. A list of basic 'curl' commands can be found [here](/docs/sdsaas?topic=sdsaas-curl).

Learn more about using the {{site.data.keyword.cloud_notm}} CLI to create applications, manage Kubernetes clusters, and more [in the documentation](/docs/cli?topic=cli-ibmcloud_cli).
