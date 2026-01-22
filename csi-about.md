---

copyright:
 years: 2024, 2025
lastupdated: "2025-12-15"

keywords: cephaas csi

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# About CSI driver
{: #csi-driver-about}

{{site.data.keyword.cephaas_full_notm}} CSI driver uses standard CSI sidecar containers maintained by the Kubernetes SIG Storage community. These container images are distributed via `registry.k8s.io` and are maintained by the upstream Kubernetes project.

You can find the source code and release information in the [Kubernetes CSI GitHub organization](https://kubernetes-csi.github.io/docs/drivers.html) driver (v1.0.0)

The following table lists the sidecar containers and related images used in the {{site.data.keyword.cephaas_full_notm}} CSI driver Helm chart, along with their versions and release details.


| Helm chart version | CSI driver version | Image source                  | Sidecar containers |
|--------------------|--------------------|-------------------------------|---------------------|
| 1.0.0              | 1.0.0             | `registry.k8s.io/sig-storage` | `csi-provisioner: v3.5.0`  
`csi-attacher: v4.8.0`  
`csi-resizer: v1.4.0`  
`csi-node-driver-registrar: v2.8.0`  
`csi-snapshotter: v6.2.2`  
`snapshot-controller: v6.2.2` |
{: caption="Helm chart and CSI driver versions" caption-side="bottom"}

- All sidecar containers listed above are sourced from the official Kubernetes SIG Storage registry.
- These components are essential for enabling dynamic provisioning, attaching, resizing, and snapshotting of volumes in Kubernetes environments.
- The CSI driver is packaged and deployed using a Helm chart, which includes the necessary sidecar containers for full functionality.

## Sidecar containers and image sources
{: #csi-containers}

The {{site.data.keyword.cephaas_full_notm}} CSI Driver v1.0.0 uses standard CSI sidecar containers maintained by the **Kubernetes SIG Storage community**. These containers are distributed via the public registry at [registry.k8s.io/sig-storage](https://kubernetes-csi.github.io/docs/sidecar-containers.html) and are aligned with upstream Kubernetes releases, ensuring timely updates and bug fixes.

**Sidecar containers used by {{site.data.keyword.cephaas_full_notm}} CSI Driver:**

- **csi-provisioner:**: v3.5.0  
- **csi-attacher**: v4.8.0  
- **csi-resizer**: v1.4.0  
- **csi-node-driver-registrar**: v2.8.0  
- **csi-snapshotter**: v6.2.2  
- **snapshot-controller**: v6.2.2  

You can find the source code and release information in the [Kubernetes CSI GitHub organization](https://github.com/kubernetes-csi).
