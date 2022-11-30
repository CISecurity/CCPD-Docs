![](http://i.imgur.com/5yZfZi5.jpg)

## End of Life and Final Release Dashboard v 2.x
------------------

** Version 2 of CIS-CAT Pro Dashboard has reached End of Life and its Final Release occurred in September 2022. It will be replaced with Dashboard v3.0.0 planned for a December 2022 release.**

Version 2.3.2 is the final release of CIS-CAT Pro Dashboard version 2 series. Dashboard version 3.0.0 will replace the 2.x versions, but the latest version will not be backwards compatible with version 2.x. A clean install of Dashboard version 3.0.0 is required as there are no upgrade or data migration options available from any previous 2.x version. Please read our [knowledge base article](https://cisecurity.atlassian.net/l/cp/mF6o97vs) to learn more. 

Version 2.3.2 will be available on CIS WorkBench for download through January 2023.

Vulnerability assessment features are deprecated.

Previous versions of 2.x will no longer be distributed as of January 2023.

Final installation and configuration and installation guides are packaged with Dashboard v2.3.2.  Dashboard version 3.0.0 documentation will be available online upon release.

------------------

## Introduction ##
CIS-CAT Pro Dashboard is a companion tool to CIS-CAT Pro Assessor. The Dashboard serves as a central repository for configuration assessment results generated from CIS-CAT Pro Assessor. Its main purpose is the view configuration assessment report averages over the short term. Graphical representations of automated configuration assessment scores for a time span less than 2 years (18 months recommended) provides security teams a quick view on current cyber configuration health. The Dashboard is intended to support organizational focus and action on the current cyber configuration posture of systems supporting  business operations. 

------------------------

## Dashboard Use Case ##

CIS-CAT Pro Dashboard best fits a single, small to medium size enterprise with a moderate amount of configuration result data. Defining “moderate” data amount depends on how many endpoints an organization has and how often those results are imported into the Dashboard. Dashboard is not designed for “big data” where organizations wish to import reports from, for example, 10,000 endpoints. We recommend seeking other data viewing tools specializing in big data handling should your organization need to view consolidated data for 1,000’s of endpoints. Members importing less than 1,000 reports monthly to a single Dashboard instance may have a better performance experience. For example, when an organization has 10,000 reports already stored in the database, additional imports will be slower. Members are encouraged to consider how Dashboard can best be utilized to support configuration state viewing and remediation efforts.

Some Members have found that multiple Dashboard installations representing each domain within their organization works well. There is no license limit to installing instances of Dashboard. However, CIS tests the Dashboard with the single enterprise with moderate data in mind. 

------------------------

## Main Features ##

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
## Obtain Dashboard ##
CIS-CAT Pro Dashboard is available to CIS SecureSuite Members. To learn more about becoming a CIS SecureSuite Member, visit our [website](https://www.cisecurity.org/). As a Member, organizations may navigate to [CIS WorkBench](https://workbench.cisecurity.org/dashboard) to obtain the CIS-CAT tools. 

Once logged into to CIS WorkBench, navigate to `Downloads` and enter the tag of `CIS-CAT Dashboard`. The previous version of Dashboard version 2 will be available until January 2023, but is NOT recommended for new Members. CIS has deprecated this version. 

For CIS-CAT Pro Dashboard v3.0.0, select your preferred installation of [Microsoft Windows](https://workbench.cisecurity.org/files/2176) or [Linux](https://workbench.cisecurity.org/files/2174).

------------------------

## Technology ##

CIS-CAT Pro Dashboard is a web application supported by a Grails Framework. All necessary components required to operate CIS-CAT Pro Dashboard are embedded. The installation, modification and upgrade process will be executed by utilizing the installer.

Embedded components alleviates the challenges of requiring expertise in various applications. CIS-CAT will complete the base configuration for you. To ease support and maintenance, CIS-CAT will only officially support the delivered components.

**Embedded components include:**

- Database - MariaDB 10.6.8
- Web application - Apache Tomcat 9
- Java - openJDK version 11

------------------------

## Installation Overview ##

The installation process will create two services that should remain running to support the application. On initial installation and upgrade, it can take several minutes for these services to start. These services are:

- MariaDB
- CCPD Windows
	
By default the installation will be placed C:\Program Files\CCPD (Microsoft Windows) or /usr/local/CCPD (Ubuntu Linux). CIS recommends modifying contents and structure using only the installer as the upgrade or install process may fail. See below for additional notes on notable sections of the installation. 

| Folder         |    Description |
| -----------------------| ------------- |
| ccpd_imports | Contains configuration assessment results only in ARF XML format produced by CIS-CAT Pro Assessor. Reports failing to import will move to the `error` folder, while successfully imported reports will move to the `processed`folder. It is possible to manually place reports in the `input` folder for CIS-CAT Pro Dashboard import.|
| certificates | By default, contains only self-signed certificates user-selected/created to support HTTPS during installation. You may optionally store an organizational certificate here, but it is not required. If, during upgrades, Members modify communication protocols, folder contents will not be cleared.|
| conf | Contains the configuration file that supports Dashboard functionality. Modifications to this file are recommended only throught the installation application. If manual changes occur, the services must be restarted and formatting errors may cause functionality in the Dashboard to not function properly. Users other than system or administrator are prevented from viewing this file. |
| content | Contains the supported CIS Benchmark content for CIS-CAT Pro Dashboard. The CIS Benchmarks provided within the build will be the latest supported content at the time of the Dashboard release. The content will be updated and overwritten with the latest on a Dashboard upgrade. CIS-CAT Pro Dashboard officially supports CIS Benchmark automated assessment content delivered with the application in datastream format. |
| logs | The log folder contains assessor and ciscatpro (dashboard) logs. For the purpose of troubleshooting issues, CIS Product Support may ask for these files. |

The installer establishes Java environment variables specifically for use with CIS-CAT Pro Dashboard. Therefore, it is recommended that no other application requiring a java runtime environment (jre) exists on the CIS-CAT Pro Dashboard host server.

The `conf` folder contains the ccpd-config.yml file that contains information to support the CIS-CAT Pro Dashboard operation. The installation process limits read/write privileges to only users whose credentials are validated by Microsoft Windows OS security mechanisms, typically System and Administrators. Users not a member of the authenticated group to not have privileges to view or write to the file. For Linux installations, the ccpd-config.yml will be granted ccpd-config.yml file has 660 privileges (-rw-rw----).

------------------------------
## Compatibility CIS-CAT Pro Dashboard v2.x Versions ##
CIS-CAT Pro Dashboard version 3 is a major version release that is not backwards compatible with the [previously deprecated CIS-CAT Pro Dashboard v2.x versions.](https://cisecurity.atlassian.net/l/cp/mF6o97vs) Read our [CIS-CAT Pro Dashboard v3.x FAQ]() to learn more.

CIS-CAT Pro Dashboard version 3.x requires a new installation. It is not possible to migrate data imported into the previous version 2.x to version 3.x.
