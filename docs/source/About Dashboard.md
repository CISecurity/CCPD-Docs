![](http://i.imgur.com/5yZfZi5.jpg)

# About CIS-CAT Pro Dashboard

------------------

## Introduction 

CIS-CAT Pro Dashboard is a companion tool to CIS-CAT Pro Assessor. **Dashboard is NOT required to run an assessment.** Members just starting with CIS-CAT should start assessing a baseline image with **[CIS-CAT Assessor](https://workbench.cisecurity.org/download/cis-cat/pro)** that supports assessments using CLI running Assessor-CLI.bat, Assessor-CLI.sh or GUI standalone. Review CIS-CAT Pro Assessor [documentation](https://ccpa-docs.readthedocs.io/en/latest/) to learn more.


The Dashboard can optionally serve as a central repository for configuration assessment results generated from CIS-CAT Pro Assessor. Its main purpose is to view configuration assessment report averages over the short term. Graphical representations of automated configuration assessment scores for a time span less than 2 years (18 months recommended) provides security teams a quick view on current cyber configuration health. The Dashboard is intended to support organizational focus and action on the current cyber configuration posture of systems supporting  business operations. 

------------------------

## Dashboard Use Case 

CIS-CAT Pro Dashboard best fits a single, small to medium size enterprise with a moderate amount of configuration result data. The size or your organization does not specifically matter if imported data will be moderate. Defining “moderate” data amount depends on how many endpoints an organization has and/or how often those results are imported into the Dashboard. Dashboard is not designed for “big data” where organizations wish to import reports from, for example, 10,000 endpoints. We recommend seeking other data viewing tools specializing in big data handling should your organization need to view consolidated data for 1,000’s of endpoints. Members importing less than 1,000 reports monthly to a single Dashboard instance may have a better performance experience. For example, when an organization has 10,000 reports already stored in the database, additional imports may be slower. Members are encouraged to consider how Dashboard can best be utilized to support configuration state viewing and remediation efforts.

Some Members have found that multiple Dashboard installations representing each domain within their organization works well. There is no license limit to installing instances of Dashboard. However, CIS tests the Dashboard with the single enterprise with moderate data usage. 

------------------------

## Main Features 

Use of Dashboard is optional. Routine assessment are best performed with CIS-CAT Pro Assessor. Dashboard offers the following features:

- View average configuration assessment score in graphical format by:
	- Overall systems
	- CIS Benchmark
	- Tagged systems
- Drill down to individual configuration assessment results
- View assessments results by CIS Critical Security Controls 
- Navigate from a high level graphical overview of environmental compliance with CIS Benchmarks to individual assessment results that produce a compliance score
- Perform on-demand, remote configuration assessment against a single, remote target system
- Create exceptions to failed results and rescore overall averages
- Custom tag systems for easier exception application or overall compliance average grouping in graphical format


------------------------------

## Obtain Dashboard 

CIS-CAT Pro Dashboard is available to CIS SecureSuite Members. To learn more about becoming a CIS SecureSuite Member, visit our [website](https://www.cisecurity.org/). As a Member, organizations may navigate to [CIS WorkBench](https://workbench.cisecurity.org/dashboard) to obtain the CIS-CAT tools. 

Once logged into to CIS WorkBench, navigate to `Downloads` and enter the tag of `CIS-CAT Dashboard`. The previous version of Dashboard version 2 will be available until January 2023, but is NOT recommended for new Members. CIS has deprecated this version. 

For CIS-CAT Pro Dashboard v3.0.0, select your preferred installation of [Microsoft Windows](https://workbench.cisecurity.org/files/2176) or [Linux](https://workbench.cisecurity.org/files/2174).

------------------------

## Technology 

CIS-CAT Pro Dashboard is a web application supported by a Grails Framework. All necessary components required to operate CIS-CAT Pro Dashboard are embedded. The installation, modification and upgrade process will be executed by utilizing the installer.

Embedded components alleviates the challenges of requiring expertise in various applications. CIS-CAT will complete the base configuration for you. To ease support and maintenance, CIS-CAT will only officially support the delivered components.

**Embedded components include:**

- Database - MariaDB 10.6.8
- Web application - Apache Tomcat 9
- Java - openJDK version 11

------------------------

## Security 

CIS-CAT team utilizes best efforts to ensure that the CIS-CAT product are free from material vulnerabilities resulting from integrated third-party libraries with continuous use of  monitoring tools as part of the software build process. 
The Center for Internet Security performs annual penetration testing on eligible software products, which includes CIS-CAT. CIS-CAT mitigates risks with recommended solutions associated with penetration test findings assessed at and above a Medium.

The Center for Internet Security product engineering practices are SOC 2 certified.
SOC 2 is a voluntary compliance standard for service organizations, developed by the American Institute of CPAs (AICPA), which specifies how organizations should manage customer data. The standard is based on the following Trust Services Criteria: security, availability, processing integrity, confidentiality, privacy.

CIS-CAT's engineering team is populated with individuals educated and certified in cyber security best practices.
The Center for Internet for Security develops cyber security best practices with our global community of cybersecurity experts. We implement these best practices within the organization. 

CIS-CAT Pro Dashboard delivers with a Software Bill of Materials (SBOM). The the bill of materials is delivered in file formats of JSON and XML and are updated with each release of the products and placed in the "Documentation" folder. The files may also be downloaded separately on [CIS WorkBench](https://workbench.cisecurity.org/files?q=&tags=39&visibility=all).

The term “Software Bill of Materials” or “SBOM” means a formal record containing the details and supply chain relationships of various components used in building software. CIS SecureSuite products utilize and embed many open source and commercial software components. The SBOM enumerates these components in the product. It is analogous to a list of ingredients on food packaging. An SBOM is useful to those who develop or manufacture software, those who select or purchase software, and those who operate software. Buyers can use an SBOM to perform vulnerability or license analysis, both of which can be used to evaluate risk in a product. Those who operate software can use SBOMs to quickly and easily determine whether they are at potential risk of a newly discovered vulnerability. A widely used, machine-readable SBOM format allows for greater benefits through automation and tool integration. The SBOMs gain greater value when collectively stored in a repository that can be easily queried by other applications and systems. Understanding the supply chain of software, obtaining an SBOM, and using it to analyze known vulnerabilities are crucial in managing risk.


------------------------

## Installation Overview 

The installation application must be used to complete all install, upgrade, and installation modifications.
The installation process will create two services that should remain running to support the application. On initial installation and upgrade, it can take several minutes for these services to start. These services are:

- MariaDB (Linux: mariadbd.service in systemctl)
- CCPD_Windows (Linux: CIS-CAT_Pro_Dashboard.service in systemctl)
	
By default the installation will be placed C:\Program Files\CCPD (Microsoft Windows) or /usr/local/CCPD (Ubuntu Linux). CIS recommends modifying contents and structure using only the installer as the upgrade or install process may fail. See below for additional notes on notable sections of the installation. 

| Folder         |    Description |
| -----------------------| ------------- |
| ccpd_imports | Contains configuration assessment results only in ARF XML format produced by CIS-CAT Pro Assessor. Reports failing to import will move to the `error` folder, while successfully imported reports will move to the `processed`folder. It is possible to manually place reports in the `input` folder for CIS-CAT Pro Dashboard import.|
| certificates | By default, contains only self-signed certificates user-selected/created to support HTTPS during installation. You may optionally store an organizational certificate here, but it is not required. If, during upgrades, Members modify communication protocols, folder contents will not be cleared.|
| conf | Contains the configuration file that supports Dashboard functionality. Modifications to this file are recommended only throught the installation application. If manual changes occur, the services must be restarted and formatting errors may cause functionality in the Dashboard to not function properly. Users other than system or administrator are prevented from viewing this file. |
| content | Contains the supported CIS Benchmark content for CIS-CAT Pro Dashboard. The CIS Benchmarks provided within the build will be the latest supported content at the time of the Dashboard release. The content will be updated and overwritten with the latest on a Dashboard upgrade. CIS-CAT Pro Dashboard officially supports CIS Benchmark automated assessment content delivered with the application in datastream format. |
| logs | The log folder contains assessor and ciscatpro (dashboard) logs. For the purpose of troubleshooting issues, CIS Product Support may ask for these files. |

The installer establishes Java environment variables specifically for use with CIS-CAT Pro Dashboard. Therefore, it is recommended that no other application requiring a java runtime environment (jre) exists on the CIS-CAT Pro Dashboard host server.

The `conf` folder contains the ccpd-config.yml file that contains information to support the CIS-CAT Pro Dashboard operation. The installation process limits read/write privileges to only users whose credentials are validated by Microsoft Windows OS security mechanisms, typically System and Administrators. Users who are not a member of the authenticated group do not have privileges to view or write to the file. For Linux installations, the ccpd-config.yml has 660 privileges (-rw-rw----).



------------------------------

## Version 3 FAQ 

- [Why use CIS-CAT Pro Dashboard?](#whyuse)
- [Can I use my existing Dashboard v2 server for an installation of Dashboard v3?](#existing)
- [Will CIS-CAT Pro Dashboard v2 continue to be supported?](#existing)
- [How do I move my history to the new version?](#migratedata)
- [Is version 3 easier to install?](#ease)
- [How will version 3 protect my database?](#protect)
- [Do I need a license?](#license)
- [What components are embedded? Are substitutions allowed?](#embed)
- [Is Active Directory supported?](#ad)
- [Has the interface changed?](#interface)
- [Can I store all my data in Dashboard v3?](#datamount)
- [Are vulnerability assessments supported?](#vuln)
- [Does the installation support IIS?](#iis)



<a name="whyuse"></a>
### Why should I use CIS-CAT Pro Dashboard?

**Dashboard is NOT required to run an assessment.** Members just starting with CIS-CAT should start assessing a baseline image with **[CIS-CAT Assessor](https://workbench.cisecurity.org/download/cis-cat/pro)** that supports assessments using CLI running Assessor-CLI.bat, Assessor-CLI.sh or GUI standalone. Review CIS-CAT Pro Assessor [documentation](https://ccpa-docs.readthedocs.io/en/latest/) to learn more.

CIS-CAT Pro Dashboard is a companion tool to CIS-CAT Pro Assessor. The Dashboard serves as a central repository for configuration assessment results generated from CIS-CAT Pro Assessor. Its main purpose is the view configuration assessment report averages over the short term. Graphical representations of automated configuration assessment scores for a time span less than 2 years (18 months recommended) provides security teams a quick view on current cyber configuration health. The Dashboard is intended to support organizational focus and action on the current cyber configuration posture of systems supporting  business operations. Export HTML formatted reports to share with security teams as they make decisions and plan remediation or exception on CIS Benchmark recommendations. Apply exceptions where risk is accepted or resolved in other ways and improve configuration assessment scores. Receive alerts on newly imported result scores that deviate beyond a user-defined threshold from previous results.

<a name="existing"></a>
### Can I install Dashboard v3.0.0 on my existing Dashboard server?

No. We do not recommend this. Some services and port may conflict. We recommend a new server that has not had CIS-CAT Pro Dashboard previously installed on it.

<a name="support"></a>
### Will CIS continue to support CIS-CAT Pro Dashboard 2.x?

No. CIS has deprecated CIS-CAT Pro Dashboard 2.x series. See our [knowledge base article](https://cisecurity.atlassian.net/l/cp/tL0N17rA).

<a name="migratedata"></a>
### I’m using CIS-CAT Pro Dashboard 2.x version series. How do I move my historical assessment data to CIS-CAT Pro Dashboard 3.x version?

The latest Dashboard is not backwards compatible. It is not possible for Assessor to authenticate with more than one Dashboard. Organizations may start fresh with Dashboard v3.0.0. It may be possible to operate two instances of an Assessor authenticated with each Dashboard version, the old (2.x) and new (3.0), until your organization is ready to migrate to the latest version 3.0.0. The latest Dashboard’s best use case is as a current or recent past view of assessment data vs. a several year history. We have changed the structure of the stored data and will not be able to migrate data from the prior versions of Dashboard. It may be possible to import configuration assessment XML ARF format reports if you have them by dropping them into the “…CCPD\ccpd_imports\input“ folder manually.

<a name="ease"></a>
### In my opinion, CIS-CAT Pro Dashboard 2.x was difficult to install, will this version be easier to install and upgrade? 

YES! CIS-CAT Pro Dashboard 3.x includes an enhanced installer application and will install or update all necessary components of CIS-CAT Pro Dashboard. Optional components are not supported. The latest dashboard application embeds all necessary components including Apache Tomcat, MariaDB, and openJDK. You don’t need to be an expert at multiple applications to run CIS-CAT Pro Dashboard. To ease your onboarding and upgrading challenges, we’ll manage the base configuration for you! 

<a name="protect"></a>
### Will CIS-CAT Pro Dashboard 3.x protect my database?

Yes. The CIS-CAT Pro Dashboard 3.x will update the configuration information during the installation and upgrade. As part of the installation, supporting configuration information such as database passwords will have more strict permissions. For example, on a Microsoft Windows machine, general “User” Groups will be prohibited from accessing the configuration file. Additionally, it is possible to configure the communication protocol of HTTPS.

<a name="license"></a>
### Do I need a license key to operate CIS-CAT Pro Dashboard 3.x?

Yes. CIS-CAT Pro Dashboard 3.x now includes embedded configuration assessment functions along with current, select supported CIS Benchmark automated content. Update your organization’s license as part of the installation or upgrade process. This is the same license utilized for all CIS SecureSuite products and is available from the CIS WorkBench under your organization’s profile. 

<a name="embed"></a>
### What major components will be embedded and how will CIS keep them up to date? Can I substitute different components such as a different database?

CIS-CAT will embed the latest version of openJDK 11, MariaDB 10.6.8, and Apache Tomcat 9. CIS-CAT will upgrade these versions as needed as part of Dashboard releases. CIS-CAT will not support substitutions for these embedded components. 

<a name="ad"></a>
### Will Dashboard 3.x support Active Directory and LDAP and LDAPS?

Yes. The latest version of Dashboard supports AD for LDAP and LDAPS.

<a name="interface"></a>
### Has the user interface changed with Dashboard v3.0.0?

No. The user interface is the same with the exception of removal of vulnerability features and functions. CIS-CAT Pro Dashboard as well as CIS-CAT Pro Assessor will drop support for vulnerability assessments, as this feature isn't widely used among Members.

<a name="datamount"></a>
### Can I use Dashboard to store all my historical assessment data?

Members should not view Dashboard as an application that stores many years of data. CIS recommends storing less than 2 years of data. CIS recommends using Dashboard to view current and most recent configuration states. 

<a name="vuln"></a>
### Will Vulnerability Assessments be supported in CIS-CAT Pro Dashboard 3.x?

No. CIS will deprecate the CIS-CAT Pro Dashboard and CIS-CAT Pro Assessor functionality that supports importing and viewing vulnerability assessment data. CIS-CAT will focus on configuration assessment data analysis.

<a name="iis"></a>
### Will Dashboard 3.x support IIS?

No. At this time, CIS will not support installations with Microsoft IIS.

------------------------------

## Compatibility CIS-CAT Pro Dashboard v2.x Versions 

CIS-CAT Pro Dashboard version 3 is a major version release that is not backwards compatible with the [previously deprecated CIS-CAT Pro Dashboard v2.x versions.](https://cisecurity.atlassian.net/l/cp/mF6o97vs) Read our [CIS-CAT Pro Dashboard v3.x FAQ]() to learn more.

CIS-CAT Pro Dashboard version 3.x requires a new installation. It is not possible to migrate data imported into the previous version 2.x to version 3.x.

## End of Life and Final Release Dashboard v 2.x

------------------

** Version 2 of CIS-CAT Pro Dashboard has reached End of Life and its Final Release occurred in September 2022. It has been replaced with Dashboard v3.0.0 released in December 2022.**

Version 2.3.2 is the final release of CIS-CAT Pro Dashboard version 2 series. Dashboard version 3.0.0 will replace the 2.x versions, but the latest version will not be backwards compatible with version 2.x. A clean install of Dashboard version 3.0.0 is required as there are no upgrade or data migration options available from any previous 2.x version. Please read our [knowledge base article](https://cisecurity.atlassian.net/l/cp/mF6o97vs) to learn more. 

Version 2.3.2 will be available on CIS WorkBench for download through January 2023.

Vulnerability assessment features are deprecated.

Previous versions of 2.x will no longer be distributed as of January 2023.

Final installation and configuration and installation guides are packaged with Dashboard v2.3.2. 