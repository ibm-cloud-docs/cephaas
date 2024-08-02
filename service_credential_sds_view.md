---

copyright:
 years: 2024, 2024
lastupdated: "2024-08-02"

keywords: sdsaas service credential view, list

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# View service credential details
{: #view-service-credential-sds}

View a service credential using the UI, CLI, or API.
{: shortdesc}


## View all service credential in the UI
{: #view-all-sds-service-credential-ui}
{: ui}

To view all the service credentials, navigate to **SDS as a Service > Object Storage > Service credentails** tab.


## View a service credential detail in the UI
{: #view-sds-service-credential-detail-ui}
{: ui}

To view details of a service credentials,

1. Navigate to **SDS as a Service > Object Storage > Service credentails** tab.

2. Click on the service credential name. The row expands downwards to display the credential details.


## View service credential details from the CLI
{: #retrieving-service-credential-details-cli}
{: cli}

Use the `credentials` command to view the list of access keys created for a given service instance (deployment).

Run the following command and ensure you have provided `INSTANCEID` of the credential whose details you want to view and the API endpoint.


```sh
ibmcloud software-defined-storage credentials --instanceid INSTANCEID --url string
```
{: pre}

See the following example.

```bash
ibmcloud software-defined-storage credentials --instanceid exampleString --url $sds_endpoint
```
{: screen}

The `$sds_endpoint` is an environment variable that points to the endpoint provided to you when CephaaS was configured. It is in the URL form. For example, https://{on-prem}.endpoint.com:{port number}/v1
{: note}
