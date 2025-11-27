---

copyright:
 years: 2024, 2025
lastupdated: "2025-11-27"

keywords: cephaas csi set up

subcollection: cephaas

---

{{site.data.keyword.attribute-definition-list}}

# CSI driver set up and installation
{: #csi-setup}

Before installing the driver, complete the following preinstallation setup activities:

1. Make sure the following tools are installed on your system before the CSI driver installation. 

    * Docker
    * Helm CLI

2. Login to the IBM Cloud Container Registry via HELM by running the following command:

```sh
    helm registry login icr.io -u iamapikey -p <your-api-key> 
```
{: codeblock}

    When prompted, enter your IBM Cloud API key as the password.

3. Create local copy of **values.yaml** file and edit the required fields using the following command:

    ```
    helm show values  oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>  > values.yaml
   ```
{: codeblock}

    Here is an example. 

    ```
    helm show values  oci://icr.io/cephaas-helm-charts/cephaas-csi --version 1.0.0 > values.yaml
    ```
{: codeblock}


4. Create a Secret using the following command: 

    ```
    oc create secret docker-registry <secret-name> \
        --docker-server=icr.io \
        --docker-username=<your-username> \
        --docker-password=<your-password-or-api-key>
     ```
{: codeblock}
   
    Create the secret in the same namespace where the CSI driver will be installed. 
    {: note}

5. Edit the following parameters in the **values.yaml**. 

    * Add csiConfig.Deployment details in this format `https://<deployment-url>`
    * Update externalSnapshotter.enabled to true
    * Update LicenseAccepted as true
    * Add your API Key in csiSecret.Token
    * Add secret name created in previous step under imagePullSecrets.name. 

6. To view the chart metadata, README, and values.yaml of a Helm chart, run the following commands:

```sh
    helm show chart oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>
    helm show readme oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>
    helm show values oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>
```
{: codeblock}

     You can view the chart details, including license information, by running the command:
    `helm show chart oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>`
    {: note}


7. Before installing the chart, you can optionally review the rendered Kubernetes manifest files generated from the values.yaml using the following command. 

```sh
    helm template cephaas-csi oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here> -f values.yaml
```
{: codeblock}

8. Install the CSI driver using the Helm chart and your updated **values.yaml** file.

```sh
   helm install cephaas-csi oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>  -f values.yaml  --namespace <your-namespace>
```
{: codeblock}
    
To verify that the CSI driver was installed successfully, run the command `helm status <chart-name> --namespace <your-namespace>`.
{: note}

When deploying the CSI driver on OpenShift, you may encounter PodSecurity violation warnings, which can cause the CSI driver installation to fail.
These warnings occur because the CSI driver requires elevated permissions, including:

- privileged: true
- hostNetwork: true
- hostPath volumes

To resolve this, you must grant the appropriate Security Context Constraints (SCCs) to the CSI driver service accounts after deploying the driver:

```sh
oc adm policy add-scc-to-user privileged -z cephaascsi-node-sa -n <your-namespace>
oc adm policy add-scc-to-user privileged -z cephaascsi-controller-sa -n <your-namespace>
```
{: codeblock}


This ensures the CSI driver pods have the necessary permissions to start successfully on OpenShift.


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
