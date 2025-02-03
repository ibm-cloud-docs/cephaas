---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-03"

keywords: sds, cephaas host unmap, delete all host volume mapping, delete volume mapping for a host,

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Unmap volume from a host
{: #unmap-hosts}

Unmap one or more volumes from host by using the UI, CLI, API or Terraform.
{: shortdesc}


## Unmap volume from a host from the UI
{: #unmap-volume-from-host-ui}
{: ui}

To remove all mapping of a volume that is mapped to a host, complete the following steps.

1. Log in to the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage) and go to **Block storage > Hosts**.

2. Click the Host **Name** from which you want to unmap the volume.

3. On the Host details page, in the Mapped volumes list, locate the volume **Name** and click the kebab menu at the end of the row.

4. Click **Unmap**. A confirmation popup is displayed.

5. Click **Unmap** to confirm the unmapping of the selected volume from the host.


You can also unmap the host from a volume from **Volume details** page.
{: tip}




## Unmap a single volume for a host from the CLI
{: #unmap-single-volume-for-hosts-cli}
{: cli}

Use the `host-vol-delete` command and specify the `HOST-ID` along with the endpoint url and the volume ID that is associated with the host to unmap it.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.{uuid}.software-defined-storage.appdomain.cloud:{port number}/v1`.
{: note}

Run the following command to delete a single volume mapping from a host.

```sh
ibmcloud software-defined-storage host-vol-delete --host-id HOST-ID --volume-id VOLUME-ID --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage host-vol-delete \
  --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
  --volume-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
  --url exampleString
```
{: screen}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstvd` as an alternative to `host-vol-deleteall` for the CLI actions.
{: tip}


## Unmap all volumes for a host from the CLI
{: #unmap-all-volume-for-hosts-cli}
{: cli}

Use the `host-vol-deleteall` command and specify the `HOST-ID` along with the endpoint url to unmap all volumes that are associated with the host.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.{uuid}.software-defined-storage.appdomain.cloud:{port number}/v1`.
{: note}

Run the following command to delete all volume mappings from a host.

```sh
ibmcloud software-defined-storage host-vol-deleteall --host-id HOST-ID --url string
```
{: pre}

See the following example.

```sh
ibmcloud software-defined-storage host-vol-deleteall \
  --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
  --url exampleString
```
{: screen}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstvda` as an alternative to `host-vol-deleteall` for the CLI actions.
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

## Unmapping a volume for a host using Terraform
{: #unmap-volume-host-tf}
{: terraform}

To unmap a volume for a host, use the CLI terminal and run the following commands. Currently terraform does not support unmapping of hosts.

* To delete a single host mapping

```sh
ibmcloud sds host-vol-delete --host-id <HOST-ID> --volume-id <VOLUME-ID>
```
{: pre}

* To delete all host mappings

```sh
ibmcloud sds host-vol-deleteall --host-id <HOST-ID>
```
{: pre}
