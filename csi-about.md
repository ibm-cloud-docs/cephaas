---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-14"

keywords: cephaas csi

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# About CSI driver

{{site.data.keyword.cephaas_full_notm}} CSI driver uses standard CSI sidecar containers maintained by the Kubernetes SIG Storage community. These container images are distributed via `registry.k8s.io` and are maintained by the upstream Kubernetes project.

You can find the source code and release information in the [Kubernetes CSI GitHub organization](https://github.com/ks) used in CephaaS CSI driver (v1.0.0)

The following table lists the sidecar containers and related images used in the {{site.data.keyword.cephaas_full_notm}} CSI driver Helm chart, along with their versions and release details.

CSI driver versionHelm chart versionImage sourceSidecar containersRelease dateRelease notes1.0.11.0.1registry.k8s.io/sig-storagecsi-provisioner: v3.5.0
- csi-attacher: v4.8.0
- csi-resizer: v1.4.0
- csi-node-driver-registrar: v2.8.0
- csi-snapshotter: v6.2.2
- snapshot-controller: v6.2.2
TBDTBD| 1.0.0              | 1.0.0              | `registry.k8s.io/sig-storage` | - `csi-provisioner: v3.5.0`<br>- `csi-attacher: v4.8.0`<br>- `csi-resizer: v1.4.0`<br>- `csi-node-driver-registrar: v2.8.0`<br>- `csi-snapshotter: v6.2.2`<br>- `snapshot-controller: v6.2.2` | Sept. 19, 2025 | Initial version |


- All sidecar containers listed above are sourced from the official Kubernetes SIG Storage registry.
- These components are essential for enabling dynamic provisioning, attaching, resizing, and snapshotting of volumes in Kubernetes environments.
- The CSI driver is packaged and deployed using a Helm chart, which includes the necessary sidecar containers for full functionality.
