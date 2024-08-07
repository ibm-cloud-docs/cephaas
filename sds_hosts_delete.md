---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-07"

keywords: sds, sdsaas host delete, delete all host volume mapping, delete volume mapping for a host,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting hosts
{: #deleting-sds-hosts}

Delete a host from a service instance by using the UI, CLI, or API.
{: shortdesc}


## Deleting host from the UI
{: #deleting-sds-single-host-ui}
{: ui}

To delete a host, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

2. Locate the Host **Name** that you want to delete and then click the **Options** menu at the end of the row to open a list of options.

3. From the options menu, click **Delete**.


## Deleting multiple host from the UI
{: #deleting-sds-multiple-hosts-ui}
{: ui}

To delete a host, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

2. Select one or more Host **Name** that you want to delete

3. Click **Delete**.



## Deleting volume mapping from a host from the UI
{: #deleting-sds-volume-mapping-from-host-ui}
{: ui}

To delete all volumes that are mapped to a host, complete the following steps.

1. On the IBM Cloud console, go to **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts**.

2. Click the Host **Name** from which you want to delete the mapped volume.

3. From the Mapped volumes list, locate the volume **Name** and click the **Options** menu at the end of the row.

4. Click **Unmap**. Confirmation popup is displayed.

5. Click **Unmap** to confirm the unmapping of selected volume from the host.


## Deleting host from the CLI
{: #deleting-sds-hosts-cli}
{: cli}

Use the `host-delete` command and specify the `INSTANCEID` and endpoint url along with the `HOST-ID` to delete the host based on the host id.

Run the following command to delete a host.

```sh
ibmcloud software-defined-storage host-delete --host-id HOST-ID --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
  ibmcloud software-defined-storage host-delete \
    --host-id exampleString \
    --instanceid exampleString \
    --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}


## Deleting a single volume mapping for a host from the CLI
{: #deleting-sds-single-volume-mapping-hosts-cli}
{: cli}

Use the `host-volid-delete` command and specify the `HOST-ID`, `INSTANCEID`, `VOLUME-ID` and `$sds_endpoint` to delete a particular volume mapped from the host.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage host-volid-delete --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-volid-delete \
  --host-id exampleString \
  --volume-id exampleString \
  --instanceid exampleString
  --url $sds_endpoint
```
{: screen}


## Deleting all volume mapping for a host from the CLI
{: #deleting-sds-all-volume-mapping-hosts-cli}
{: cli}

Use the `host-vol-deleteall` command and specify the `HOST-ID` and `INSTANCEID` to delete all volumes associated with the given host id based on the instance id.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
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


## Deleting a host with the API
{: #deleting-sds-host-api}
{: api}

Make a `DELETE /hosts/{id}` request to delete a specific host.

```sh
curl -X DELETE '$sds_api_endpoint/v1/hosts/{id}' \
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

There is no response body for a successful delete operation. HTTP response code 204 is returned.

To verify that the host is deleted, list the hosts by making a `GET /hosts` call.

## Deleting a volume mapping for a host with the API
{: #deleting-sds-single-volume-mapping-host-api}
{: api}

Make a `DELETE /hosts/{id}/volumes/{vol_id}` request to delete a specific volume that is mapped to a given host.

```sh
curl -X DELETE '$sds_api_endpoint/v1/hosts/{id}/volumes{vol_id}' \
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

There is no response body for a successful delete operation. HTTP response code 204 is returned.


To verify that the volume mapping for a given host is deleted, list the host details by making a `GET /hosts/{id}` call.



## Deleting all volume mapping for a host with the API
{: #deleting-sds-all-volume-mapping-host-api}
{: api}

Make a `DELETE /hosts/{id}/volumes` request to delete all volumes mapped for a given host.

```sh
curl -X DELETE '$sds_api_endpoint/v1/hosts/{id}/volumes' \
--header 'Authorization: Bearer $IAM_TOKEN'
```
{: pre}

There is no response body for a successful delete operation. HTTP response code 204 is returned.


To verify that all volumes mappings for a given host is deleted, list the hosts by making a `GET /hosts/{id}` call.






