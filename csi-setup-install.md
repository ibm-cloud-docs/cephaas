---

copyright:
 years: 2024, 2025
lastupdated: "2025-09-23"

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
    * IBM Cloud Container Registry

2. Login to the IBM Cloud Container Registry via HELM by running the following command:

    ```sh
    helm registry login icr.io -u iamapikey -p <your-api-key> 
    ```
    {: pre}

    When prompted, enter your IBM Cloud API key as the password.

3. Create local copy of values.yaml file and edit the required fields using the following command:

    ```sh
    helm show values oci://icr.io/cephaas-dev-container-images/csi-driver-helm-dev/cephaas-csi --version <specify-tag-here>  > values.yaml
    ```
    {: pre}

    Here is an example. 

    ```sh
    helm show values oci://icr.io/cephaas-dev-container-images/csi-driver-helm-dev/cephaas-csi --version 1.0.0-2025265-1758523414-main-3b6de8a > values.yaml
    ```
    {: pre}

4. Create a Secret using the following command: 

    ```sh
    oc create secret docker-registry <secret-name> \
        --docker-server=icr.io \
        --docker-username=<your-username> \
        --docker-password=<your-password-or-api-key>
    ```
    {: pre}

5. Edit the following parameters in the values.yaml. 

    * Add csiConfig.Deployment details in this format `https://<deployment-url>`
    * Update externalSnapshotter.endabled to true
    * Update LicenseAccepted as true
    * Add your API Key in csiSecret.Token
    * Secret

6. You can optionally view the chart metadata, README file, and values.yaml file using the following commands. 

    ```sh
    helm show chart oci://icr.io/cephaas-dev-container-images/csi-driver-helm-dev/cephaas-csi --version <specify-tag-here>
    helm show readme oci://icr.io/cephaas-dev-container-images/csi-driver-helm-dev/cephaas-csi --version <specify-tag-here>
    helm show values oci://icr.io/cephaas-dev-container-images/csi-driver-helm-dev/cephaas-csi --version <specify-tag-here>
    ```
    {: pre}

7. Before installing the chart, review the rendered Kubernetes manifest files generated from the values.yaml using the following command. 

    ```sh
    helm template cephaas-csi oci://icr.io/cephaas-dev-container-images/csi-driver-helm-dev/cephaas-csi --version <specify-tag-here> -f values.yaml
    ```
    {: pre}

8. Install the CSI driver using the Helm chart and your updated values.yaml file.

    ```sh
    helm install cephaas-csi oci://icr.io/cephaas-dev-container-images/csi-driver-helm-dev/cephaas-csi --version <specify-tag-here> -f values.yaml
    ```
    {: pre}


To verify that the CSI driver was installed successfully, run the command `helm status <chart-name>`.
{: note}
