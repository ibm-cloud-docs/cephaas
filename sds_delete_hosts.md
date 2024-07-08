---

copyright:
 years: 2024, 2024
lastupdated: "2024-07-08"

keywords: sds, sdsaas host delete, delete all host volume mapping, delete volume mapping for a host,

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Deleting hosts
{: #deleting-sds-hosts}

Delete a host from a service instance by using the UI, CLI, or API.
{: shortdesc}


## Deleting host from the UI
{: #deleting-sds-block-volume-ui}
{: ui}

To delete a host, complete the following steps.

1. On the IBM Cloud console, navigate to **SDS as a Service > Block Storage > Hosts**.

2. Locate the Host **Name** that you want to delete and then click the **Options** menu at the end of the row to open a list of options.

3. From the options menu, click **Delete**.

4. Confirm the deletion.


## Deleting host from the CLI
{: #deleting-sds-hosts-cli}
{: cli}

Use the `host-delete` command and specify the `INSTANCEID` to delete the host based on the instance id.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage host-delete --host-id HOST-ID --instanceid INSTANCEID
```
{: pre}

See the following example.

```bash
  ibmcloud software-defined-storage host-delete \
    --host-id exampleString \
    --instanceid exampleString
```
{: screen}


## Deleting a single volume mapping for a host from the CLI
{: #deleting-sds-single-volume-mapping-hosts-cli}
{: cli}

Use the `host-volid-delete` command and specify the `HOST-ID`, `INSTANCEID` and `VOLUME-ID` to delete a particular volume mapped from the host.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage host-volid-delete --host-id HOST-ID --volume-id VOLUME-ID --instanceid INSTANCEID
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-volid-delete \
  --host-id exampleString \
  --volume-id exampleString \
  --instanceid exampleString
```
{: screen}


## Deleting all volume mapping for a host from the CLI
{: #deleting-sds-all-volume-mapping-hosts-cli}
{: cli}

Use the `host-vol-deleteall` command and specify the `HOST-ID` and `INSTANCEID` to delete all volumes associated with the given host id based on the instance id.

Run the following command to delete a volume.

```sh
ibmcloud software-defined-storage host-vol-deleteall --host-id HOST-ID --instanceid INSTANCEID
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage host-vol-deleteall \
  --host-id exampleString \
  --instanceid exampleString
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



## Sanitizing your data before you delete a volume
{: #sanitizing-your-data-before-you-delete-a-volume}

When you delete a Block Storage volume, IBM guarantees that your data is inaccessible on the physical disk and is eventually eradicated. If you have extra compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see the [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final).

Sanitizing and deleting the volume means your data can't be restored.



## Next steps
{: #next-step-deleting-hosts-sds}


