---

copyright:
 years: 2025, 2025
lastupdated: "2025-12-19"

keywords: cephaas csi

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Node prerequisites for CSI Driver
{: #node-pre}

All Kubernetes worker nodes running the CSI node plugin must meet these prerequisites to ensure reliable NVMe/TCP volume operations.

NVMe/TCP functionality depends on kernel-level support for both NVMe and TCP transport. If the required kernel modules are missing or the operating system version is unsupported on the node, the CSI driver may fail to perform as expected, leading to issues such as inability to attach or mount NVMe/TCP volumes. Ensuring these prerequisites are met is critical for stable and reliable storage operations in Kubernetes environments.

## Supported operating system
{: #supported-os}

- Red Hat Enterprise Linux (RHEL) 9.5 or later  
- Must use the **nvme-cli** version shipped with the OS, which is version 2.11 or later

Older versions of RHEL or nvme-cli may not support certain NVMe/TCP features or could lead to connection failures or `I/O error`. We recommend using the tested versions (RHEL 9.5 and nvme-cli 2.11) or newer for compatibility and stability.
{: note}

## Required kernel modules
{: #kernel-modules}

The following kernel modules must be loaded on every Kubernetes worker node:

- `nvme`
- `nvme_tcp`

### Verifying module status
{: #module-status}

Run the following command:

```bash
lsmod | grep nvme
```

Expected output should include both, nvme and nvme_tcp.
