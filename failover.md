---

copyright:
 years: 2024, 2026
lastupdated: "2026-02-19"

keywords: cephaas, event notifications, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Failover behavior
{: #failover-behavior}

In a dual–disaster recovery (DR) site setup of {{site.data.keyword.cephaas_full_notm}}, each site has a defined role - primary or secondary that determines how metadata and object requests are processed. The following section explains how the two sites interact under normal operation and what happens during a failover event.

To perform a failover, you must contact IBM. IBM will initiate the failover on your behalf.
{: important}

## Metadata requests
{: #metadata-requests}

Metadata‑based operations (such as bucket creation, deletion, or updates) must always be processed by the primary site to maintain strong consistency.

- When a client sends metadata requests to the secondary site, the requests are automatically proxied to the primary site.  
- The secondary site never processes metadata updates on its own unless a failover makes it the new primary.


## Object requests
{: #object-requests}

The secondary site can directly serve object‑level requests (PUT/GET/DELETE).

However, to prevent race conditions:

- Do not load balance object traffic across both sites in a round‑robin manner.
- Each client or application should target a single site at a time for object I/O.  
- This ensures object version ordering is not violated across geographically distributed sites.


## When failover occurs
{: #when-failover-occurs}

Failover changes which site acts as the primary for metadata operations.

- The **new primary** begins terminating all metadata requests locally.
- It becomes fully authoritative for all metadata updates going forward.


If the original primary site goes down:

- Metadata requests sent to the secondary site will fail, because the secondary cannot apply them while still in secondary role.
- Only the primary site can commit metadata updates.


## When to initiate a failover
{: #initiate-failover}

Failover should only be performed if you can make sure:

- All future metadata requests will be sent exclusively to the new primary.
- No clients or services will continue sending metadata operations to the old primary.


### Risk of split‑brain scenarios
{: #split-brain}

A split‑brain can occur if both sites process metadata updates independently.

Example risk:

- The old primary comes back online.
- A client unintentionally sends a metadata request to the old primary before it has synchronized with the new primary.
- The two sites now contain diverging metadata states.

This creates inconsistent bucket definitions or placement rules, which can lead to data loss or corruption.

To avoid split‑brain scenario:

1. Do not perform a failover unless the old primary is fully isolated or guaranteed offline.
2. After failover, ensure all clients, load balancers, DNS entries, and internal services now target the new primary for metadata operations.
3. When the old primary returns, bring it up only after it can safely synchronize with the new primary.
