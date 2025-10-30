---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-30"

keywords: ceph as a service, sds, host, view host details, host summary list

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# View host details
{: #view-host-details}

View single host detail or a summary information about all hosts for the chosen deployment.
{: shortdesc}

## View all hosts in the UI
{: #view-all-hosts-ui}
{: ui}

To view a list of all hosts, in the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://{DomainName}/software-defined-storage), click **Deployments** > **Name** link and then click **Block Storage > Hosts**.

By default, all Hosts are displayed for the chosen Deployment. In the list of all **Hosts**, you can see the following information.

| Field           | Description |
|-----------------|-------------|
| Name            | Click the name of the host to see individual host details. |
| Volumes mapped  | Shows the count of the number of volumes that are mapped to the host. |
| Host NQN        | The NVMe Qualified Name (NQN) of the configured host. |
{: caption="Details about all hosts" caption-side="bottom"}

By default, 10 hosts are shown from the list of all hosts. Change this default by clicking the Page Control down arrow and increase the list to 25, 50 or 100 hosts. Use the Page Control arrows after the list to go to the following page or return to the current page.

The row actions menu on the Hosts list page provides you with options to manage the single host information.

Table describes the kebab menu options.

| Action             | Description |
|--------------------|-------------|
| View host details  | Click to open the detailed view of the host. |
| Rename host        | Click to change the host name. |
| Map volumes        | Click to map the host to a volume. |
| Delete             | Remove the mapping between the volume and host. |
{: caption="Row actions menu options for Hosts." caption-side="bottom"}

When you select one or more hosts, the **Delete** button is enabled and displayed which enables you to perform multiple delete operations.


## View single host details in the UI
{: #view-single-host-details-ui}
{: ui}

To view details of a single host, go to the list of all hosts and click the hostname link.

The Host details page shows the details of the chosen hostname and all its mapped volumes. The table describes this information.

| Field | Description |
|-------|-------------|
| **Host details** | |
| Name  | The name of the host you specified when you created the host. Click the pen icon to edit the host name. The name can be up to 63 lowercase alpha-numeric characters and include the hyphen (-), and must begin with a lowercase letter. The name must be unique for the deployments. |
| Host ID | Unique alphanumeric value to identify the host. |
| Host NQN | The NVMe Qualified Name (NQN) of the configured host |
| Volumes mapped | Shows the total number of volumes mapped to the host. |
| Created date | System-generated date when the host was added.|
| Deployment | Name of the instance |
| **Mapped volumes** | |
| Name                | Volume name.                                             |
| Mapped status       | Shows the status of the volume that is mapped to the host. |
| Storage identifier  | Storage identification number.                             |
| Gateway IP          | IP address.                                              |
| Namespace ID        | Namespace identification number.                         |
| Namespace UUID      | Universal unique identification number of the namespace. |
{: caption="Host details" caption-side="bottom"}

The Mapped volumes section shows the list of all the volumes that are mapped to the Host and a link to map volumes to the host.

The kebab menu has the option to unmap the attached volume from the host.



## View a list of all hosts from the CLI
{: #view-all-host-cli}
{: cli}

Run this command to view the list of summary information about all hosts.

```sh
ibmcloud software-defined-storage hosts [--limit LIMIT] [--name NAME] --url string
```
{: pre}


The following example shows all hosts in your availability zone.

```sh
ibmcloud software-defined-storage hosts --limit 10
...

Total_Count   4
Hosts
              Created_At        2025-02-27T11:15:42.000Z
              Host_ID           r134-9492bd82-f2db-4871-a85d-34321c695f26
              Host_NQN          nqn.2025-02.org.nvmeautomation:uuid:c34ed557-c1b1-4036-83aa-b8cbf3567b69
              Host_Name         automation-host-bg9qtv3d
              Volume_Mappings
                                Namespace_ID        3
                                Namespace_UUID      0d632e1ec03b5f139ff222a4494fe21d
                                Status              mapped
                                Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                                Volume_ID           r134-bad36c92-8cfc-4912-b6bc-e714460a9ef8
                                Volume_Mapping_ID   r134-c9ce93f8-e45d-42f3-abc2-0d9adcd67eb4
                                Volume_Name         svt-volume-automation-18244


              Created_At        2025-02-27T11:09:29.000Z
              Host_ID           r134-35ba6b46-2025-42a5-b06d-65f812228df8
              Host_NQN          nqn.2025-02.org.nvmeautomation:uuid:de251917-ca4a-4595-9209-f065243a945b
              Host_Name         automation-host-8ul6shc0
              Volume_Mappings
                                Namespace_ID        2
                                Namespace_UUID      a451b0d6d23d518489e4fab13468ac3f
                                Status              mapped
                                Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                                Volume_ID           r134-a6d6777d-6146-40a6-9e6e-b707c0dc6466
                                Volume_Mapping_ID   r134-66758b4f-f8ff-4256-bf49-ac99d5e44524
                                Volume_Name         svt-volume-automation-68494


              Created_At        2025-02-27T11:04:50.000Z
              Host_ID           r134-a2c83bdd-06b4-4800-8e95-02a8c8ea2d23
              Host_NQN          nqn.2014-08.com.vmware:nvme:Host-ESX-102
              Host_Name         host106-prash
              Volume_Mappings
                                Namespace_ID        1
                                Namespace_UUID      134872d307bc56459fb95a2020fde511
                                Status              mapped
                                Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                                Volume_ID           r134-2be0b97c-10b8-4cff-8a8b-d77a680d7470
                                Volume_Mapping_ID   r134-67d6d3e4-9c63-42c7-9ef7-cb38e9e83338
                                Volume_Name         vol-1-prash

                                Namespace_ID        4
                                Namespace_UUID      99fb4307c0c8594aabfa308b609291bb
                                Status              mapped
                                Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                                Volume_ID           r134-f8ae9a0f-5d9e-4319-aeb1-8a8ac0f2ebe3
                                Volume_Mapping_ID   r134-26d13661-711a-4a0a-b073-5032fc81ccdc
                                Volume_Name         test112345


              Created_At        2025-02-27T09:52:21.000Z
              Host_ID           r134-dc3e6f0a-15fb-4b7e-926e-04943856ffce
              Host_NQN          nqn.2014-08.com.vmware:nvme:vm9-esv-host
              Host_Name         automation219760
              Volume_Mappings
                                Namespace_ID        1
                                Namespace_UUID      134872d307bc56459fb95a2020fde511
                                Status              mapped
                                Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                                Volume_ID           r134-2be0b97c-10b8-4cff-8a8b-d77a680d7470
                                Volume_Mapping_ID   r134-89c930d0-32f3-4111-a270-b365543280ac
                                Volume_Name         vol-1-prash

                                Namespace_ID        2
                                Namespace_UUID      a451b0d6d23d518489e4fab13468ac3f
                                Status              mapped
                                Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                                Volume_ID           r134-a6d6777d-6146-40a6-9e6e-b707c0dc6466
                                Volume_Mapping_ID   r134-bfd44254-f35b-4e19-90b1-85aa88708718
                                Volume_Name         svt-volume-automation-68494
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_full_notm}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` and `hsts` as an alternative to `hosts` for the CLI actions.
{: tip}


## View details of a single host from the CLI
{: #view-single-host-detail-cli}
{: cli}

Run the following command to show host details for a specific host `ID`.

```sh
ibmcloud software-defined-storage host --host-id HOST-ID --url string
```
{: pre}


The following example uses the host ID to show host details.

```sh
$ ibmcloud software-defined-storage host \
  --host-id r134-dc3e6f0a-15fb-4b7e-926e-04943856ffce \
  --url $sds_endpoint
...

Host_ID           r134-dc3e6f0a-15fb-4b7e-926e-04943856ffce
Host_Name         my-host
Host_NQN          nqn.2014-08.com.vmware:nvme:vm9-esv-host
Created_At        2025-02-27T09:52:21.000Z
Volume_Mappings
                  Gateways
                                      IP_Address   10.64.4.16
                                      Port         8009

                                      IP_Address   10.64.4.17
                                      Port         8009

                                      IP_Address   10.64.4.18
                                      Port         8009

                                      IP_Address   10.64.4.19
                                      Port         8009

                  Namespace_ID        2
                  Namespace_UUID      a451b0d6d23d518489e4fab13468ac3f
                  Status              mapped
                  Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                  Volume_ID           r134-a6d6777d-6146-40a6-9e6e-b707c0dc6466
                  Volume_Mapping_ID   r134-bfd44254-f35b-4e19-90b1-85aa88708718
                  Volume_Name         my-vol1

                  Gateways
                                      IP_Address   10.64.4.16
                                      Port         8009

                                      IP_Address   10.64.4.17
                                      Port         8009

                                      IP_Address   10.64.4.18
                                      Port         8009

                                      IP_Address   10.64.4.19
                                      Port         8009

                  Namespace_ID        1
                  Namespace_UUID      134872d307bc56459fb95a2020fde511
                  Status              mapped
                  Subsystem_NQN       nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f
                  Volume_ID           r134-2be0b97c-10b8-4cff-8a8b-d77a680d7470
                  Volume_Mapping_ID   r134-89c930d0-32f3-4111-a270-b365543280ac
                  Volume_Name         my-vol2

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_full_notm}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).


You can also use the alias `sds` as an alternative to `software-defined-storage` for the CLI actions.
{: tip}





For more information about available command options, run `ibmcloud sds hosts --help`.


## View a list of all hosts with the API
{: #view-all-host-api}
{: api}

Make a `GET /hosts` request to list summary information about all hosts.

Before you begin, make sure that you have [set up your API environment](/docs/cephaas?topic=cephaas-set-up-environment&interface=api).
{: requirement}

See the following example.

```sh
curl -X GET $sds_endpoint/hosts\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H "IBM-API-Version: 2025-02-01"
```
{: pre}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_full_notm}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).

A successful response looks like the following example.

```json
{
  "hosts": [
    {
      "id": "r134-886f1457-7bee-4893-b3b8-0a75b0076a85",
      "name": "groovey-hardwood",
      "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002145",
      "created_at": "2025-02-27T09:52:08Z",
      "href": "$sds_endpoint/hosts/r134-886f1457-7bee-4893-b3b8-0a75b0076a85",
      "volume_mappings": [
        {
          "id": "r134-b561e8f8-cea4-4934-8527-726a5ccc309f",
          "status": "mapped",
          "href": "$sds_endpoint/hosts/r134-886f1457-7bee-4893-b3b8-0a75b0076a85/volume_mappings/r134-b561e8f8-cea4-4934-8527-726a5ccc309f",
          "volume": {
            "name": "magma-agreeably-groovy-hardwood",
            "id": "r134-1dee2264-a3c2-415d-bc86-dd05ad4f06dd"
          },
          "host": {
            "name": "groovey-hardwood",
            "nqn": "nqn.2014-08.org.nvmexpress:uuid:29181642-300c-a1e2-497a-172017002145",
            "id": "r134-886f1457-7bee-4893-b3b8-0a75b0076a85"
          },
          "subsystem_nqn": "nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f",
          "namespace": {
            "id": 1,
            "uuid": "ff5e44ffdeb15e1d9d134f6f0a2dc4bf"
          },
          "gateways": [
            {
              "ip_address": "xxx.xx.x.xx",
              "port": 8009
            },
            {
              "ip_address": "xxx.xx.x.xx",
              "port": 8009
            },
            {
              "ip_address": "xxx.xx.x.xx",
              "port": 8009
            },
            {
              "ip_address": "xxx.xx.x.xx",
              "port": 8009
            }
          ]
        }
      ]
    },
    {
      "id": "r134-f8e5b0dc-cfb3-470a-806e-a42cf47516d6",
      "name": "synthetics-test-host-dnd",
      "nqn": "nqn.2014-08.org.nvmexpress:uuid:d9eb0d42-f381-328d-0492-ce5ddce1297a",
      "created_at": "2025-02-20T09:08:53Z",
      "href": "$sds_endpoint/hosts/r134-f8e5b0dc-cfb3-470a-806e-a42cf47516d6"
    }
  ],
  "first": {
    "href": "$sds_endpoint/hosts?limit=1000"
  },
  "limit": 1000,
  "total_count": 2
}

```
{: screen}


## Viewing single host details with the API
{: #view-single-host-details-api}
{: api}

Make a `GET /hosts/{id}` request to see details of a host. See the following example.

```sh
curl -X GET $sds_endpoint/hosts/r134-b82edf1f-79ad-46e7-a800-cabb9a3d4921\
  -H 'accept: application/json'\
  -H "Authorization: Bearer $IAM_TOKEN"\
  -H "IBM-API-Version: 2025-02-01"
```
{: pre}

A successful response provides details of the host, such as the `host ID`, `host name`, `nqn`, `service instance ID` and also includes mapped volume details if it mapped to a volume.

```json
{
  "id": "r134-9492bd82-f2db-4871-a85d-34321c695f26",
  "name": "automation-host-bg9qtv3d",
  "nqn": "nqn.2025-02.org.nvmeautomation:uuid:c34ed557-c1b1-4036-83aa-b8cbf3567b69",
  "created_at": "2025-02-27T11:15:42Z",
  "href": "$sds_endpoint/hosts/r134-9492bd82-f2db-4871-a85d-34321c695f26",
  "volume_mappings": [
    {
      "id": "r134-c9ce93f8-e45d-42f3-abc2-0d9adcd67eb4",
      "status": "mapped",
      "href": "$sds_endpoint/hosts/r134-9492bd82-f2db-4871-a85d-34321c695f26/volume_mappings/r134-c9ce93f8-e45d-42f3-abc2-0d9adcd67eb4",
      "volume": {
        "name": "svt-volume-automation-18244",
        "id": "r134-bad36c92-8cfc-4912-b6bc-e714460a9ef8"
      },
      "host": {
        "name": "automation-host-bg9qtv3d",
        "nqn": "nqn.2025-02.org.nvmeautomation:uuid:c34ed557-c1b1-4036-83aa-b8cbf3567b69",
        "id": "r134-9492bd82-f2db-4871-a85d-34321c695f26"
      },
      "subsystem_nqn": "nqn.2014-08.com.ibm:nvmeof-f538f202-2907-4061-8463-6a40dbe6b69f",
      "namespace": {
        "id": 3,
        "uuid": "0d632e1ec03b5f139ff222a4494fe21d"
      },
      "gateways": [
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        },
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        },
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        },
        {
          "ip_address": "xx.xx.x.xx",
          "port": 8009
        }
      ]
    }
  ]
}

```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when {{site.data.keyword.cephaas_full_notm}} was configured. It is in the URL form. For example, `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:{port number}/v1`. You can set the URL once and then not have to add it for every command. For guidance on how to set the URL, see [Config commands](/docs/cephaas?topic=cephaas-ic-sds-cli-reference&interface=cli#ic-config-commands).



## View host details using Terraform
{: #view-host-tf}
{: terraform}

To view Terraform objects

```terraform
terraform state list
```
{: pre}

To target a host resource, run the following command:

```terraform
terraform state show ibm_sds_host.<ibm_sds_host_name>
```
{: pre}



## Next steps
{: #next-step-view-hosts}

Add hosts or manage your existing hosts.
