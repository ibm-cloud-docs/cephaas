
---

copyright:
 years: 2024, 2025
lastupdated: "2025-11-06"

keywords: ceph as a service, known issues

subcollection: cephaas

---

# Object asynchronous disaster recovery
{: #object-async-dr}

The **Object async DR** feature in {{site.data.keyword.cephaas_full_notm}} enables asynchronous object storage replication between a primary instance and a secondary instance. This capability is designed to provide robust disaster recovery in the event of a catastrophic failure or site loss, ensuring data durability and business continuity.

## Secure communication between sites
{: #secure-com}

To facilitate secure communication between the primary and secondary sites, the following features are implemented:

- **TLS Encryption**: TLS certificates secure the replication connections between the sites. These certificates are issued for the domain `software-defined-storage.appdomain.cloud` and are rotated periodically to maintain security.


- **High availability and site management**: To ensure continuous availability between sites, load balancing is used. It allows traffic to seamlessly route across sites, even during upgrades or node outages, minimizing service disruption.

Site fail overs are fully managed by IBM, ensuring operational consistency.

## Supported operations
{: #supported-ops}

Users can perform the following operations via the UI, CLI, or API:

- [Managing S3 credentials](/docs/cephaas?group=managing-s-certificates)
- [Quota management](/docs/cephaas?group=managing-capacity-allocations)

Credential operations and quota modifications are restricted to the primary site. 
{: note}


## Monitoring multisite DR with UI
{: #monitoring-multisite}

The {{site.data.keyword.cephaas_full_notm}} UI includes monitoring capabilities based on replication performance. **Replication** tab of the object storage dashboard displays the following graphs:

- Replication throughput: Measures the data transfer rate during replication.
