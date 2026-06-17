---

copyright:
  years: 2024, 2026
lastupdated: "2026-06-17"

keywords: context-based restrictions, CBR, network security, cluster security, ROKS, access control

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Securing access with context-based restrictions
{: #cbr}

You can use context-based restrictions (CBR) in {{site.data.keyword.cloud_notm}} to control access to your resources based on factors such as network location, IP address, or service endpoints.
{: shortdesc}

In IBM Fusion as a service (FusionaaS), CBR helps you secure access to your Red Hat OpenShift on {{site.data.keyword.cloud_notm}} (ROKS) clusters and related resources.

## About CBR in FusionaaS
{: #cbr-about}

Context-based restrictions (CBR) allow you to define rules that restrict access to resources by evaluating request context, such as:

- Source IP address or subnet
- Virtual private cloud (VPC)
- Service endpoints

CBR rules can be used to enhance the security posture of your clusters by limiting where and how they can be accessed.

For more information about how CBR works in {{site.data.keyword.cloud_notm}}, see [Protecting cluster resources with context-based restrictions](https://cloud.ibm.com/docs/containers?topic=containers-cbr&interface=ui){: external}.

## CBR support in FusionaaS
{: #cbr-support}

In FusionaaS version 1, CBR support is available with the following scope:

- You can configure CBR rules for your ROKS cluster masters
- You cannot configure CBR rules for {{site.data.keyword.cloud_notm}} API endpoints used by IKS or ROKS

In FusionaaS version 1, configuring context-based restriction (CBR) rules for {{site.data.keyword.cloud_notm}} API endpoints is not supported. You can apply CBR rules only to cluster masters.
{: important}

## Protecting cluster access
{: #cbr-protect-cluster}

You can use CBR rules to restrict access to your cluster masters. This helps ensure that only requests from approved networks or environments can reach your cluster control plane.

For guidance on protecting cluster endpoints, see [Protecting cluster resources with context-based restrictions](https://cloud.ibm.com/docs/containers?topic=containers-cbr&interface=ui#protect-api-types-cbr){: external}.

## Unsupported scenarios
{: #cbr-unsupported}

The following scenario is not supported in FusionaaS version 1:

- Configuring CBR rules for {{site.data.keyword.cloud_notm}} API endpoints that are used to manage or interact with IKS or ROKS services

If you attempt to apply CBR rules to these endpoints, the configuration is not enforced in FusionaaS.

## Best practices
{: #cbr-best-practices}

- Use CBR rules to restrict access to cluster masters wherever possible
- Combine CBR with IAM roles and policies to control who can access resources
- Validate your network configurations to ensure that allowed sources are correctly defined
