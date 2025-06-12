<!-- markdownlint-disable MD033 -->
<p align="center">
  <a href="https://www.boldbi.com?utm_source=github&utm_medium=backlinks">
    <img src="https://cdn.boldbi.com/DevOps/boldbi-logo.svg" alt="Bold BI" width="400"/>
  </a>
</p>

<p align="center">
  <a href="https://github.com/boldbi/boldbi-kubernetes/releases/latest">
    <img src="https://img.shields.io/github/v/release/boldbi/boldbi-kubernetes?sort=semver" alt="GitHub release"/>
  </a>
  <a href="https://help.boldbi.com/embedded-bi?utm_source=github&utm_medium=backlinks">
    <img src="https://img.shields.io/badge/docs-help.boldbi.com-blue.svg" alt="Documentation"/>
  </a>
  <a href="https://www.boldbi.com/support?utm_source=github&utm_medium=backlinks">
    <img src="https://img.shields.io/badge/file_issues-boldbi_support-blue.svg" alt="File Issues"/>
  </a>
</p>

---

# 🚀 Bold BI on Kubernetes

**Bold BI** is an advanced **business intelligence and dashboarding platform** that enables you to visualize data, build interactive dashboards, and embed analytics seamlessly within your applications.

---

## 📋 Prerequisites

To deploy Bold BI in a Kubernetes cluster, ensure you have the following:

### ⚙️ Infrastructure
| Component             | Requirement |
|----------------------|-------------|
| **Kubernetes**       | Version `1.29+` |
| **Cloud Providers**  | EKS / GKE / AKS / ACK / OKE / On-Prem |
| **Node OS**          | Ubuntu |
| **Min. Node Count**  | 2 |
| **Node Config**      | 2 CPU, 8 GB RAM, 20 GB Disk |
| **Storage**          | 10+ GB ReadWriteMany (e.g., AWS EFS, Azure Files, GCP Filestore) |

### 📦 Tooling
| Tool             | Notes |
|------------------|-------|
| **kubectl**      | Required |
| **Helm**         | Required |
| **Cloud CLI**    | AWS CLI / Azure CLI / GCP CLI / Oracle CLI / Alibaba CLI |
| **Web Browser**  | Chrome / Edge / Firefox |
| **Database**     | PostgreSQL 13+ / SQL Server 2016+ / MySQL 8.0+ / Oracle 19c+ |

---

## 🚀  **Deploy Using Helm**

> Helm offers a highly configurable and repeatable way to deploy Bold BI in Kubernetes. This is the recommended approach for production environments.

