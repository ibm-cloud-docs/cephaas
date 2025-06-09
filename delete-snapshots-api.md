---

copyright:
 years: 2024, 2025
lastupdated: "2025-06-09"

keywords: cephaas, delete snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


## Deleting a collection of snapshots through the API
{: #delete-filtered-snapshots-api}
{: api}

Make a `DELETE /snapshots` request to delete snapshots that match the specified filter such as all the snapshot of particular volume. 

```sh
curl -X DELETE $sds_endpoint/snapshots/${id}\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

There is no response body for a successful delete operation.

To verify that the snapshot is deleted, list the snapshots by making a `GET /snapshots` request.
