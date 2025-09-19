---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas, deleting single snapshot, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Delete a single snapshot
{: #delete-single-snapshot}

You can delete a single snapshot of a volume through API and CLI.

## Deleting a single snapshot in the API
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

## Deleting a single snapshot from the CLI
{: #delete-single-snapshot-cli}
{: cli}

To delete a single snapshot, run the following command.

```sh
ibmcloud sds volume-snapshot-delete --snap-id <snap-id> --force
```
{: pre}

`--snap-id <snap-id>` is required. `--force` is optional.

See the following example.

```bash
ic sds volume-snapshot-delete --snap-id r134-9ede0937-511c-422e-b8e5-b65bb49ed1fd
Are you sure you want to delete? [y/n]> y
...
OK
```
{: screen}
