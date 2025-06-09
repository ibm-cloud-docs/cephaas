---

copyright:
 years: 2024, 2025
lastupdated: "2025-06-09"

keywords: cephaas, updating snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


## Updating a snapshot through the API
{: #update-snapshot-api}
{: api}

Make a `PATCH /snapshots/{id}` request to update a snapshot. This request updates a snapshot with the information in a provided snapshot patch. 

You can update only the name of a snapshot. 
{: Note}

```sh
curl -X PATCH $sds_endpoint/snapshots/${id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
   --data'{
   "name": "snapshot-2025-05-13"
}'
```
{: pre}

A successful response looks like this:

```json
{
  "lifecycle_state": "stable",
  "size": 30,
  "minimum_capacity": 30,
  "name": "my-resource",
  "resource_type": "resource_type",
  "deletable": true,
  "created_at": "2000-01-23T04:56:07.000+00:00",
  "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5",
  "href": "http://example.com/aeiou",
  "source_volume": {
    "name": "my-resource",
    "resource_type": "resource_type",
    "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5",
    "href": "http://example.com/aeiou"
  }
}
```
{: screen}

