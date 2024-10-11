---

copyright:
 years: 2024, 2024
lastupdated: "2024-10-11"

keywords: cephaas activity tracker events

subcollection: sdsaas

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.cephaas_full_notm}}
{: #at_events}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cephaas_full}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For instructions, see [Configuring an IBM Cloud Logs target](/docs/atracker?topic=atracker-getting-started-target-cloud-logs){: external}.

For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).


## Viewing activity tracking events for {{site.data.keyword.cephaas_full_notm}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the {{site.data.keyword.cephaas_full_notm}} dashboard
{: #log-launch-integrated}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)



## List of management events
{: #at_actions}

The following table lists the {{site.data.keyword.cephaas_short}} actions that generates an event.

| Action             | Description      |
|--------------------|------------------|
| software-defined-storage.instance.create | Service instance was created   |
| software-defined-storage.instance.update | Service instance was updated  |
| software-defined-storage.instance.delete | Service instance was deleted  |
| software-defined-storage.account.create | Storage account credential was created |
| software-defined-storage.account.delete | Storage account credential was deleted |
| software-defined-storage.account.get | One or more storage account credentials were retrieved |
| software-defined-storage.instance.get | S3 Cert status was retrieved |
| software-defined-storage.instance.create | S3 TLS certificate was created |
| software-defined-storage.volume.create | The volume was created |
| software-defined-storage.volume.read | One or more volumes were retrieved |
| software-defined-storage.volume.update | The volume was updated |
| software-defined-storage.volume.delete | The volume was deleted |
| software-defined-storage.host.create | The host was created |
| software-defined-storage.host.read | One or more hosts were retrieved |
| software-defined-storage.host.delete | The host was deleted |
| software-defined-storage.volumemap.create | The volume was mapped |
| software-defined-storage.volumemap.delete | The volume was unmapped |
{: caption="Actions that generate management events" caption-side="bottom"}
