---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-07"

keywords: cephaas, delete snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Delete a collection of snapshots
{: #delete-collection-snapshots}

You can delete all the snapshots of a particulat block volume through API and CLI.

## Deleting a collection of snapshots in the API
{: #delete-filtered-snapshots-api}
{: api}

Make a `DELETE /snapshots` request to delete snapshots of particular volume.

```sh
curl -X DELETE $sds_endpoint/snapshots/$\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
  --data '{
    {"id": "r134-b274-678d-4dfb-8981-c71dd9d4daa5"}
  }'
```
{: pre}

There is no response body for a successful delete operation.

To verify that the snapshot is deleted, list the snapshots by making a `GET /snapshots` request.

## Deleting a collection of snapshots from the CLI
{: #delete-snapshots-from-from-cli}
{: cli}

To delete snapshots that match the specified filter such as all the snapshot of particular volume using the command-line interface (CLI), run the following command.

```sh
ibmcloud sds volume-snapshots-delete --source-volume-id SOURCE-VOLUME-ID --force
```
{: pre}

`--force` is optional.

See the following example.

```bash
ic sds volume-snapshots-delete --source-volume-id r134-76a4e08c-aa22-4fd3-9eb5-5cae0e78a285
Are you sure you want to delete? [y/n]> y
...
OK
```
{: screen}
