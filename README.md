This document will describe how to install Kubernetes Event Exporter on IBM Cloud using Kubernetes services.

**Step 1 - provision Kubernetes Cluster**

- Click the **Catalog** button on the top
- Select **Service** from the **Catalog**
- Search for **Kubernetes Service** and click on it

![Kubernetes Event Exporter_html_46d1c04e26ba5eea](https://user-images.githubusercontent.com/5286796/106395901-d0d5ab00-642a-11eb-9e44-01e69e7fd5d9.png)

- You are now at the Kubernetes deployment page. You need to specify some information about the cluster.

- Choose either of the following plans; **standard** or **free**. The free plan only have one worker node and no subnet. To provision a standard cluster. You will need to upgrade your account to Pay-As-You-Go
- To upgrade to a Pay-As-You-Go account, complete the following steps:
- In the console, go to Manage > Account.
- Select Account settings and click `Add credit card`.
- Enter your payment information, click Next, and submit your information
- Choose **classic** or **VPC** , read the docs and choose the most suitable type for yourself

![Kubernetes Event Exporter_html_4d3a968071544952](https://user-images.githubusercontent.com/5286796/106395900-cfa47e00-642a-11eb-812a-92c17872b42d.png)

- Now choose your location settings,
- Choose **Geography** (continent)

![Kubernetes Event Exporter_html_72496e6b0b2c820d](https://user-images.githubusercontent.com/5286796/106395899-ce735100-642a-11eb-9784-98168da06b29.png)

- Choose Single or Multizone. 

> In single zone, your data is only kept on the datacenter while on the other hand with Multizone, it is distributed to multiple zones, thus safer in an unforeseen zone failure
>
> If you wish to use Multizone, please set up your account with VRF
> 

- If at your current location selection, there is no available Virtual LAN, a new VLAN will be created for you
- Choose a Worker node setup or use the preselected one. SSet Worker node amount per zone
- Choose **Master Service Endpoint**. 
- 
> In VRF-enabled accounts, you can choose private-only to make your master accessible on the private network or via VPN tunnel. Choose public-only to make your master publicly accessible. When you have a VRF-enabled account, your cluster is set up by default to use both private and public endpoints.
   
- Give desired **tags** to your cluster, for more information visit tags
- Click **create**
- Wait for your cluster to be provisioned
- Your cluster is ready for usage

**Step 2 Deploy IBM Cloud Block Storage plug-in**

The Block Storage plug-in is a persistent, high-performance iSCSI storage that you can add to your apps by using Kubernetes Persistent Volumes (PVs).

- Click the **Catalog** button on the top
- Select **Software** from the catalog
- Search for **IBM Cloud Block Storage plug-in** and click on it
- On the application page, click in the dot next to the cluster you wish to use
- Click on Enter or Select Namespace and choose the default Namespace or use a custom one (if you get error please wait 30 minutes for the cluster to finalize)
- Give a **name** to this workspace
- Click **install** and wait for the deployment

# **Step 3 **Installing **Kubernetes Event Exporter**

## Introduction

This chart bootstraps a Kubernetes Event Exporter deployment on a Kubernetes cluster using the Helm package manager.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.1.0

## **Installing the Chart**

To install the chart with the release name my-release:

```sh
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm install my-release bitnami/kubernetes-event-exporter
```

These commands deploy Kubernetes Event Exporter on the Kubernetes cluster in the default configuration. The [Parameters](https://hub.kubeapps.com/#%23parameters) section lists the parameters that can be configured during installation.

## **Uninstalling the Chart**

To uninstall/delete the my-release deployment:

```sh
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

**Kubernetes Event Exporter parameters**


 

| **Parameter**       | **Description**                                              | **Default**                                                  |      |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| config.logFormat    | How 			the logs are formatted. Allowed values: pretty or json | pretty                                                       |      |
| config.logLevel     | Verbosity 			of the logs (options: fatal, error, warn, info or debug) | debug                                                        |      |
| config.receivers    | Array 			containing event receivers                 | [ 			{"name": "dump", "file": { "path": 			"/dev/stdout" }} ] |      |
| Config.route.routes | Array 			containing event route configuration       |                                                              |      |


 
