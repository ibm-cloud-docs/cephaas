---

copyright:
 years: 2024, 2024
lastupdated: "2024-09-19"

keywords: cephaas activity tracker events

subcollection: sdsaas

---
{{site.data.keyword.attribute-definition-list}}

# Activity Tracking events for {{site.data.keyword.cephaas_short}}
{: #sds-at}

Use the {{site.data.keyword.cloud_notm}} Activity Tracker service to track events performed on your resources. You can use these services to investigate abnormal activity and critical actions and comply with regulatory audit requirements and to provide a record of what is happening with your resources.

The Activity Tracker service records user-initiated activities that change the state of a service in IBM Cloud. To start monitoring your user's actions, see [Getting started with Activity Tracker](docs/activity-tracker?topic=activity-tracker-getting-started).

## List of management events
{: #sds-list-management-events}

The following table lists the actions that generate an event:

| Action   | Description                                      |
|:---------|:-------------------------------------------------|
| software-defined-storage.volume.create | |
| software-defined-storage.volume.read | |
| software-defined-storage.volume.update | |
| software-defined-storage.volume.delete | |
| software-defined-storage.host.create | |
| software-defined-storage.host.read | |
| software-defined-storage.host.delete | |
| software-defined-storage.volumemap.create | |
| software-defined-storage.volumemap.delete | |
{: caption="Table 1. List of management events" caption-side="top"}

## List of instance events
{: #sds-list-instance-events}

The following table lists the actions that generate an event:

| Action   | Description                                      |
|:---------|:-------------------------------------------------|
| software-defined-storage.instance.create |   |
| software-defined-storage.instance.update |   |
| software-defined-storage.instance.delete |   |
| software-defined-storage.instance.last_operation_get | |
{: caption="Table 1. List of instance events" caption-side="top"}


## List of object events
{: #sds-list-object-events}

The following table lists the actions that generate an event:

| Action   | Description                                      |
|:---------|:-------------------------------------------------|
| software-defined-storage.account.create | |
| software-defined-storage.account.delete | |
| software-defined-storage.account.get | |
| software-defined-storage.instance.get | |
| software-defined-storage.instance.create | |
{: caption="Table 1. List of objects events" caption-side="top"}



## Enabling events
{: #sds-enabling-events}

Some services require a paid plan or more configuration to enable events. Add any information on how to allow the customer to enable the collection of events.

### Enabling events through the UI
{: #sds-enabling-events-ui}

1.	From the IBM Cloud console [resource list](https://cloud.ibm.com/resources), select the service instance that you are interested in adding for event tracking. This takes you to the CephaaS Storage Console.
2.	Choose the Deployment for which you want to enable event tracking.
3.	Go to the configuration tab.
4.	Scroll down to the advanced configuration section and toggle the events you want to track for this bucket.
5.	After a few minutes, any activity will be visible in the Activity Tracker web UI.

### Enabling events by using the command line
{: #sds-enabling-events-cli}



### Enabling events by using an API call
{: #sds-enabling-events-api}

[To do] Add an example of a cURL command that also includes any headers like authorization headers that might be required.


## Viewing events
{: #sds-view-events}

You can view the Activity Tracker events that are associated with your Storage deployment by using [IBM Cloud Activity Tracker](/docs/activity-tracker?topic=activity-tracker-getting-started).

To view events, you must identify the location where events are collected and available for monitoring. Then, you must access the web UI of the IBM Cloud Activity Tracker instance in that location. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/activity-tracker?topic=activity-tracker-observe).




## Analyzing events
{: #sds-analyze-events}

[TO DO] Add information on custom fields that are included in `requestData` and `responseData` fields and that can help users understand your events.
