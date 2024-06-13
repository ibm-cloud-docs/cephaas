---

copyright:
  years: 2024
lastupdated: "2024-05-08"

keywords: Block Storage, IOPS, Security, Encryption, LUN, secondary storage, mount storage, provision storage, iSCSI, MPIO, redundant

subcollection: sdsaas

---

{: ui-linked}

# Getting started with Software Defined Storage as a Service (SDSaaS)
{: #getting-started}

SDSaaS is a persistent, high-performance iSCSI storage that is provisioned and managed independently of Compute instances. iSCSI-based SDSaaS LUNs are connected to authorized devices through redundant multi-path I/O (MPIO) connections.

SDSaaS brings best-in-class levels of durability and availability with an unmatched feature set. It is built by using industry standards and best practices. SDSaaS is designed to protect the integrity of the data and maintain availability through maintenance events and unplanned failures, and provide a consistent performance baseline.
{: shortdesc}


## Before you begin
{: #prereqs}
{: step}

SDSaaS LUNs can be provisioned from 20 GB to 12 TB with two options:
- Provision **Endurance** tiers that feature pre-defined performance levels and other features like snapshots and replication.
- Build a high-powered **Performance** environment with allocated input/output operations per second (IOPS).

For more information about the SDSaaS offering, see [What is SDSaaS](https://www.ibm.com/products/sdsaas){: external}.

## Provisioning considerations
{: #provconsiderSDSBlockStorage}
{: step}

### Block size
{: #sdsblockstoragesize}

IOPS for both Endurance and Performance is based on a 16-KB IO size with a 50/50 read and write, 50/50 random and sequential workload. A 16-KB block is the equivalent of one write operation to the volume.
{: important}

The IO size that is used by your application directly impacts the storage performance. If the IO size that is used by your application is smaller than 16 KB, the IOPS limit is realized before the throughput limit. Conversely, if the IO size that is used by your application is larger than 16 KB, the throughput limit is realized before the IOPS limit.

| IO Size (KB) | IOPS | Throughput (MB/s) |
|-----|-----|-----|
| 4 | 1,000 | 4 |
| 8 | 1,000 | 8 |
| 16 | 1,000 | 16 |
| 32 | 500 | 16 |
| 64 | 250 | 16 |
| 128 | 128 | 16 |
| 512 | 32 | 16 |
| 1024 | 16 | 16 |
{: caption="Table 1 shows examples of how block size and IOPS affect the throughput. Average IO size x IOPS = Throughput in MB/s." caption-side="top"}

### Authorized hosts
{: #numberofhosts}

Another factor to consider is the number of hosts that are using your volume. IOPS limits are enforced at the volume level. In other words, two hosts connected to a volume with 6000 IOPS share that 6000 IOPS. At high IOPS counts, you might several hosts to access the volume simultaneously to realize the maximum IOPS available, especially at extreme IOPS counts (10,000s).

The maximum IOPS for a block storage volume is 48,000 IOPS. If your workload requires high throughput, it's best to configure at least a couple servers to access your volume to avoid a single-server bottleneck.

The default limit for the number of authorizations per block volume is eight. That means that up to eight hosts can be authorized to access the SDSaaS LUN. For more information about authorization and increasing the limit of 8, see the [FAQs].

### Network connection
{: #networkconnectivity}

The speed of your Ethernet connection must be faster than the expected maximum throughput from your volume. Generally, don't expect to saturate your Ethernet connection beyond 70% of the available bandwidth. For example, if you have 6,000 IOPS and are using a 16-KB IO size, the volume can handle approximately 94-MBps throughput. If you have a 1-Gbps Ethernet connection to your LUN, it becomes a bottleneck when your servers attempt to use the maximum available throughput. It's because 70 percent of the theoretical limit of a 1-Gbps Ethernet connection (125 MB per second) would allow for 88 MB per second only.

To achieve maximum IOPS, adequate network resources need to be in place. Other considerations include private network usage outside of storage, and host-side and application-specific tunings (IP stack or queue depths, and other settings).

Storage traffic ought to be isolated from other traffic types, and not be directed through firewalls and routers. For more information, see the [FAQ] section.

Storage traffic is included in the total network usage of Public virtual servers.
{: tip}

## Submitting your order
{: #submitorder}
{: step}

When you're ready to submit your order, you can place it in the [console].




## Managing your new storage
{: #managingnewstorage}
{: step}

In the console, from the CLI, with the API, or Terraform, you can manage various aspects of your SDSaaS such as host authorizations and cancellations. For more information, see [Managing SDSaaS].

You can keep your data in sync in two different locations by using replication. Replication uses one of your snapshot schedules to automatically copy snapshots to a destination volume in a remote data center. The copies can be recovered in the remote site if a catastrophic event occurs or your data becomes corrupted. For more information, see [Replication and Disaster Recovery – Replicating Data].
