---

copyright:
 years: 2024, 2025
lastupdated: "2025-11-27"

keywords: cephaas, managing snapshots, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Snapshots overview
{: #working-with-snapshots}

In {{site.data.keyword.cephaas_full_notm}}, you can create snapshots of your block volumes for getting point-in-time backups of your data. Snapshots in {{site.data.keyword.cephaas_full_notm}} offers a flexible and efficient way to capture and manage point-in-time copies of your block volumes. You can also mount snapshots directly without needing to create a new volume. Snapshots are accessible via REST API, CLI, and a user-friendly UI for various operations such as view, create, update, restore, and delete. These features make snapshots a powerful tool for backup, recovery, and data management use cases.

In the {{site.data.keyword.cephaas_full_notm}}, snapshots are supported currently only for block storage and the snapshot operations can be performed through API and CLI. 
{: note}

Before you can access the Snapshot API for performing various tasks, make sure you have defined variables for the IAM token and API endpoint. For instructions, see [Setting up your API and CLI environment](/docs/cephaas?topic=cephaas-set-up-environment&interface=api).
{: Requirement}

The following snapshots operations are supported through the API and CLI:

- [Viewing the existing snapshots](/docs/cephaas?topic=cephaas-view-snapshots)
- [Viewing a specific snapshot](/docs/cephaas?topic=cephaas-view-specific-snapshot)
- [Creating a new snapshot](/docs/cephaas?topic=cephaas-create-new-snapshots)
- [Updating a snapshot](/docs/cephaas?topic=cephaas-update-a-snapshot)
- [Deleting a single snapshot](/docs/cephaas?topic=cephaas-delete-single-snapshot)
- [Deleting a collection of snapshots](/docs/cephaas?topic=cephaas-delete-collection-snapshots)
- [Creating volumes from snapshots](/docs/cephaas?topic=cephaas-volume-from-snapshots)
