---

copyright:
 years: 2024, 2025
lastupdated: "2025-06-09"

keywords: cephaas, deleting single snapshot, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


## Deleting a single snapshot through the API
{: #delete-snapshot-api}
{: api}

Make a `DELETE /snapshots/{id}` request to delete a snapshot. 

The delete operation cannot be reversed. 
{: Warning}

```sh
curl -X DELETE $sds_endpoint/snapshots/${id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

There is no response body for a successful delete operation.

To verify that the snapshot is deleted, list the snapshots by making a `GET /snapshots` request.


