---

copyright:
  years: 2020, 2021
lastupdated: "2024-10-14"

keywords: cephaas, architecture, workload isolation levels

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Architecture and workload isolation of {{site.data.keyword.cephaas_full_notm}}
{: #compute-isolation}

{{site.data.keyword.cephaas_full}} is a hardware appliance hosted in your datacenter and remotely managed for you by IBM.

Review the following sample architecture for {{site.data.keyword.cephaas_full_notm}}, and learn more about the different isolation levels, so that you can choose the solution that best meets the requirements of the workloads that you want to run in the cloud.
{: shortdesc}

## {{site.data.keyword.cephaas_full_notm}} architecture
{: #architecture}

The following diagram and table describe the default components that are set up in an {{site.data.keyword.cephaas_full}} architecture.

![Architecture of IBM Storage Ceph as a Service](images/architecture-cephaas.svg "Title text that shows on hover here"){: caption="A description that prints on the page" caption-side="bottom"}

## {{site.data.keyword.cephaas_short}} workload isolation
{: #workload-isolation}

_Document how customer workloads are isolated from each other by plan. Do customer workloads run within the customer account?  Are customer workloads isolated within Kubernetes namespaces? Do customer workloads run on dedicated compute? Check out the example from Kubernetes: https://cloud.ibm.com/docs/containers?topic=containers-service-arch#worker-components_

Each {{site.data.keyword.cephaas_full_notm}} instance manages one appliance which is located within your datacenter. The service lifecycle and access operations and APIs are managed within your {site.data.keyword.cloud_notm} account and is not accessible to any other {site.data.keyword.cloud_notm} account. All data management and access APIs are accessible within your datacenter and are not remotely accessible.
