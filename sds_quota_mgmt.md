---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-01"

keywords:

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}


# Block quota and capacity management
{: #sds-quota-capacity-mgmt}

CephaaS supports service instance level quotas for both the unified (block & object )and low cost object storage plans. The block and object level quota allocation depends on the committed capacity along with the user opted max burst capacity usage limit. Object storage quota can be set by allocating the quota value to the default STANDARD for the unified storage plan and the default storage class STANDARD-IA for the low cost object storage plan.

Since the provisioned capacity and quota is at service instance level setting, the quota can be set for block storage pool as well as object storage pool.

## Managing quota from the UI
{: #managing-sds-block-quota-ui}


1. On the IBM web conole, go to **Settings** and select the **Deployment** whose quota you want to manage.
2. Click **Edit preferences**.
3. Review the capacity limit. Select **Include burst capacity** if you want to expand your total available capacity.

    Including burst capacity may incur overage fees for the amount of burst capacity userd.
    {: note}

4. Click **Next** and review the storage capacity allocations.
5. Use the **+** & **-** controls to increase the allocated capacity.

    The allocated capacity cannot be reduced or set below the current amount of used or provisionied capacity.
    {: note}

6. Click **Save** to set the new storage capacity allocations.


## Managing block quota with the API
{: #managing-sds-block-quota-api}


### Get total provisioned capacity
{: #sds-get-total-providioned-capacity}

Make a `GET /internal/v1/block/total_provisioned` request to get the total provisioned capacity for block volumes.

A successful response looks like this:

```json
{

    "total_provisioned_bytes": 200000,  // provisioned capacity in bytes

    "total_provisioned_count": 35,  // number of provisioned volumes

    "service_instance_id": "xxxx" // a valid service instance ID

}
```


### Set block quota
{:# sds-set-block-quota}

Make a `PUT /internal/v1/block_quota` request to set the block quota for a given deployment (service instance).

Request Body:

{

    "quota": 50  // quota in TB
}

A successful response looks like this:

```json
{

    "quota": 50,  // quota in TB
    "service_instance_id": "xxxx" // a valid service instance ID

}
```


HTTP Response Codes:

200: Request was successful


### Get block quota
{: #sds-get-block-quota}

Make a `GET /internal/v1/block_quota` request to get the block quota details of a deployment (Service instance)

Request Body: None

Response:

{

    "quota": 200000,  // quota in TB

    "service_instance_id": "xxxx" // a valid service instance ID

}
