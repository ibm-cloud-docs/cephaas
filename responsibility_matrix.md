---

copyright:
 years: 2024, 2024
lastupdated: "2024-11-14"

keywords: sds, cephaas, responsibilities matrix

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using {{site.data.keyword.cephaas_full_notm}}
{: #responsibility-matrix}


Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.cephaas_short}}. For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities){: external}.
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.cephaas_full_notm}}. For the overall terms of use, see [{{site.data.keyword.cephaas_full_notm}} Terms and Notices](https://www.ibm.com/terms/?id=i126-9923){: external}.



## Incident and operations management
{: #incident-and-ops}


Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, and recovery.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Infrastructure health monitoring and notification| Remediate all infrastructure and hypervisor environment issues. Notify customers of applicable incidents.  | Ascertain the impact of each incident that is reported. Engage IBM Support as required. |
|Infrastructure health management| Continuously deliver new features, updates, and bug fixes as needed in a manner transparent to you. Schedule maintenance activities that have customer impact in advance and post notifications to the IBM Cloud status page.  | Set preferences to receive emails notifications. Monitor the IBM Cloud status page for general announcements. |
|Workload monitoring| Remediate all hardware failures, notification of potential workload impact.  | Engage IBM Support as required. |
|Incident management | Communicate unplanned incidents with customer impact through the CIE process. | If you are an impacted customer, obtain a report about the incident upon request. |
{: row-headers}
{: caption="Responsibilites for incident and operations" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Change management
{: #change-management}

Change management includes tasks such as deployment, configuration, upgrades, patching, configuration changes, and deletion.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Scaling | Scale the storage infrastructure as requested and to meet the capacity that you selected.  | Monitor the capacity usage for future increase of your subscription. Estimate and place order to add more capacity for your service instances. |
| Updates, fixes, and new features| Provide regular updates, bug fixes, and new features, following a continuous delivery model in a way that is transparent to you for all infrastructure tools, IBM deployed cloud services and IBM management, monitoring, and automation tools. Post notifications for changes that impact you.  | Set preferences to receive email notifications. Monitor the IBM Cloud status page for general announcements. Use best practices and keep application operating systems and workload applications patched and secure with the most recent security patches. |
| Creating and deploying configurations | Deploy and configure {{site.data.keyword.cephaas_full_notm}}. Provides the capability to select committed capacity for the service. | |
| Deleting block and object storage |  | You can delete block & object storage whenever you need to.|
{: row-headers}
{: caption="Responsibilites for change management" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Identity and access management
{: #iam-responsibilities}


Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.

| Task  | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Identity and access| Provide the function to restrict access to resources through the IBM Cloud console. Provide default access to the provisioned environment.  | Manage access to resources through IBM Cloud IAM (Identity and Access Management). Manage access to the on-premises environment. |
|Observability| Ensure overall health of the system by allowing integration of IBM Cloud Activity Tracker with your on-premises environment that audits the actions the users take in the cluster. | Set up IBM Cloud Activity Tracker or other functions to track user activity. |
{: row-headers}
{: caption="Responsibilites for identity and access management" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}

## Security and regulation compliance
{: #security-compliance}


Security and regulation compliance includes tasks such as security controls implementation and compliance certification.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Compliance | Maintain controls commensurate with the compliance certifications/attestations as stated in official data sheets. | Ensure and seek appropriate legal guidance in order to validate its compliance with pertinent industry compliance certifications and regulations. |
| Security | Continuous monitoring of resources to check for vulnerabilities and security breaches. | Update IAM policies and rules using IBM Cloud console to suit to your requirement. Also, ensure that the use of Storage resources are inline with the terms and conditions set forth in the IBM Cloud Service description and any other associated transaction documents. |
{: row-headers}
{: caption="Responsibilites for security and regulation compliance" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}


## Disaster recovery
{: #disaster-recovery}

Disaster recovery includes tasks such as data and configuration backup, replicating data and configuration to the disaster recovery environment, and failover on disaster events.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Meet disaster recovery objectives | Provides procedure for manual disaster recovery. | Use application level backup and DR solutions while maintaining a disaster recovery plan for their applications.  |
| Meet high availability objectives | IBM Cloud is available globally and is highly available. For more information about high availability, see the [IBM service level objectives](/docs/overview?topic=overview-slo). {{site.data.keyword.cephaas_full_notm}} deployment on-prem is highly available for services as well as data access by means of replication and erasure coding.  | Follow best practices for application level high availability. |
{: row-headers}
{: caption="Responsibilites for disaster recovery" caption-side="bottom"}
{: summary="The rows are read from left to right. The first column describes the task that the customer or IBM might be responsibility for. The second column describes {{site.data.keyword.IBM_notm}} responsibilities for that task. The third column describes your responsibilities as the customer for that task."}
