---

copyright:
 years: 2024, 2025
lastupdated: "2025-02-13"

keywords: sds, host, view host details, host summary list

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# View host mapping details
{: #view-host-mapping-details}

View details of a host or summary information about all host mappings for the chosen deployment.
{: shortdesc}



## Viewing host mapping details from the CLI
{: #viewing-host-mapping-cli}
{: cli}

View details of a single volume mapping or summary information about all host mappings from the CLI.


### Viewing details of a single volume mapping from the CLI
{: #view-single-host-detail-cli}

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
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstm` as an alternative to `host-mapping` for the CLI actions.
{: tip}



### View a list of all volume mapping for a host from the CLI
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
{: note}

You can also use the alias `sds` as an alternative to `software-defined-storage` and `hstms` as an alternative to `host-mappings` for the CLI actions.
{: tip}

For more information about available command options, run `ibmcloud sds hosts --help`.


## View all hosts with the API
{: #viewing-hosts-api}
{: api}

You can list all hosts and view details for a specific host within all deployments that you have access to.

Before you begin, make sure that you [set up your API environment](/docs/cephaas?topic=cephaas-set-up-environment&interface=api).

### View a list of all volume mappings for a host with the API
{: #view-all-host-mappings-api}
{: api}

Make a `GET /hosts` call to list all volume mappings for a host. See the following example.

```sh
curl -X 'GET' '$sds_api_endpoint/v1/hosts/{id}/volume_mappings -H 'accept: application/json'
```
{: pre}

A successful response looks like the following example.

```json
**Example needed**
```

### Viewing details of a single volume mapping for a host with the API
{: #view-single-host-details-api}
{: api}

Make a `GET /hosts/{id}/volume_mappings/{volume_mapping_id}` call to see details of a single volume mapping for a host. See the following example.

```sh
curl -X 'GET' '$sds_api_endpoint/v1/hosts/r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921/volume_mappings/{volume_mapping_id}' -H 'accept: application/json'
```
{: pre}

A successful response provides details of the host, such as the `host ID`, `host name`, `nqn`, `service instance ID` and also includes mapped volume details if it mapped to a volume.

```json

**Example needed**
```
{: codeblock}
