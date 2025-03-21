---

copyright:
 years: 2024, 2025
lastupdated: "2025-03-11"

keywords: about block storage volume, volume encryption, IAM permissions for block storage volume, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# About Block storage volume
{: #block-storage-volume-about}

Block storage volume provides hypervisor-mounted, high-performance data storage for your instances. The infrastructure provides rapid scaling across zones, extra security, and performance.
{: shortdesc}

{{site.data.keyword.cephaas_full}} volume data is stored redundantly across multiple physical disks in an Availability Zone to prevent data loss due to failure of any single component.

When you create, view, or update a volume, the volume state is reported in the UI, CLI, API and Terraform. For guidance, see [View block volume](/docs/cephaas?topic=cephaas-view-volume).


## IAM roles for creating and managing volumes
{: #block-storage-iam}

Block Storage requires IAM permissions for role-based access control. Depending on your assigned role, you can create and manage volumes. For more information, see [IAM roles and actions](/docs/cephaas?topic=cephaas-managing-iam).

For more information, see the [best practices for assigning access](/docs/account?topic=account-account_setup#account_setup). For the complete IAM process, which includes inviting users to your account and assigning Cloud IAM access, see the [IAM getting started tutorial](/docs/account?topic=account-iamoverview).
{: tip}


## Block storage volume type
{: #block-storage-volumes-type}

{{site.data.keyword.cephaas_full_notm}} offers block-level volumes that can be attached to any available deployment in your premise and within certain limits. These volumes are deleted by default when the deployment is deleted. You can delete data volumes manually before deleting the deployment.


## Block storage volume encryption
{: #storage-encryption}

{{site.data.keyword.cloud_notm}} takes the need for security seriously and understands the importance of being able to encrypt data to keep it safe.

Data volumes are encrypted by default with IBM-managed encryption. When you create a volume, they are encrypted with IBM-managed encryption by default.


## Deleting your block storage volume
{: #delete-storage-volume}

If you no longer need a volume, you can delete it at any time. IBM wipes all data before the storage is reused. If you have more compliance requirements such as NIST 800-88 Guidelines for Media Sanitization, you must perform data sanitation procedures before you delete your volumes. For more information, see [NIST 800-88 Guidelines for Media Sanitation](https://csrc.nist.gov/pubs/sp/800/88/r1/final){: external}.

## Next steps
{: #block-storage-about-nextsteps}

Create block volumes.

For instructions, see [Creating block volumes](/docs/cephaas?topic=cephaas-creating-block-volume&interface=ui).
