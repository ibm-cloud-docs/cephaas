---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-14"

keywords: unified storage, volume size, IOPS, Security, Encryption, LUN, secondary storage, mount storage, provision storage, iSCSI, MPIO, redundant

subcollection: cephaas

---
{{site.data.keyword.attribute-definition-list}}
{: ui-linked}

# Getting started with {{site.data.keyword.cephaas_full_notm}}
{: #getting-started}

{{site.data.keyword.cephaas_full}} is a powerful software-defined enterprise storage platform that delivers a cloud-like experience on-premises with the convenience and flexibility of a pay-as-you-go model. Designed to provision storage in minutes, it enables self-provisioning of storage resources, allowing enterprises to quickly adapt to rapidly changing demands, breaking down the barriers of managing multiple dedicated storage systems.
{: shortdesc}

By eliminating over-provisioning and right-sizing your infrastructure, you can ensure optimal resource utilization and cost-efficiency. Based on the benefits of IBM Storage Ceph, it breaks down the silos of dedicated, proprietary storage infrastructure and software, offering unified support for multiple protocols across a single platform. With a seamless, single point of management, it simplifies operations, giving you control over your entire storage environment from one interface.


## Before you begin
{: #prereqs}
{: step}

{{site.data.keyword.cephaas_full_notm}} can be provisioned from 10 GB to 12 TB with two options:
- Provision **Endurance** tiers that feature pre-defined performance levels and other features like snapshots and replication.
- Build a high-powered **Performance** environment with allocated input/output operations per second (IOPS).



## Provisioning considerations
{: #provconsiderationsBlockStorage}
{: step}

### Block storage volume size
{: #sdsblockstoragevolumesize}

IOPS for both Endurance and Performance is based on a 16-KB IO size with a 50/50 read and write, 50/50 random and sequential workload. A 16-KB block is the equivalent of one write operation to the volume.
{: important}

The IO size that is used by your application directly impacts the storage performance. If the IO size that is used by your application is smaller than 16 KB, the IOPS limit is realized before the throughput limit. Conversely, if the IO size that is used by your application is larger than 16 KB, the throughput limit is realized before the IOPS limit.


### Authorized hosts
{: #numberofhosts}

Another factor to consider is the number of hosts that are using your volume. IOPS limits are enforced at the volume level. In other words, two hosts connected to a volume with 6000 IOPS share that 6000 IOPS. At high IOPS counts, you might several hosts to access the volume simultaneously to realize the maximum IOPS available, especially at extreme IOPS counts (10,000s).

The maximum IOPS for a block storage volume is 48,000 IOPS. If your workload requires high throughput, it's best to configure at least a couple servers to access your volume to avoid a single-server bottleneck.

The default limit for the number of authorizations per block volume is eight. That means that up to eight hosts can be authorized to access the CephaaS LUN. For more information about authorization and increasing the limit of 8, see the [FAQs].

### Network connection
{: #networkconnectivity}

The speed of your Ethernet connection must be faster than the expected maximum throughput from your volume. Generally, don't expect to saturate your Ethernet connection beyond 70% of the available bandwidth. For example, if you have 6,000 IOPS and are using a 16-KB IO size, the volume can handle approximately 94-MBps throughput. If you have a 1-Gbps Ethernet connection to your LUN, it becomes a bottleneck when your servers attempt to use the maximum available throughput. It's because 70 percent of the theoretical limit of a 1-Gbps Ethernet connection (125 MB per second) would allow for 88 MB per second only.

To achieve maximum IOPS, adequate network resources need to be in place. Other considerations include private network USAGE outside of storage, and host-side and application-specific tunings (IP stack or queue depths, and other settings).

Storage traffic ought to be isolated from other traffic types, and not be directed through firewalls and routers. For more information, see the [FAQ] section.

Storage traffic is included in the total network USAGE of Public virtual servers.
{: tip}

## Submitting your order
{: #submitorder}
{: step}

When you're ready to submit your order, you can place it in the [console].



## Managing your new storage
{: #managingnewstorage}
{: step}

In the console, from the CLI, with the API, or Terraform, you can manage various aspects of your {{site.data.keyword.cephaas_short}} such as host authorizations and cancellations. For more information, see [Managing {{site.data.keyword.cephaas_short}}].

You can keep your data in sync in two different locations by using replication. Replication uses one of your snapshot schedules to automatically copy snapshots to a destination volume in a remote data center. The copies can be recovered in the remote site if a catastrophic event occurs or your data becomes corrupted. For more information, see [Replication and Disaster Recovery – Replicating Data].
