---

copyright:
 years: 2024, 2026
lastupdated: "2026-04-29"

keywords: glossary, ceph as a service,

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Glossary
{: #glossary}

This glossary provides terms and definitions used in {{site.data.keyword.cephaas_full}}, helping you to understand important concepts, features, and terminology related to storage, management, security, and integration.

## **Activity tracking events**
{: #activity-tracking-events}

Events that record actions or changes within the system for auditing or monitoring purposes.

## **Bandwidth**
{: #bandwidth}

The data transfer rate allocated to a volume or resource, typically measured in MB/s or GB/s.

## **Capacity allocation**
{: #capacity-allocation}

The process of assigning a specific amount of storage space to a volume or other storage resource.

## **Create, Delete, Update (CRUD operations)**
{: #crud-operations}

The basic operations for managing resources—creating, deleting, and updating them.

## **Datastore**
{: #datastore}

A storage repository for virtual machine files and other data, often used in virtualization environments.

## **Deployment**
{: #deployment}

An instance of the {{site.data.keyword.cephaas_full_notm}}, including its configuration, resources, and associated workloads.

## **Endpoints**
{: #endpoints}

Network addresses (URLs) used to access APIs or services.

## **Event notification**
{: #event-notification}

A message or alert generated when a specific event occurs, such as a certificate expiring or a volume being deleted.

## **Expand (volume)**
{: #expand-volume}

Increasing the capacity of an existing storage volume to accommodate more data.

## **Host**
{: #host}

A server or virtual machine that connects to storage volumes to read or write data.

## **Host NQN (NVMe Qualified Name)**
{: #host-nqn}

A unique identifier for a host in NVMe-oF environments, used to establish secure connections between hosts and storage.

## **Initiator**
{: #initiator}

The component (usually software or hardware) on a host that initiates a connection to storage resources.

## **IOPS (Input/Output Operations Per Second)**
{: #iops}

A performance metric indicating how many read/write operations a storage resource can handle per second.

## **Link Aggregation Control Protocol (LACP)**
{: #lacp}

A type of link aggregation that ensures connectivity continues even after one of the connections breaks.

## **Mapping (volume to host mapping)**
{: #mapping}

The process of associating a storage volume with a host, allowing the host to access the volume.

## **NVMe-oF (Non-Volatile Memory Express over Fabrics)**
{: #nvme-of}

A protocol that enables NVMe storage devices to be accessed over network fabrics such as Ethernet or Fibre Channel.

## **Observability**
{: #observability}

The ability to monitor, measure, and understand the state and behavior of a system.

## **Open Service Broker (OSB)**
{: #osb}

A provider that implements the Open Service Broker API (OSB), a standard interface for provisioning and managing cloud services.

## **Provisioned size**
{: #provisioned-size}

The amount of storage capacity allocated to a volume or resource.

## **PSK (PreShared Key) encryption**
{: #psk-encryption}

A method of securing communications using a shared secret key that is distributed to both parties in advance.

## **Quad Small Form-factor Pluggable (QSFP)+**
{: #qsfp}

A type of transceiver that is used for connecting network equipment in data centers, high-performance computing environments, and telecommunications. QSFP cables are essential for modern network environments and data centers.

## **RC**
{: #rc}

Resource Controller in IBM cloud platform used for provisioning service instances.

## **RSOS (Remote Storage Orchestration Service)**
{: #rsos}

An endpoint or service that enables the provisioning and management of storage volumes on-premises. It acts as an orchestration layer, allowing users to automate and control storage resources outside the cloud, typically within their own data centers.

## **Service Instance**
{: #service-instance}

RC manageable resource of software-defined storage in IBM cloud.

## **Service Broker**
{: #service-broker}

Provider for service instances, implements OSB spec.

## **S3 certificate**
{: #s3-certificate}

A digital certificate used to secure communications and authenticate access to S3-compatible object storage.

## **S3 credentials**
{: #s3-credentials}

Authentication information (such as access keys and secrets) used to access S3-compatible object storage.

## **Snapshot**
{: #snapshot}

A point-in-time copy of data, such as a volume or datastore, used for backup, recovery, or cloning purposes.

## **Specversion**
{: #specversion}

The version of the event specification (such as CloudEvents) used in event notifications.

## **SSR (Systems Service Representative)**
{: #ssr}

A support specialist who assists with the maintenance, troubleshooting, and repair of IBM systems and infrastructure. SSRs provide technical support, perform hardware and software servicing, and help ensure systems remain operational and reliable for customers.

## **VMWare vSphere plug-in**
{: #vmware-vsphere-plugin}

A software component that integrates IBM Storage Ceph as a Service with VMware vSphere environments.

## **vSphere host**
{: #vsphere-host}

A physical or virtual server managed by VMware vSphere.

## **vSphere snapshot**
{: #vsphere-snapshot}

A point-in-time copy of a virtual machine or datastore in a VMware environment.

## **Workload isolation**
{: #workload-isolation}

The practice of separating workloads to improve security, performance, or compliance.

## **Endpoint URL**
{: #endpoint-url}

The network address used to access a service or API.
