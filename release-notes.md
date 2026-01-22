---

copyright:
 years: 2024, 2026
lastupdated: "2026-01-22"

keywords: ceph as a service, cephaas, release notes

subcollection: cephaas

content-type: release-note

---


{{site.data.keyword.attribute-definition-list}}


# Release notes for {{site.data.keyword.cephaas_full_notm}}
{: #relnotes}

Use these release notes to learn about the latest updates to {{site.data.keyword.cephaas_full}} that are grouped by month and year.
{: shortdesc}

## January 2026
{: #sds-jan26}

### 22 January 2026
{: #sds-22-jan26}
{: release-note}

This {{site.data.keyword.cephaas_full_notm}} release supports the Asynchronous disaster recovery feature, extending to both, low-cost disaster recovery (brownfield) and greenfield environments.

Ceph upgrade
:   {{site.data.keyword.cephaas_full_notm}} now supports upgraded Ceph version from 8.0 to 8.1 for improved performance and compatibility.

Async Disaster Recovery (DR) Enhancements
:   This release includes comprehensive checks for synchronization, failover, and replication consistency across environments. See [Object asynchronous disaster recovery](/docs/cephaas?topic=cephaas-object-async-dr)

High Availability Improvements
:   Increased replica counts for critical platform and storage pods to enhance resilience.

## September 2025
{: #sds-august25}


### 29 September 2025
{: #sds-29-sep2025}
{: release-note}

TLS Encryption for NVMe/TCP
:   {{site.data.keyword.cephaas_full_notm}} now supports TLS encryption for NVMe/TCP via API, CLI, and UI, ensuring secure data transmission and payload encryption.

Carbon 11 UI and navigation upgrade 
:   This release introduces UI updates aligned with Carbon 11, including improvements to responsiveness, layout alignment, colors, fonts, and hover states. Page navigations have been streamlined, with full validation for input handling, browser compatibility, and performance optimization. 

Snapshot functionality
:   Users can manage block volume snapshots via API and CLI, with read-only UI visibility for enhanced monitoring, management, and resiliency.

Event notifications
:   {{site.data.keyword.cephaas_full_notm}} now supports sending event alerts via email, SMS, and webhooks through {{site.data.keyword.en_full}}, enabling easier communication and event-driven automation.

## March 2025
{: #sds-mar25}


### 20 March 2025
{: #sds-mar2025}
{: release-note}

General availability of API, Go SDK and Terraform
:   Block and Object storage management API reference documentation are now available along with documentation for Go SDK and Terraform.

### 4 March 2025
{: #sds-mar0425}
{: release-note}

Introducing {{site.data.keyword.cephaas_full}}
:   {{site.data.keyword.cephaas_full_notm}} is a multi-protocol, cloud-like software-defined storage solution, delivered on-premises, and fully managed by IBM. This innovative service offers a fast and effortless way to transition to a modern cloud-operating model, allowing you to quickly and easily self-deploy storage within your data center, without the need for costly infrastructure setup or lengthy implementation timelines.
