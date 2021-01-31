# Installing Kubernetes Event Exporter on IBM Cloud

# *Step 1 provision Kubernetes Cluster*

- Click the **Catalog** button on the top

- Select **Service** from the **Catalog**

- Search for **Kubernetes Service** and click on it

  ![Kubeapps_newdoc_html_46d1c04e26ba5eea](https://user-images.githubusercontent.com/5286796/106395222-0d9fa300-6427-11eb-9100-bf270bedfdb4.png)

- You are now at the Kubernetes deployment page. You need to specify some details about the cluster

- Choose a plan **standard** or **free** , the free plan only has one worker node and no subnet, to provision a standard cluster, you will need to upgrade your account to Pay-As-You-Go

- To upgrade to a Pay-As-You-Go account, complete the following steps:

- In the console, go to Manage > Account.

- Select Account settings; and click Add credit card.

- Enter your payment information, click Next, and submit your information

- Choose **classic** or **VPC** , read the docs and choose the most suitable type for yourself

  ![Kubeapps_newdoc_html_4d3a968071544952](https://user-images.githubusercontent.com/5286796/106395219-0c6e7600-6427-11eb-99e4-fb7c5d0c5d5e.png)

- Now choose your location settings,

- Choose **Geography** (continent)

![Kubeapps_newdoc_html_72496e6b0b2c820d](https://user-images.githubusercontent.com/5286796/106395218-0aa4b280-6427-11eb-9589-6638903ae4ff.png)

-   Choose 	Single or Multizone, in single zone your data is only kept in on 	datacenter, on the

​      other hand with Multizone it is distributed to multiple zones, thus safer in an unforeseen

​      zone failure

- If you wish to use Multizone please set up your account with[VRF

- If at your current location selection, there is no available Virtual LAN, a new VLAN will be created for you
- Choose a Worker node setup or use the preselected one, set Worker node amount per zone
- Choose **Master Service Endpoint**. In VRF-enabled accounts, you can choose private-only to make your master accessible on the private network or via VPN tunnel. Choose public-only to make your master publicly accessible. When you have a VRF-enabled account, your cluster is set up by default to use both private and public endpoints.
   Give desired **tags** to your cluster, for more information visit tags
- Click **create**
   • Wait for your cluster to be provisioned
   • Your cluster is ready for usage

**Step 2 Deploy IBM Cloud Block Storage plug-in**

The Block Storage plug-in is a persistent, high-performance iSCSI storage that you can add to your apps by using Kubernetes Persistent Volumes (PVs).

- Click the **Catalog** button on the top
- Select **Software** from the catalog
- Search for **IBM Cloud Block Storage plug-in** and click on it
   • On the application page Click in the dot next to the cluster, you wish to use
   • Click on Enter or Select Namespace and choose the default Namespace or use a custom one (if you get error please wait 30 minutes for the cluster to finalize)
- Give a **name** to this workspace
- Click **install** and wait for the deployment

# **Step 3 Installing Kubeapps on IBM Cloud**

## **Install Kubeapps**

Use the Helm chart to install the latest version of Kubeapps:

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
kubectl create namespace kubeapps
helm install kubeapps --namespace kubeapps bitnami/kubeapps
```

The above commands will deploy Kubeapps into the kubeapps namespace in your cluster. It may take a few minutes to execute. 

You can check the status of the deployment using the command below:

```sh
kubectl get pods -w --namespace kubeapps
```

Once it has been deployed and the Kubeapps pods are running, continue to another step.

##  **Create a demo credential with which to access Kubeapps and Kubernetes**

You can create a Kubernetes service account and use the API token to authenticate with the Kubernetes API server via Kubeapps:

```sh
kubectl create serviceaccount kubeapps-operator
kubectl create clusterrolebinding kubeapps-operator --clusterrole=cluster-admin --serviceaccount=default:kubeapps-operator
```

## **Start the Kubeapps Dashboard**

Once Kubeapps is installed, securely access the Kubeapps Dashboard from your system by running:

```sh
kubectl port-forward -n kubeapps svc/kubeapps 8080:80
```

# Deploy an application with Kubeapps

Once you have the Kubeapps Dashboard up and running, you can start deploying applications into your cluster.

- Start with the Dashboard welcome page
- Use the "Catalog" menu to select an application from the list of available charts
- Click the "Deploy" button
- You can customize the deployment by editing the form or YAML configuration file. Click "Deploy" to proceed
- The application will now be deployed. You will be able to track the new Kubernetes deployment directly from the browser


