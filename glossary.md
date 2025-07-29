---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-29"

keywords: glossary, ceph as a service,

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Glossary
{: #glossary}

This glossary provides terms and definitions used in {{site.data.keyword.cephaas_full}}, helping you to understand important concepts, features, and terminology related to storage, management, security, and integration.


## **Activity tracking events**

Events that record actions or changes within the system for auditing or monitoring purposes.

## **Bandwidth**

The data transfer rate allocated to a volume or resource, typically measured in MB/s or GB/s.

## **Block storage**

A type of data storage where data is stored in fixedsized blocks. Each block acts as an individual hard drive, and block storage is commonly used for databases and virtual machines.

## **Capacity allocation**

The process of assigning a specific amount of storage space to a volume or other storage resource.

## **Create, Delete, Update (CRUD operations)**

The basic operations for managing resources—creating, deleting, and updating them.

## **Datastore**

A storage repository for virtual machine files and other data, often used in virtualization environments.

## **Deployment**

An instance of the CephaaS service, including its configuration, resources, and associated workloads.

## **Endpoints**

Network addresses (URLs) used to access APIs or services.

## **Environment variable**

A variable set in the operating system or shell that provides configuration information to commands or scripts.

## **Event notification**

A message or alert generated when a specific event occurs, such as a certificate expiring or a volume being deleted.

## **Expand (volume)**

Increasing the capacity of an existing storage volume to accommodate more data.

## **Host**

A server or virtual machine that connects to storage volumes to read or write data.

## **Host NQN (NVMe Qualified Name)**

A unique identifier for a host in NVMe-oF environments, used to establish secure connections between hosts and storage.

## **href**

A URL or link to the resource in the API.

## **Initiator**

The component (usually software or hardware) on a host that initiates a connection to storage resources.

## **IOPS (Input/Output Operations Per Second)**

A performance metric indicating how many read/write operations a storage resource can handle per second.

## **Mapping (volume to host mapping)**

The process of associating a storage volume with a host, allowing the host to access the volume.

## **NVMe-oF (Non-Volatile Memory Express over Fabrics)**

A protocol that enables NVMe storage devices to be accessed over network fabrics such as Ethernet or Fibre Channel.

## **Object storage**

A storage architecture that manages data as objects, as opposed to files or blocks. Each object includes the data, metadata, and a unique identifier.

## **Observability**

The ability to monitor, measure, and understand the state and behavior of a system.


## **Provisioned size**

The amount of storage capacity allocated to a volume or resource.

## **PSK (PreShared Key) encryption**

A method of securing communications using a shared secret key that is distributed to both parties in advance.

## **S3 certificate**

A digital certificate used to secure communications and authenticate access to S3-compatible object storage.

## **S3 credentials**

Authentication information (such as access keys and secrets) used to access S3compatible object storage.

## **Snapshot**

A point-in-time copy of data, such as a volume or datastore, used for backup, recovery, or cloning purposes.

## **Source**

The origin of an event or resource, often specified as a CRN.

## **Specversion**

The version of the event specification (such as CloudEvents) used in event notifications.

## **Status**

The current state of a resource (e.g., pending, available, failed, updating).

## **Terraform**

An open-source infrastructure-as-code tool for provisioning and managing cloud resources.


## **VMWare vSphere plug-in**

A software component that integrates IBM Storage Ceph as a Service with VMware vSphere environments.


## **vSphere host**

A physical or virtual server managed by VMware vSphere.

## **vSphere snapshot**

A point-in-time copy of a virtual machine or datastore in a VMware environment.

## **Workload isolation**

The practice of separating workloads to improve security, performance, or compliance.

## **Endpoint URL**

The network address used to access a service or API.