This chart installs [Bold BI](https://www.boldbi.com/) on Kubernetes. You can create Kubernetes cluster in cloud cluster providers(GKE,AKS and EKS). Please follow the below documentation for Bold BI deployment in a specific cloud environments.
    
#### Deployment prerequisites

* [Install Helm](https://helm.sh/docs/intro/install/) to deploy Bold BI using Helm.
* [Install Kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
* [File Storage](docs/pre-requisites.md#file-storage)
* [Create and connect a cluster](docs/pre-requisites.md#create-a-cluster)
* [Load Balancing](docs/pre-requisites.md#load-balancing)

> **Note:** Note the [Ingress IP address](docs/pre-requisites.md#get-ingress-ip) and map it with a DNS to crafting values.yaml when installing Bold BI with helm chart.

## Get Repo Info

1. Add the Bold BI helm repository

```console
helm repo add boldbi https://boldbi.github.io/boldbi-kubernetes
helm repo update
```

2. View charts in repo

```console
helm search repo boldbi

NAME            CHART VERSION   APP VERSION     DESCRIPTION
boldbi/boldbi   12.1.5           12.1.5         Embed powerful analytics inside your apps and t...
```

_See [helm repo](https://helm.sh/docs/helm/helm_repo/) for command documentation._

## 🛠️ Install Helm Chart

To deploy **Bold BI** using Helm, start by customizing a `values.yaml` file specific to your cloud provider.

> 📌 **Download the appropriate configuration file below:**

| Cloud Provider | Configuration File |
|----------------|--------------------|
| ☁️ **Google Kubernetes Engine (GKE)** | [`gke-values.yaml`](https://raw.githubusercontent.com/boldbi/boldbi-kubernetes/main/helm/custom-values/gke-values.yaml) |
| ☁️ **Amazon Elastic Kubernetes Service (EKS)** | [`eks-values.yaml`](https://raw.githubusercontent.com/boldbi/boldbi-kubernetes/main/helm/custom-values/eks-values.yaml) |
| ☁️ **Azure Kubernetes Service (AKS)** | [`aks-values.yaml`](https://raw.githubusercontent.com/boldbi/boldbi-kubernetes/main/helm/custom-values/aks-values.yaml) |
| ☁️ **Oracle Kubernetes Engine (OKE)** | [`oke-values.yaml`](https://raw.githubusercontent.com/boldbi/boldbi-kubernetes/main/helm/custom-values/oke-values.yaml) |

---

<table>
    <tr>
      <td>
       <b>Name</b>
      </td>
      <td>
       <b>Description</b>
      </td>
    </tr>
    <tr>
      <td>
       namespace
      </td>
      <td>
       The namespace in which the Bold BI resources will be deployed in the kubernetes cluster.<br/>
       The default namespace is <i>bold-services</i>
      </td>
    </tr>
    <tr>
      <td>
       appBaseUrl *
      </td>
      <td>
       Domain with http/https protocol. Follow the <a href='docs/configuration.md#ssl-configuration'>SSL Configuration</a> to configure SSL certificate for https protocol after deploying Bold BI in your cluster.
      </td>
    </tr>
    <tr>
      <td>
       optionalLibs
      </td>
      <td>
       These are the client libraries used in Bold BI by default.<br/>
       '<i>mongodb,mysql,influxdb,snowflake,oracle,google,clickhouse</i>'<br/>
       Please refer to <a href='docs/configuration.md#client-libraries'>Optional Client Libraries</a> section to know more.
      </td>
    </tr>
    <tr>
      <td>
       clusterProvider
      </td>
      <td>
       The type of kubernetes cluster provider you are using.<br/>
       The recommended values are '<i>gke,eks and aks</i>'
      </td>
    </tr>
    <tr>
      <td>
       persistentVolume *
      </td>
      <td>
       Please refer to <a href='docs/configuration.md#persistent-volume'>this</a> section to know more on how to set Persistant Volumes for Bold BI.
      </td>
    </tr>
    <tr>
      <td>
       loadBalancer
      </td>
      <td>
       Currently we have provided support for Nginx and Istio as Load Balancers in Bold BI. Please refer to <a href='docs/configuration.md#load-balancing'>this</a> section for configuring Load balancer for Bold BI.
      </td>
    </tr>
    <tr>
      <td>
       autoscaling
      </td>
      <td>
       By default autoscaling is enabled in Bold BI. Please refer to <a href='docs/configuration.md#auto-scaling'>this</a> section to configure autoscaling in Bold BI.
      </td>
    </tr>
    <tr>
      <td>
       bingMapWidget
      </td>
      <td>
       Please refer to <a href='docs/configuration.md#bing-map-widget'>this</a> section to configure Bing Map Widget in Bold BI.
      </td>
    </tr>
    <tr>
      <td>
       customLocalePath
      </td>
      <td>
       Custom locale file path for Localization.
      </td>
    </tr>
        <tr>
      <td>
       customSizePdfExport
      </td>
      <td>
       To utilize a customized page size for A4 PDF export, set this feature to true. By default, this feature is set to false.
      </td>
    </tr>
        <tr>
      <td>
       browserTimeZone
      </td>
      <td>
       If you need to use Browser time zone feature , enable this to true. By default this feature will be set to false. 
      </td>
    </tr>
        <tr>
      <td>
       useSiteIdendifier
      </td>
      <td>
       The variable is optional, and the default value is TRUE. 
          By default, all sites in Bold BI require a site identifier, which differentiates sites on the same domain. That is https://example.com/bi/site/<site_identifier>
          You can ignore the site identifier by setting the value as FALSE. If the site identifier is disabled, each site requires a unique domain.
      </td>
    </tr>
        <tr>
      <td>
       AppSettings__EnableQueryMetricsInDebugFiles
      </td>
      <td>
       If the query metrics needs to be logged in debug files, enable this to true. By default, this option is set to false.
      </td>
    </tr>
        <tr>
      <td>
       AppSettings__EnableQueryMetricsWithQueryInDebugFiles
      </td>
      <td>
       If the query and query metrics needs to be logged in debug files, enable this to true. By default, this option is set to false.
      </td>
    </tr>
    </tr>
        <tr>
      <td>
       azureApplicationInsights:<br />
       connectionString: ""
      </td>
      <td>
       Integrating Azure Application Insights with Bold BI Enterprise Edition enables you to track and visualize your application’s performance, detect issues, and enhance your application’s overall reliability.
      </td>
    </tr>
        <tr>
      <td>
       tolerationEnable: false<br />
       tolerations:
      </td>
      <td>
       Tolerations allow the pods to be scheduled into nodes with matching taints. Set this to true if you use tolerations in your cluster. If you need more than one toleration, you can add multiple tolerations below.
      </td>
    </tr>
        <tr>
      <td>
       nodeAffinityEnable: false<br />
       nodeAffinity:
      </td>
      <td>
       Node affinity ensures that the pods are scheduled into nodes with matching labels. Set this to true if you use node affinity in your cluster.
      </td>
    </tr>
        <tr>
      <td>
         podAffinityEnable: false
      </td>
      <td>
        Pod affinity ensures that the pods are scheduled into nodes with matching pods. Set this to true if you use pod affinity in your cluster
      </td>
    </tr>
        <tr>
      <td>
         podAntiAffinityEnable: false
      </td>
      <td>
        Pod anti-affinity ensures that the pods are not scheduled into nodes with matching pods. Set this to true if you use pod anti-affinity in your cluster.
      </td>
    </tr>
    </table>
<br/>

## Environment variables for configuring Application Startup in backend

The following environment variables are optional. If not provided, a manual Application Startup configuration is needed.

<table>
    <tr>
      <td>
       <b>Name</b>
      </td>
      <td>
       <b>Description</b>
      </td>
    </tr>
    <tr>
      <td>
       licenseKey
      </td>
      <td>
       License key of Bold BI
      </td>
    </tr>
    <tr>
      <td>
       email *
      </td>
      <td>
       It should be a valid email.
      </td>
    </tr>
    <tr>
      <td>
       password *
      </td>
      <td>
       It should meet our password requirements. <br /> <br />Note: <br />Password must meet the following requirements. It must contain,At least 6 characters, 1 uppercase character, 1 lowercase character, 1 numeric character, 1 special character
      </td>
    </tr>
    <tr>
      <td>
       dbType *
      </td>
      <td>
       Type of database server can be used for configuring the Bold BI.<br/><br />The following DB types are accepted:<br />1. mssql – Microsoft SQL Server/Azure SQL Database<br />2. postgresql – PostgreSQL Server<br />3. mysql – MySQL/MariaDB Server
      </td>
    </tr>
    <tr>
      <td>
       dbHost *
      </td>
      <td>
       Name of the Database Server
      </td>
    </tr>
    <tr>
      <td>
       dbPort
      </td>
      <td>
       The system will use the following default port numbers based on the database server type.<br />PostgrSQL – 5432<br />MySQL -3306<br /><br />Please specify the port number for your database server if it is configured on a different port.<br /><br />For MS SQL Server, this parameter is not necessary.
      </td>
    </tr>
    <tr>
      <td>
       dbUser *
      </td>
      <td>
       Username for the database server<br /><br />Please refer to [this documentation](https://help.boldbi.com/embedded-bi/faq/what-are-the-database-permissions-required-to-set-up-bold-bi-embedded/) for information on the user's permissions.
      </td>
    </tr>
    <tr>
      <td>
       dbPassword *
      </td>
      <td>
       The database user's password
      </td>
    </tr>
    <tr>
      <td>
       dbName
      </td>
      <td>
       If the database name is not specified, the system will create a new database called bold-services.<br /><br />If you specify a database name, it should already exist on the server.
      </td>
    </tr>
    <tr>
      <td>
       maintenanceDB
      </td>
      <td>
       For PostgreSQL DB Servers, this is an optional parameter.<br />The system will use the database name `postgres` by default.<br />If your database server uses a different default database, please provide it here.
      </td>
    </tr>
    <tr>
      <td>
       dbAdditionalParameters
      </td>
      <td>
       If your database server requires additional connection string parameters, include them here.<br /><br />Connection string parameters can be found in the official document.<br />My SQL: https://dev.mysql.com/doc/connector-net/en/connector-net-8-0-connection-options.html<br />PostgreSQL: https://www.npgsql.org/doc/connection-string-parameters.html<br />MS SQL: https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring<br /><br /><b>Note:</b> A semicolon(;) should be used to separate multiple parameters.
      </td>
    </tr>
    <tr>
      <td>
       dbSchema
      </td>
      <td>
       A database schema defines the structure, organization, and constraints of data within a database, including tables, fields, relationships, and indexes<br /><br />In MSSQL, the default schema is dbo.<br />
       In PostgreSQL, the default schema is public.<br /><br />
       Both schemas contain tables and other database objects by default.
      </td>
    </tr>
</table>
<br/>

## Environment variables for configuring Branding in backend

The following environment variables are optional. If they are not provided, Bold BI will use the default configured values.

<table>
   <tr>
      <td>
       <b>Name</b>
      </td>
      <td>
       <b>Description</b>
      </td>
    </tr>
    <tr>
      <td>
       mainLogo
      </td>
      <td>   
       This is header logo for the applicationand the preferred image size is 40 x 40 pixels.
      </td>
    </tr>
    <tr>
      <td>
       loginLogo
      </td>
      <td>     
       This is login logo for the application and the preferred image size is 200 x 40 pixels.
      </td>
    </tr>
    <tr>
      <td>
       emailLogo
      </td>
      <td>     
       This is email logo, and the preferred image size is 200 x 40 pixels.
      </td>
    </tr>
    <tr>
      <td>
       favicon
      </td>
      <td>     
       This is favicon and the preferred image size is 40 x 40 pixels. 
      </td>
    </tr>
    <tr>
      <td>
       footerLogo
      </td>
      <td>     
       This is powered by logo and the preferred size is 100 x 25 pixels.
       <br />
       <br />
       <b>Note:</b><br/>• All the branding variables are accepted as URL.<br/>• <b>Ex:</b> https://example.com/loginlogo.jpg <br/>• <b>Image type:</b> png, svg, jpg, jpeg.<br/>• If you want to use the custom branding, provide the value for all branding variables If all variable values are given, application will use the branding images, otherwise it will take the default logos. 
      </td>
    </tr>
    <tr>
      <td>
       siteName
      </td>
      <td>
      This is organization name.     
      <br />
       If the value is not given, the site will be deployed using the default name.
      </td>
    </tr>
    <tr>
      <td>
       siteIdentifier
      </td>
      <td>     
       This is site identifier, and it will be the part of the application URL.
      <br />
      If the value is not given, the site will be deployed using the default value.
      </td>
    </tr>
</table>
<br/>


> **Note:** Items marked with `*` are mandatory fields in values.yaml

Run the following command to delpoy Bold BI in your cluster.

```console
helm install [RELEASE_NAME] boldbi/boldbi -f [Crafted values.yaml file]
```
Ex:  `helm install boldbi boldbi/boldbi -f my-values.yaml`

Refer [here](docs/configuration.md) for advanced configuration including SSL termination, optional client libraries, etc.

_See [helm install](https://helm.sh/docs/helm/helm_install/) for command documentation._

## Upgrade

- Run the following command to get the latest version of Bold BI helm chart.

  ```console
  helm repo update
  ```

- Create a new YAML file or update the existing one with changes such as a new image tag, environment variables, and other configuration details. You can access the latest updated YAML file from the location below:

  [boldbi/values.yaml](https://raw.githubusercontent.com/boldbi/boldbi-kubernetes/main/helm/boldbi/values.yaml)

- Run the below command to apply changes in your Bold BI release or upgrading Bold BI to latest version.

  ```console
  helm upgrade [RELEASE_NAME] boldbi/boldbi -f [Crafted values.yaml file]
  ```

  Ex:  `helm upgrade boldbi boldbi/boldbi -f my-values.yaml`

## Uninstall Chart

```console
helm uninstall [RELEASE_NAME]
```
Ex:  `helm uninstall boldbi`

This removes all the Kubernetes components associated with the chart and deletes the release.

_See [helm uninstall](https://helm.sh/docs/helm/helm_uninstall/) for command documentation._

## Application Startup

Configure the Bold BI On-Premise application startup to use the application. Please refer the following link for more details on configuring the application startup.
    
https://help.boldbi.com/embedded-bi/application-startup


---

## ⚙️ Advanced Deployment Options

> For users who require fine-grained control using raw manifests or need to deploy combined components.

- 📘 [**Deploy Bold BI using kubectl**](docs/index.md)  
  Manual deployment using raw YAML files and `kubectl`.

- 📘 [**Common Deployment (BI + Reports) using Helm**](helm/bold-common/README.md)  
  Unified Helm chart to deploy both Bold BI and Bold Reports together.
"""

## 📚 Frequently Asked Questions (FAQ)

- [🔄 How to auto-deploy Bold BI in Kubernetes](docs/bold-bi-auto-deployment.md)  
- [🔐 SSL setup with cert-manager](docs/FAQ/how-to-manually-configure-ssl-using-cert-manger-in-bold-bi-kubernetes-deployment.md)  
- [🔗 Deploy Bold BI in EKS with NLB + ACM SSL](docs/FAQ/how-deploy-bold-bi-in-eks-using-network-load-balancer-with-ssl-certificate-from-acm.md)  
- [🌀 Deploy in EKS using ALB](docs/FAQ/how-to-deploy-bold-bi-in-eks-using-application-load-balancer.md)  
- [☁️ Deploy Bold BI in Alibaba ACK](docs/FAQ/how-to-deploy-bold-bi-in-an-ack-cluster.md)  
- [📦 Deploy Bold BI + Reports in Alibaba ACK](docs/FAQ/how-to-deploy-bold-bi-and-bold-reports-in-an-ack-cluster.md)  
- [⏫ Upgrade Bold BI using kubectl](upgrade/upgrade.md)  
- [📁 Migrate from Azure SMB to NFS FileShare](docs/FAQ/how-to-migrate-app_data-from-azure-smb-fileshare-to-nfs-fileshare.md)  

---

## 📄 License & Usage

> 📜 **Terms of Use:**  
> [https://www.boldbi.com/terms-of-use#embedded](https://www.boldbi.com/terms-of-use#embedded?utm_source=github&utm_medium=backlinks)

The provided container images include pre-installed optional libraries for convenience. It's your responsibility to ensure license compliance for all bundled software. If you prefer full control over the installation and libraries, consider downloading the [standalone package](https://www.boldbi.com/download).

For support, contact: [Bold BI Support](https://www.boldbi.com/support?utm_source=github&utm_medium=backlinks)
"""
