---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-28"

keywords: sds, host, view host details, host summary list

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# View host mapping details
{: #view-host-mapping-details}

View details of a single host mapping to a one or more volumes or view a list of all host mappings for the deployment.
{: shortdesc}

Before you begin, make sure that you have [set up your CLI and API environment](/docs/cephaas?topic=cephaas-set-up-environment).
{: requirement}


## View all mapped volumes to a host in the UI
{: #view-all-mapped-vols-host-ui}
{: ui}

To view all mapped hosts to a volume, in the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), go to  **{{site.data.keyword.cephaas_full_notm}} > Block Storage > Hosts** and click on the single host name link.

All mapped volumes are displayed for the chosen host on the Mapped volume section of Host details page. In the list, you can see the following information.

| Field               | Description |
|---------------------|-------------|
| Name                | Volume name.                                             |
| Mapped status       | Shows the status of the volume that is mapped to the host. |
| Storage identifier  | Storage identification number.                             |
| Gateway IP          | IP address.                                              |
| Namespace ID        | Namespace identification number.                         |
| Namespace UUID      | Universal unique identification number of the namespace. |
{: caption="Details of all mapped volumes to a host." caption-side="bottom"}

By default, 10 hosts are shown from the list of all hosts. Change this default by clicking the Page Control down arrow and increase the list to 25, 50 or 100 hosts. Use the Page Control arrows after the list to go to the following page or return to the current page.

The row actions menu on the Hosts list page provides you with options to manage the single host information.

Table describes the kebab menu options.

| Action             | Description |
|--------------------|-------------|
| Unmap             | Remove the mapping between the volume and host. |
{: caption="Row actions menu options for mapped volumes to a host." caption-side="bottom"}




## View a list of all volume mapping for a host from the CLI
{: #view-all-host-mappings-cli}
{: cli}

Run this command to view the list of all volume mappings for a host.

```sh
ibmcloud software-defined-storage host-mappings --host-id HOST-ID --url string
```
{: pre}


The following example shows all volumes mapped to a host in your deployment.

```sh
ibmcloud software-defined-storage host-mappings \
  --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
  --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstms` as an alternative to `host-mappings` for the CLI actions.
{: tip}


## Viewing details of a single volume to a host mapping from the CLI
{: #view-single-host-mapping-detail-cli}
{: cli}

Run the following command to show volume mapping details for a specific `HOST-ID` and `VOLUME_MAPPING_ID`.

```sh
ibmcloud software-defined-storage host-mapping --host-id HOST-ID --volume-mapping-id VOLUME-MAPPING-ID --url string
```
{: pre}


The following example uses the host ID to show host details.

```sh
$ ibmcloud software-defined-storage host-mapping \
  --host-id r134-69d5c3e2-8229-45f1-89c8-e4dXXb2e126e \
  --volume-mapping-id r134-f24710c4-d5f4-4881-ab78-7bfXX6281f39 \
  --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstm` as an alternative to `host-mapping` for the CLI actions.
{: tip}



For more information about available command options, run `ibmcloud sds hosts --help`.


## View a list of all volume mappings for a host with the API
{: #view-all-host-mappings-api}
{: api}

Make a `GET /hosts` request to list all volume mappings for a host.

See the following example.

```sh
curl -X GET $sds_endpoint/hosts/{id}/volume_mappings\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response displays a list all the volume mapping for the host.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


## View details of a single volume mapping for a host with the API
{: #view-single-host-mapping-details-api}
{: api}

Make a `GET /hosts/{id}/volume_mappings/{volume_mapping_id}` request to see details of a single volume mapping for a host. See the following example.

```sh
curl -X GET $sds_endpoint/hosts/r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921/volume_mappings/{volume_mapping_id} \
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H 'IBM-API-Version: 2025-02-01'
```
{: pre}

A successful response provides details of the host, such as the `host ID`, `host name`, `nqn`, `service instance ID` and also includes mapped volume details if it mapped to a volume.

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_short}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).
