---

copyright:
 years: 2024, 2025
lastupdated: "2025-07-28"

keywords: cephaas settings, creating S3 Certificate, ceph as a service

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}


# Upgrading the vSphere plug-in
{: #upgrade-vsphere-plugin}

This topic describes how to upgrade an existing installation of the {{site.data.keyword.cephaas_full}} plug-in for vSphere, ensuring continued compatibility and access to the latest features and improvements.

## About the upgrade process
{: #about-upgrade-process}

This procedure will upgrade the plug-in from version 1.1.x.x to 1.3.0.0.

The upgrade package will be in the format e.g. ibm-storage-ceph-as-a-service-plugin-upgrade-2024_06-XX-XXXX.tar.gz.
{: note}

## Upgrade procedure steps
{: #steps-upgrade-process}

The following steps guide you through upgrading the {{site.data.keyword.cephaas_full}} plug-in for vSphere using a manual package installation method. This process involves downloading the upgrade package, transferring it to the plug-in appliance, and executing the installation using the provided utility.

1. Download the specific upgrade package from Fix Central to your local server or laptop.
2. Securely copy the upgrade package to the plug-in appliance using a tool such as scp to the /tmp directory of the appliance.
3. Install the package file on the plug-in appliance using ibm-install /tmp/ibm-storage-ceph-as-a-service-plugin-upgrade-2024_06_XX-XXXX.tar.gz

If a storage system configured in an enhanced stretch cluster has been previously added through the 1.2 plug-in with pools only from one site, then you must add pools from other sites as well after upgrading to the 1.3 plug-in to be able to provision new storage (create a datastore). 
{: note}

## What to do next
{: #whatnext-after-upgrade}

After the plug-in is successfully deployed, a successful deployment message appears in both a banner as well as within a temporary notification. In addition, in **Recent Tasks** there are now tasks for both Download plug-in and Deploy plug-in with Completed status.

Click **REFRESH BROWSER** on the banner, to complete the plug-in activation.

Refreshing the browser is necessary in order to ensure the plug-in activation.
{: important}

