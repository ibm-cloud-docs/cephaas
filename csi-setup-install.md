---

copyright:
 years: 2024, 2025
lastupdated: "2025-10-01"

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

    ```
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

    Add secret name created in previous step under imagePullSecrets.name. 

4. Create a Secret using the following command: 

    ```
    oc create secret docker-registry <secret-name> \
        --docker-server=icr.io \
        --docker-username=<your-username> \
        --docker-password=<your-password-or-api-key>
     ```
{: codeblock}

5. Edit the following parameters in the **values.yaml**. 

    * Add csiConfig.Deployment details in this format `https://<deployment-url>`
    * Update externalSnapshotter.endabled to true
    * Update LicenseAccepted as true
    * Add your API Key in csiSecret.Token
    * Secret name created in the previous step

6. You can view the license information of a Helm chart by running the command `helm show chart <chart-name>`.

    ```
    helm show chart oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>
    helm show readme oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>
    helm show values oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>
     ```
{: codeblock}

    You can view the chart details, including license information, by running the following command: `helm show chart oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>>`.
    {: note}

7. Before installing the chart, you can optionally review the rendered Kubernetes manifest files generated from the values.yaml using the following command. 

    ```
    helm template cephaas-csi oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here> -f values.yaml
     ```
{: codeblock}

8. Install the CSI driver using the Helm chart and your updated **values.yaml** file.

    ```
    
   helm install cephaas-csi oci://icr.io/cephaas-helm-charts/cephaas-csi --version <specify-tag-here>  -f values.yaml  --namespace <your-namespace>
    ```
{: codeblock}


    To verify that the CSI driver was installed successfully, run the command `helm status <chart-name> --namespace <your-namespace>`.
    {: note}
