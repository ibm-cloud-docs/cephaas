---

copyright:
  years: 2020, 2021
lastupdated: "2024-09-12"

keywords: cephaas, architecture, workload isolation levels

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}



# Learning about {{site.data.keyword.cephaas_short}} architecture and workload isolation
{: #compute-isolation}



_The short description should be a single, concise paragraph that contains one or two sentences and no more than 50 words. Summarize your offering's architecture and support for isolating one tenants' workload from another._

Review the following sample architecture for {{site.data.keyword.cephaas_short}}, and learn more about different isolation levels so that you can choose the solution that best meets the requirements of the workloads that you want to run in the cloud.
{: shortdesc}

## {{site.data.keyword.cephaas_short}} architecture
{: #architecture}

_Review the following example: https://cloud.ibm.com/docs/containers?topic=containers-service-arch. Review the System Architecture Guide: https://pages.github.ibm.com/CloudEngineering/system_architecture/services/multitenancy.html. Provide an architectural overview diagram identifying what runs within the IBM Service Account and what runs in the customer's account._

## {{site.data.keyword.cephaas_short}} workload isolation
{: #workload-isolation}

_Document how customer workloads are isolated from each other by plan. Do customer workloads run within the customer account?  Are customer workloads isolated within Kubernetes namespaces? Do customer workloads run on dedicated compute? Check out the example from Kubernetes: https://cloud.ibm.com/docs/containers?topic=containers-service-arch#worker-components_
