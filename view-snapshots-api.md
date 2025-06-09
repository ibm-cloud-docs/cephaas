---

copyright:
 years: 2025, 2025
lastupdated: "2025-06-09"

keywords: cephaas, view existing snapshots with API, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}



## Viewing existing snapshots with the API
{: #listing-snapshots-api}
{: api}

You can view the existing snapshots by calling the Snapshots API.

Make a `GET /snapshots` request to view the existing snapshot. 

```sh
curl -X GET $sds_endpoint/snapshots\
   -H "accept: application/json"\
   -H "Authorization: Bearer $IAM_TOKEN"\
   -H "IBM-API-Version: 2025-02-01"\
   --data '{
  "name": "my-snapshot",
  "source_volume": {
    "id": "r006-1a6b7274-678d-4dfb-8981-c71dd9d4daa5"
  }
}'
```
{: pre}

A successful response looks like this. 

```json

{
  "snapshots": [
    {
      "lifecycle_state": "stable",
      "size": 30,
      "minimum_capacity": 30,
      "name": "my-snapshot",
      "resource_type": "resource_type",
      "deletable": true,
      "created_at": "2000-01-23T04:56:07.000+00:00",
      "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5",
      "source_volume": {
        "name": "my-resource",
        "resource_type": "resource_type",
        "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5"
      }
    },
    {
      "lifecycle_state": "stable",
      "size": 30,
      "minimum_capacity": 30,
      "name": "my-snapshot",
      "resource_type": "resource_type",
      "deletable": true,
      "created_at": "2000-01-23T04:56:07.000+00:00",
      "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5",
      "source_volume": {
        "name": "my-resource",
        "resource_type": "resource_type",
        "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5"
      }
    },
    {
      "lifecycle_state": "stable",
      "size": 30,
      "minimum_capacity": 30,
      "name": "my-snapshot",
      "resource_type": "resource_type",
      "deletable": true,
      "created_at": "2000-01-23T04:56:07.000+00:00",
      "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5",
      "source_volume": {
        "name": "my-resource",
        "resource_type": "resource_type",
        "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5"
      }
    },
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
        "id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5"
      }
    }
  ],
  "next": {
    "href": "http://example.com/aeiou"
  },
  "total_count": 20,
  "limit": 20,
}
```
{: pre}

