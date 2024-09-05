---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-05"

keywords: cephaas, create service instance, create deployment

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}


# Deployments
{: #deployments}

{{site.data.keyword.cephaas_full_notm}} is represented in IBM cloud as a billable resource entity referred to as deployments or service instance. The {{site.data.keyword.cephaas_short}} deployment lifecycle is handled by Resource Controller using provision through model.

IBM cloud resources are self-served such that you can manage the resources using CRUD operations through IBM cloud. But given the on-prem nature of {{site.data.keyword.cephaas_short}}, complete self serve of deployments is not possible since offline steps are involved. Hence you can only create deployments while the rest of the lifecycle operations are expected to be done offline except for quota settings that can be done through an update operation.


## Creating deployments
{: #provision-deployment}

You can create a deployment (also called as service instance) by resource controller through the custom catalogue UI, RC CLIs and API.

The Resource Controller (RC) API and CLI allows you to set and manage the service specific attributes using the '–parameters' flag for inputs which is a volatile attribute.

You must have 'Administrator' and 'Editor' role to create the service instance.
{: note}

### Creating deployments using CLI
{: #creating-deployment-cli}
{: cli}




### Creating deployments with the API
{: #creating-deployment-api}
{: api}


To create a deployment, you need the bearer token of the user-id used.

Use a hostless or full satellite location as Location for the deployment.
{: prereq}

```sh
curl -X POST $rc_endpoint/v2/resource_instances -H "Authorization: $token" -H 'Content-Type: application/json' -d '{
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
