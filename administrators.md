---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-12"

keywords: cephaas, administrator, object storage, access, iam, create service instance, deployment, ceph as a service

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

For more information, see the [IAM overview](/docs/cephaas?topic=cephaas-iam-overview).

### Managing access
{: #administrators-manage-access}

The _service credential_ is a collection of important information that is needed to connect to a deployment of {{site.data.keyword.cephaas_full}}. It gives a user an identifier for the deployment of {{site.data.keyword.cephaas_full_notm}} (that is, the Resource Instance ID), service and authorization endpoints, and a means of associating the subject with an API key (that is, Service ID).

The **Manager** role allows users to perform all service level actions based on the service role assigned. This role allows you to manage all aspects of data storage such as create, update, delete and view operations for volumes, hosts and object service credentials. This role **does not allow** users to modify the deployments.

The **Administrator** role allows for the user to see that the deployment exists, and to view existing credentials, and modify the deployments. When the credentials are created, they are associated with a service ID. This service ID would need to have the **Manager** role on the deployment to be able to create and delete volumes and hosts.

For more information on IAM roles and permissions, see [the {{site.data.keyword.cloud_notm}} IAM overview](/docs/cephaas?topic=cephaas-iam-overview).


## Creating deployments
{: #provision-deployment}

You can create a deployment (also called as service instance) through the UI, or by using resource controller (RC) CLI, and API.

With the Resource controller (RC) API and CLI, you can set and manage the service-specific attributes by using the '–parameters' flag for inputs, which is a volatile attribute.

You must have an **Administrator**, **Operator** and **Editor** role to create the deployment.
{: note}

To create a deployment, you must have the **Subscription Plan ID**, **Satallite CRN** and **Order ID** handy. You can get the Plan ID from the [Global Catalog](https://globalcatalog.cloud.ibm.com/). To locate your Satellite CRN, click on the **hamburger menu > Resource list > Satellite location**.
{: requirement}


### Creating deployments by using UI
{: #creating-deplyment-ui}
{: ui}

You can start creating a deployment after cost estimation and the order processing is initiated.


1. Open the order status email from your IBM sales partner and click on the link **Prepare deployment**. After you log in, the link opens the deployment dashboard, which lists your in-progress or completed orders.

2. On the **Prepare deployment** screen, select your **IBM Cloud Satellite location** and **Resource group**.

    While creating the IBM Cloud Satellite location, you can choose Object storage standard plan. For more information, see [IBM Cloud Satellite](/docs/satellite?topic=satellite-locations).
    {: tip}

3. Enter your **Deployment name** and click **Create**.

    Your **Deployment Preparation** status will show as **Completed**.

    After the on-premise hardware setup is completed, the deployment shows **Available** status and ready-to-be provisioned.



### Creating deployments by using CLI
{: #creating-deployment-cli}
{: cli}


1. First, make sure that you have an API key. Get it from [IBM Cloud Identity and Access Management](https://cloud.ibm.com/iam/apikeys).

2. Log in to {{site.data.keyword.cloud_notm}} Platform by using the CLI. It's also possible to store the API key in a file or set it as an environment variable.

    ```sh
    ibmcloud login --apikey <value>
    ```
    {: pre}

3. Next, create an {{site.data.keyword.cephaas_full_notm}} deployment by specifying the name for the deployment, the Subscription plan and Satellite details. Now you have a CRN for the instance.

    ```sh
    ibmcloud resource service-instance-create <service_instance_name> software-defined-storage <plan_id> satloc_dal_<satellite_guid> -p '{"satellite_crn":"<"satellite_crn>,"order_id":"<order-id>}' -g Default
    ```
    {: pre}

    See example.

    ```sh
    $ iibmcloud resource service-instance-create abcd-51150B3JN0 software-defined-storage 94f887fd-e984-4298-8efa-6ae7d3adc9d6 satloc_dal_cuvckfu20ia0nl71ndgg -p '{"satellite_crn":"crn:v1:staging:public:satellite:us-south:a/0b7bd21d002841be9c6a1936412394dd:cuvckfu20ia0nl71ndgg::","order_id":"51150B3JN0"}' -g Default
    ...

    Creating service instance service-instance-cli in resource group resource-group-1 of account account-1 as user@company.com...
    OK
    Service instance service-instance-cli  was created.

    Name:                   abcd-51150B3JN0
    ID:                     crn:v1:staging:public:software-defined-storage:satloc_dal_cuvckfu20ia0nl71ndgg:a/0571b3a07aba4a7c8bb3ba1edaf93521:3764d865-75f6-4b8f-9c13-eeaf882b0705::
    GUID:                   3764d865-75f6-4b8f-9c13-eeaf882b0705
    Location:               satloc_dal_cuvckfu20ia0nl71ndgg
    Service Name:           software-defined-storage
    Service Plan Name:      capacity
    Resource Group Name:    Default
    State:                  provisioning
    Type:                   service_instance
    Sub Type:
    Locked:                 false
    One-time credentials:   false
    Created at:             2025-02-28T10:52:41Z
    Created by:             user@company.com
    Updated at:             2025-02-28T10:52:51Z
    Last Operation:
                            Status    create in progress
                            Message   Started create instance operation
    ```
    {: screen}


    During instance creation, the status shows as provisioning state. Wait until the status changes to Active state to start using the volume and host operations.
    {: note}


When creating a new instance, if you encounter the error `No resource group targeted`, it indicates that the default resource group is not available and that a resource group must be explicitly set. A list of available resource groups can be found by using `ibmcloud resource groups` and the target can be set with `ibmcloud target -g <resource-group>`.
{: tip}


### Creating deployments with the API
{: #creating-deployment-api}
{: api}


To create a deployment, you need the Bearer token of the user-id used.

Use a hostless or full satellite location as Location for the deployment.
{: prereq}

```sh
curl --location 'https://resource-controller.cloud.ibm.com/v2/resource_instances/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $IAM_TOKEN' \
--data '{
    "name": "test-maryam-27feb:2:29",
    "target": "satloc_dal_cspit2i20f0dosc3rn20",
    "resource_group": "e094c5810724956dc62890402dbbbe3d",
    "resource_plan_id": "34beb6d3-7afb-406c-9c75-6e2ab91e87ed",
    "parameters": {
        "satellite_crn" : "crn:v1:staging:public:satellite:us-south:a/3faf73b8d12b47fa6ce87494f8ae7686:cspit2i20f0dosc3rn20::",
        "order_id":"MVT-test-1"
    }
}'
```
{: pre}

A successful response looks like this:

```json
{
    "id": "crn:v1:staging:public:software-defined-storage:satloc_dal_cspit2i20f0dosc3rn20:a/3faf73b8d12b47fa6ce87494f8ae7686:a8d1c2c0-de91-4c59-a983-9866d8cd5b2a::",
    "guid": "a8d1c2c0-de91-4c59-a983-9866d8cd5b2a",
    "url": "/v2/resource_instances/a8d1c2c0-de91-4c59-a983-9866d8cd5b2a",
    "created_at": "2025-02-28T12:59:29.736799693Z",
    "updated_at": "2025-02-28T12:59:40.705078066Z",
    "deleted_at": null,
    "created_by": "IBMid-6960008R79",
    "updated_by": "",
    "deleted_by": "",
    "scheduled_reclaim_at": null,
    "restored_at": null,
    "scheduled_reclaim_by": "",
    "restored_by": "",
    "name": "test-sample-28feb:6:29",
    "region_id": "satloc_dal_cspit2i20f0dosc3rn20",
    "account_id": "3faf73b8d12b47fa6ce87494f8ae7686",
    "reseller_channel_id": "",
    "resource_plan_id": "34beb6d3-7afb-406c-9c75-6e2ab91e87ed",
    "resource_group_id": "e094c5810724956dc62890402dbbbe3d",
    "resource_group_crn": "crn:v1:staging:public:resource-controller::a/3faf73b8d12b47fa6ce87494f8ae7686::resource-group:e094c5810724956dc62890402dbbbe3d",
    "target_crn": "crn:v1:staging:public:globalcatalog::a/3faf73b8d12b47fa6ce87494f8ae7686::deployment:satdep_cspit2i20f0dosc3rn20_sattmpl_34beb6d3-7afb-406c-9c75-6e2ab91e87ed%3Asatcon_dal13892",
    "parameters": {
        "order_id": "MVT-test-1",
        "satellite_crn": "crn:v1:staging:public:satellite:us-south:a/3faf73b8d12b47fa6ce87494f8ae7686:cspit2i20f0dosc3rn20::"
    },
    "allow_cleanup": false,
    "crn": "crn:v1:staging:public:software-defined-storage:satloc_dal_cspit2i20f0dosc3rn20:a/3faf73b8d12b47fa6ce87494f8ae7686:a8d1c2c0-de91-4c59-a983-9866d8cd5b2a::",
    "state": "provisioning",
    "type": "service_instance",
    "resource_id": "2bea02b0-c0a4-11ee-83aa-3171b0bf2976",
    "dashboard_url": "https://cloud.ibm.com/software-defined-storage/crn:v1:staging:public:software-defined-storage:satloc_dal_cspit2i20f0dosc3rn20:a%2F3faf73b8d12b47fa6ce87494f8ae7686:a8d1c2c0-de91-4c59-a983-9866d8cd5b2a::",
    "last_operation": {
        "type": "create",
        "state": "in progress",
        "async": true,
        "description": "Started create instance operation",
        "cancelable": false,
        "poll": false
    },
    "resource_aliases_url": "/v2/resource_instances/a8d1c2c0-de91-4c59-a983-9866d8cd5b2a/resource_aliases",
    "resource_bindings_url": "/v2/resource_instances/a8d1c2c0-de91-4c59-a983-9866d8cd5b2a/resource_bindings",
    "resource_keys_url": "/v2/resource_instances/a8d1c2c0-de91-4c59-a983-9866d8cd5b2a/resource_keys",
    "plan_history": [
        {
            "resource_plan_id": "34beb6d3-7afb-406c-9c75-6e2ab91e87ed",
            "start_date": "2025-02-28T12:59:29.736799693Z",
            "requestor_id": "IBMid-6960008R79"
        }
    ],
    "migrated": false,
    "extensions": {
        "allocate_burst_capacity": true,
        "available_burst_capacity": 60,
        "committed_capacity": 200,
        "quota": {
            "block": 130,
            "object": 130
        },
        "storage_type": "unified",
        "tenure": 0
    },
    "controlled_by": "",
    "locked": false,
    "onetime_credentials": false
}

```
{: screen}

During deployment creation, the status shows as `provisioning` state. Wait until the status changes to `Active` state to start using the volume and host operations.
{: note}
