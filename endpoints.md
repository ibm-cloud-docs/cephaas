---

copyright:
 years: 2024, 2024
lastupdated: "2024-11-21"

keywords: cephaas, endpoint, location, object storage, bucket, region, rclone, resiliency

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Endpoints
{: #endpoints}

Sending a REST API request, calling the {{site.data.keyword.cephaas_short}} CLI or configuring a storage client requires setting a target endpoint or URL. Each storage appliance has a unique endpoint as named as follows:

- `<cephaas-instance-id>.software-defined-storage.appdomain.cloud`

To retrieve your `cephaas-instance-id` from the IBM Cloud CLI:

1. Download the IBM Cloud CLI.

2. Login to your IBM Cloud account using the `ibmcloud login` command.

3. Retrieve a list of all {{site.data.keyword.cephaas_short}} service instances / deployments in your IBM Cloud account using the `software-defined-storage` service name:

   `ibmcloud resource service-instances --service-name software-defined-storage`

4. Retrieve the {{site.data.keyword.cephaas_short}} instance id (GUID) of the desired instance:

   `ibm-cloud resource service-instance <cephaas-deployment-name> --guid`

An example of a {{site.data.keyword.cephaas_short}} endpoint would be: `a5646acb-bf72-4127-bd4d-71b5ba3ae253.software-defined-storage.appdomain.cloud`

All {{site.data.keyword.cephaas_full}} endpoints require either TLS 1.2 or TLS 1.3 encryption.
{: note}

## Management API Endpoints
{: #mgmt-api-endpoints}

Each Management API has a separate host identifier as follows:
- Block Management API: `https://block-storage.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:443`
- Object Management API: `https://object-storage.<cephaas-instance-id>.software-defined-storage.appdomain.cloud:443`

## S3 API Endpoints
{: #s3-api-endpoints}

The Object Storage S3 data access APIs do not have a fully-qualified domain name assigned by IBM. Instead, a set of IP addresses are provided to you and you can provide your own, custom domain name and certificate. For instructions, see [Uploading S3 certificate](/docs/cephaas?topic=cephaas-uploading-s3-certificate).
