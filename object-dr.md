
---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-28"

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

- **Authentication**: User credentials are created in Service Manager (SM) and deployed to both sites to enable authenticated communication. This credential is also rotated periodically.

- **High availability and site management**: To ensure continuous availability between sites, Virtual IP (VIP) addresses and load balancing are used. This design allows traffic to seamlessly route across sites, even during upgrades or node outages, minimizing service disruption.

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
- Replication lag: Indicates the delay between primary and secondary site synchronization.


