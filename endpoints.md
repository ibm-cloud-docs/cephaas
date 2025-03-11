---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-11"

keywords: cephaas, endpoint, location, region, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Endpoints
{: #endpoints}

Sending a REST API request, calling the {{site.data.keyword.cephaas_short}} CLI, or configuring a storage client requires setting a target endpoint or URL. Each storage appliance have a unique endpoint that is named as `https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud`.

To retrieve your `cephaas-instance-id` from the IBM Cloud CLI, do the following steps:

1. Download the IBM Cloud CLI.

2. Log in to your IBM Cloud account by using the `ibmcloud login` command.

3. Retrieve a list of all {{site.data.keyword.cephaas_short}} deployments in your IBM Cloud account by using the `software-defined-storage` service name.

    ```sh
    ibmcloud resource service-instances --service-name software-defined-storage
    ```
    {: pre}

4. Retrieve the {{site.data.keyword.cephaas_short}} instance ID (GUID) of the instance you want.

    ```sh
    ibm-cloud resource service-instance <cephaas-deployment-name> --guid
    ```
    {: pre}

Example of an {{site.data.keyword.cephaas_short}} endpoint: `a5646acb-bf72-4127-bd4d-71b5ba3ae253.software-defined-storage.appdomain.cloud`

All {{site.data.keyword.cephaas_full}} endpoints require either TLS 1.2 or TLS 1.3 encryption.
{: note}

## Management API Endpoints
{: #mgmt-api-endpoints}

The CephaaS Management API has a separate host identifier.

For example,
`https://sds-cephaas.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:443`



## S3 API Endpoints
{: #s3-api-endpoints}

The Object Storage S3 data access APIs do not have a fully qualified domain name that is assigned by IBM. Instead, a set of IP addresses are provided to you and you can provide your own, custom domain name and certificate. For instructions, see [Uploading S3 certificate](/docs/cephaas?topic=cephaas-uploading-s3-certificate).
