---

copyright:
 years: 2024, 2025
lastupdated: "2025-06-09"

keywords: cephaas, view specific snapshot with API, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


## Viewing a specific snapshot through the API
{: #retrieve-snapshots-api}
{: api}

Make a `GET /snapshots/{id}` request to retrieve a single snapshot specified by the identifier in the URL.

```sh
curl -X GET $sds_endpoint/snapshots/${id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
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

