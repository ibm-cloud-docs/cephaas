---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-28"

keywords: cephaas csi

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# About CSI driver
{: #csi-driver-about}

{{site.data.keyword.cephaas_full_notm}} CSI driver uses standard CSI sidecar containers maintained by the Kubernetes SIG Storage community. These container images are distributed via `registry.k8s.io` and are maintained by the upstream Kubernetes project.

You can find the source code and release information in the [Kubernetes CSI GitHub organization](https://githubCSI) driver (v1.0.0)

The following table lists the sidecar containers and related images used in the {{site.data.keyword.cephaas_full_notm}} CSI driver Helm chart, along with their versions and release details.

| Helm chart version | CSI driver version | Image source                  | Sidecar containers                                                                                                                                                                                                 |
|--------------------|--------------------|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.0.0              | 1.0.0              | `registry.k8s.io/sig-storage` | - `csi-provisioner: v3.5.0`<br>- `csi-attacher: v4.8.0`<br>- `csi-resizer: v1.4.0`<br>- `csi-node-driver-registrar: v2.8.0`<br>- `csi-snapshotter: v6.2.2`<br>- `snapshot-controller: v6.2.2` |

- All sidecar containers listed above are sourced from the official Kubernetes SIG Storage registry.
- These components are essential for enabling dynamic provisioning, attaching, resizing, and snapshotting of volumes in Kubernetes environments.
- The CSI driver is packaged and deployed using a Helm chart, which includes the necessary sidecar containers for full functionality.
