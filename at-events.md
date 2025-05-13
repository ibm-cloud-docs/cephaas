---

copyright:
 years: 2024, 2025
lastupdated: "2025-05-13"

keywords: cephaas, activity tracker events, auditing events, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracker events for {{site.data.keyword.cephaas_short}}
{: #at_events}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cephaas_full}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service to route auditing events from your account to destinations of your choice, by configuring targets and routes, that define where activity tracking events are sent. For instructions, see [Configuring an IBM Cloud Logs target](/docs/atracker?topic=atracker-getting-started-target-cloud-logs){: external}.

For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

## Locations where activity tracking events are generated
{: #at-locations}


### Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}

{{site.data.keyword.cephaas_full_notm}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}



## Viewing activity tracking events
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #at-events-log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)



## List of management events
{: #at_actions}

The following table lists the {{site.data.keyword.cephaas_short}} actions that generate an event.

| Action             | Description      |
|--------------------|------------------|
| software-defined-storage.instance.create       | The service instance was created.   |
| software-defined-storage.instance.update       | The Service instance was updated. |
| software-defined-storage.instance.delete       | The Service instance was deleted.  |
| software-defined-storage.certificate.inspect   | The certificate status was retrieved. |
| software-defined-storage.certificate.update    | The certificate was updated. |
| software-defined-storage.certificate.create    | The certificate was created. |
| software-defined-storage.certificate.delete    | The certificate was deleted. |
| software-defined-storage.s3-credential.create  | The S3 credential was created. |
| software-defined-storage.s3-credential.delete  | The S3 credential was deleted. |
| software-defined-storage.s3-credential.get     | One or more S3 credentials were retrieved. |
| software-defined-storage.volume.create         | The volume was created. |
| software-defined-storage.volume.read           | One or more volumes were retrieved. |
| software-defined-storage.volume.update         | The volume was updated. |
| software-defined-storage.volume.delete         | The volume was deleted. |
| software-defined-storage.host.create           | The host was created. |
| software-defined-storage.host.read             | One or more hosts were retrieved. |
| software-defined-storage.host.update           | The host was updated. |
| software-defined-storage.host.delete           | The host was deleted. |
| software-defined-storage.host.unmap            | The host was unmapped. |
| software-defined-storage.host.map              | The host was mapped. |
{: caption="Actions that generate management events" caption-side="bottom"}
