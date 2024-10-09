---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-09"

keywords: sds, cephaas host unmap, delete all host volume mapping, delete volume mapping for a host,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Unmap volume from a host
{: #unmap-hosts}

Unmap one or more volumes from host by using the UI, CLI, or API.
{: shortdesc}


## Unmap volume from a host from the UI
{: #unmap-volume-from-host-ui}
{: ui}

To remove all mapping of a volume that is mapped to a host, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

2. Click the Host **Name** from which you want to unmap the volume.

3. On the Host details page, in the Mapped volumes list, locate the volume **Name** and click the kebab menu at the end of the row.

4. Click **Unmap**. A confirmation popup is displayed.

5. Click **Unmap** to confirm the unmapping of the selected volume from the host.



## Unmap all volumes for a host from the CLI
{: #unmap-all-volume-for-hosts-cli}
{: cli}

Use the `host-vol-deleteall` command and specify the `HOST-ID` and `INSTANCEID` to unmap all volumes that are associated with the given host id based on the instance id.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, `https://{on-prem}.endpoint.com:{port number}/v1`.
{: note}

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage host-vol-deleteall --host-id HOST-ID --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-vol-deleteall \
  --host-id exampleString \
  --instanceid exampleString
  --url $sds_endpoint
```
{: screen}

You can also use the aliase `sds` an alternative to `software-defined-storage` for the CLI actions.
{: tip}

## Unmap a volume for a host with the API
{: #unmap-single-volume-for-host-api}
{: api}

Make a `DELETE /hosts/{id}/volumes/{vol_id}` request to delete a specific volume that is mapped to a host.

```sh
curl -X DELETE '$sds_api_endpoint/v1/hosts/{host-id}/volumes/{volume-id}'
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

The command unmaps a volume from a host.

There is no response that is returned if the request is successful. HTTP response code 204 is returned.


To verify that the volume mapping for a host is deleted, list the host details by making a `GET /hosts/{id}` call.



## Unmap all volumes for a host with the API
{: #unmap-all-volume-for-host-api}
{: api}

Make a `DELETE /hosts/{id}/volumes` request to delete all volumes that are mapped for a host.

```sh
curl -X DELETE '$sds_api_endpoint/v1/hosts/{host-id}/volumes'
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

The command unmaps all volumes from a host.
There is no response that is returned if the request is successful. HTTP response code 204 is returned.


To verify that all volumes mappings for a host are deleted, list the hosts by making a `GET /hosts/{id}` call.
