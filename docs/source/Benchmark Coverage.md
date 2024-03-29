![](http://i.imgur.com/5yZfZi5.jpg)

# CIS Benchmark Support

----------------------

## CIS Benchmark Coverage

CIS-CAT Pro supports remote configuration assessment for a single system. The CIS-CAT Pro Dashboard is packaged with CIS Benchmark automated assessment content. CIS-CAT Pro Dashboard supports automated assessment content in **datastream format** only. Some CIS Benchmarks currently are not offered in this format. See below for the list of CIS Benchmark automated assessment content supported in the latest version of CIS-CAT Pro Dashboard. 

For some older Windows platforms such as Microsoft Windows Server 2008 R2, it is required to be current with service pack updates in order for the assessment to process without error.

- **AKS-Optimized Azure Linux 2 v1.0.0**
- **AlmaLinux OS 8 v3.0.0**
- **AlmaLinux OS 9 v1.0.0**
- **Amazon Elastic Kubernetes Service (EKS) v1.3.0**
- **Amazon Linux 2 v2.0.0**
- **Amazon Linux 2 STIG v2.0.0**
- **Amazon Linux 2023 v1.0.0**
- **Apple macOS 10.15 Catalina v3.0.0**
- **Apple macOS 11.0 Big Sur v4.0.0**
- **Apple macOS 12.0 Monterey v3.0.0**
- **Apple macOS 13.0 Ventura v2.0.0**
- **Apple macOS 14.0 Sonoma v1.0.0**
- **Azure Compute Microsoft Windows Server 2019 v1.0.1**
- **Azure Compute Microsoft Windows Server 2022 v1.0.0**
- **Azure Kubernetes Service (AKS) v1.4.0**
- **CentOS Linux 7 v3.1.2**
- **Cisco IOS 15 v4.1.1**
- **Cisco IOS 16 v2.0.0**
- **Cisco IOS 17 v2.0.0**
- **Debian Family Linux v1.0.0**
- **Debian Linux 10 v2.0.0**
- **Debian Linux 11 v1.0.0**
- **Debian Linux 11 STIG v1.0.0**
- **Docker v1.6.0**
- **Fedora 28 Family Linux v2.0.1**
		- NOTE:  Requires the "ignore.platform.mismatch" property be set to "true" in the Assessor's properties file.
- **Google Chrome Benchmark v2.1.0**
- **Google Kubernetes Engine (GKE) v1.4.0**
- **Kubernetes V1.20 Benchmark v1.0.1**
- **Kubernetes V1.23 Benchmark v1.0.1**
- **Kubernetes v1.8.0**
- **Microsoft Edge Benchmark v2.0.0**
- **Microsoft IIS 10 Benchmark v1.2.1**
- **Microsoft Office Enterprise v1.1.0**
- **Microsoft Intune for Windows 10 v1.1.0**
- **Microsoft Intune for Windows 11 v1.0.0**
- **Microsoft Windows 10 Enterprise v2.0.0**
- **Microsoft Windows 10 Stand-alone v2.0.0**
- **Microsoft Windows 11 Enterprise v2.0.0**
- **Microsoft Windows 11 Stand-alone v2.0.0**
- **Microsoft Windows Server 2008 (non-R2) v3.1.0**
- **Microsoft Windows Server 2008 R2 v3.3.0**
- **Microsoft Windows Server 2012 (non-R2) v3.0.0**
- **Microsoft Windows Server 2012 R2 v3.0.0**
- **Microsoft Windows Server 2016 v2.0.0**
- **Microsoft Windows Server 2016 STIG v2.0.0**
- **Microsoft Windows Server 2019 v2.0.0**
- **Microsoft Windows Server 2019 STIG v1.1.0**
- **Microsoft Windows Server 2022 v2.0.0**
- **Microsoft Windows 8.1 Workstation v2.4.0**
- **NGINX v2.0.1**
- **Oracle Cloud Infrastructure Container Engine for Kubernetes(OKE) v1.3.0**
- **Oracle Linux 7 v3.1.1**
- **Oracle Linux 8 v3.0.0**
- **Oracle Linux 9 v1.0.0**
- **Red Hat Enterprise Linux 7 v3.1.1**
- **Red Hat Enterprise Linux 7 STIG v2.0.0**
- **Red Hat Enterprise Linux 8 v3.0.0**
- **Red Hat Enterprise Linux 8 STIG v1.0.0**
- **Red Hat Enterprise Linux 9 v1.0.0**
- **Red Hat OpenShift Container Platform v1.4.0**
- **Rocky Linux 8 Benchmark, v2.0.0**
- **Rocky Linux 9 Benchmark, v1.0.0**
- **SUSE Linux Enterprise 12 v3.1.0**
- **SUSE Linux Enterprise 15 v1.1.1**
- **Ubuntu Linux 18.04 LTS v2.1.0**
- **Ubuntu Linux 20.04 LTS v2.0.1**
- **Ubuntu Linux 20.04 LTS STIG v2.0.0**
- **Ubuntu Linux 22.04 LTS v1.0.0**

----------------------

## Data Stream Format

CIS-CAT Pro Dashboard is designed to assess with CIS Benchmark automated assessment content that is in conformance with the Security Content Automation Protocol (SCAP). The Dashboard  supports tailored and CIS official content. All automated assessment files exist in the content directory of the CIS-CAT installation location. Dashboard only accepts datastream collection files (files that end in the -collection.xml). This is an all-in-one OVAL file format that combines all of the file types (including sce scripts) into a single file. The datastream format can be obtained from the DATASTREAM folder of an exported forked benchmark. See an example CIS Benchmark below. Non-datastream files will appear as blank rows in the assess popup window.

![](img/datastream.png)