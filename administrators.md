---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-05"

keywords: cephaas, administrator, object storage, access, iam, create service instance, deployment

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# For administrators
{: #administrators}

Storage and system administrators familiar with {{site.data.keyword.cephaas_full}} can easily manage users, create API keys, and grant roles to users and services.
{: shortdesc}

## Setting up your storage
{: #administrators-setup}

First, you need to have at least one {{site.data.keyword.cephaas_full_notm}} resource instance, and some volumes to store the data in. How do you want to segment access to your data? Where do you want your data to physically reside? How often is the data accessed?

For more information, see [IAM overview](/docs/cephaas?topic=cephaas-iam-overview).

### Managing access
{: #administrators-manage-access}

The _service credential_ is a collection of important information that is needed to connect to a deployment of {{site.data.keyword.cephaas_full}}. It gives a user an identifier for the deployment of {{site.data.keyword.cephaas_full_notm}} (that is, the Resource Instance ID), service and authorization endpoints, and a means of associating the subject with an API key (that is, Service ID).

The `Manager` role allows users to perform all service level actions based on the service role assigned. This role allows you to manage all aspects of data storage such as create, update, delete and view operations for volumes, hosts and object service credentials. This role **does not allow** users to modify the deployments.

The `Administrator` role allows for the user to see that the deployment exists, and to view existing credentials, and modify the deployments. When the credentials are created, they are associated with a service ID. This service ID would need to have the `Manager` role on the deployment to be able to create and delete volumes and hosts.

For more information on IAM roles and permissions, see [the {{site.data.keyword.cloud_notm}} IAM overview](/docs/cephaas?topic=cephaas-iam-overview).


## Creating deployments
{: #provision-deployment}

You can create a deployment (also called as service instance) through the UI, or by using resource controller (RC) CLI, and API.

With the Resource controller (RC) API and CLI, you can set and manage the service-specific attributes by using the '–parameters' flag for inputs, which is a volatile attribute.

You must have an 'Administrator', 'Operator' and 'Editor' role to create the deployment.
{: note}

To create a deployment, you must have the `Subscription Plan ID`, `Satallite CRN` and `Order ID` handy. You can get the Plan ID from the [Global Catalog](https://globalcatalog.cloud.ibm.com/). To locate your satallite CRN, click on the **hamburger menu > Resource list > satallite location**.
{: requirement}


### Creating deployments by using UI
{: #creating-deplyment-ui}
{: ui}

You can start creating a deployment after cost estimation and the order processing is initiated.


1. Open the order status email from your IBM sales partner and click on the link **Prepare deployment**. The link opens the deployment dashboard which lists your in-progress or completed orders.
2. On the **Prepare deployment** screen, select your **IBM Cloud Satellite location** and **Resource group**.
3. Enter your **Deployment name**.
4. Click **Create**.
5. Your **Deployment Preparation** status will be reflected as **Completed**.
6. After the on-premise hardware setup is done, the deployment will be reflected as **Available** and ready-to-be provisioned.



### Creating deployments by using CLI
{: #creating-deployment-cli}
{: cli}


1. First, make sure that you have an API key. Get it from [IBM Cloud Identity and Access Management](https://cloud.ibm.com/iam/apikeys).

2. Log in to {{site.data.keyword.cloud_notm}} Platform by using the CLI. It's also possible to store the API key in a file or set it as an environment variable.

    ```sh
    ibmcloud login --apikey <value>
    ```
    {: pre}

3. Next, create an {{site.data.keyword.cephaas_full_notm}} deployment by specifying the name for the deployment, the Subscription plan and satallite details. Now you have a CRN for the instance.

    ```sh
    ibmcloud resource service-instance-create <name> software-defined-storage <plan id> <catalog satellite location> -p '{"satellite_crn": <satellite_location_crn>, "order_id": <order_id>}' -g <resource_group_name>
    ```
    {: pre}

    See example.

    ```sh
    $ ibmcloud resource service-instance-create service-instance-cli software-defined-storage 38bacce6d-9644-4b88-8v40-f5e44e6c75c5 satloc_dal_cqsuoub20mq4s939tq20 -p '{"satellite_crn"}: "crn:v1:staging:public:satellite:us-south:a/3faf73b8d12b47fa6ce87494f8ae7686:cqsuoub20mq4s939tq20::","order_id":"account-1"}' -g resource-group-1
    Creating service instance service-instance-cli in resource group resource-group-1 of account account-1 as user@company.com...
    OK
    Service instance service-instance-cli  was created.

    Name:             service-instance-cli
    ID:               crn:v1:staging:public:software-defined-storage:satloc_dal_cqsuoub20mq4s939tq20:a/3faf73b8d12b47fa6ce87494f8ae7686:421e79b8-aa9f-4d69-bc57-4a9d5955e1a6::
    GUID:             421e79b8-aa9f-4d69-bc57-4a9d5955e1a6
    Location:         satloc_dal_cqsuoub20mq4s939tq20
    State:            provisioning
    Type:             service_instance
    Sub Type:
    Allow Cleanup:    false
    Locked:           false
    Created at:       2024-08-23T07:38:11Z
    Updated at:       2024-08-23T07:38:12Z
    ```
    {: screen}


    During instance creation, the status shows as provisioning state. Wait until the status changes to Active state to start using the volume and host operations.
    {: note}


When creating a new instance, if you encounter the error `No resource group targeted`, it indicates that the default resource group is not available and that a resource group must be explicitly set. A list of available resource groups can be found by using `ibmcloud resource groups` and the target can be set with `ibmcloud target -g <resource-group>`.
{: tip}


### Creating deployments with the API
{: #creating-deployment-api}
{: api}


To create a deployment, you need the bearer token of the user-id used.

Use a hostless or full satellite location as Location for the deployment.
{: prereq}

```sh
curl -X POST $rc_endpoint/v2/resource_instances -H "Authorization: Bearer $token" -H 'Content-Type: application/json' -d '{
        "name": "sds-unified-1",
        "target": "us-south",
        "resource_group": "8c3bdd054c7b459b8ddb327d1609b2f4",
        "resource_plan_id": "38bace6d-9644-4b88-8c40-f5e44e6c75c5",
        "parameters": {
            "committed_capacity":"100",
            "tenure":"5",
            "storage_type": "unified"
       }
  }' |jq
```
{: pre}

A successful response looks like this:

```json
{
  "_id": "66248c60-4350-11ee-93ea-093eed40336e",
  "_rev": "1-e8e76187cd43545726005411b3a22811",
  "committedCapacity": 600,
  "createdByIAMID": "IBMid-663003U96I",
  "creationDate": "2024-04-15T08:48:24.324507588Z",
  "crn": "crn:v1:staging:public:sds-samriddhi:global:a/f85ab2d7af0c43edbdf7d47241a9494f:66248c60-4350-11ee-93ea-093eed40336e::",
  "planID": "1b7afb92-91be-4a19-8647-f5a1f57b6d4b",
  "region": "global",
  "serviceInstanceID": "66248c60-4350-11ee-93ea-093eed40336e",
  "storageType": "unified",
  "tenantID": "298f2202abc54fd3ad26602c396106a4",
  "tenure": 5
  "burstCapacity: 180,
  "allocatedBurstCapacity: 0,
  "quota.block": 300,
  "quota.object: 300,
  "satellite_crn": "crn:v1:staging:public:satellite:us-south:a/3faf73b8d12b47fa6ce87494f8ae7686:coss5vm20tfjc8f72430::"
  "order_id": "BSS_123456789",
  "state": "provisioning"
}
```
{: screen}
