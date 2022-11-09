![](http://i.imgur.com/5yZfZi5.jpg)


------------------------------
# Environment Requirements #

The following environment characteristics are required.

**Server**
- A single Microsoft Windows Server 2016 or 2019
	- 8GB RAM
	- 10 GB disk space allocated to the main OS drive (usually the c:\ drive)
	- 2 vCPUs, 4 cores each
- Server does NOT currently host CIS-CAT Pro Dashboard v2.x 

The application is lightweight on processor and memory use. Assessment result import process will increase the memory and processing usage. CIS-CAT recommends conducting assessment result imports via the API during low peak business hours to avoid disrupting other business activities.

Load balanced configurations are not supported.

CIS utilizes a Microsoft Windows Server 2019 testing environment in AWS t2.large instance (designed for burst processing).

**Browser**
- Google Chrome

Other browsers maybe produce unexpected behavior.

**Traffic**
- Traffic allowed on port 8080 and 1433
	- As needed, add an inbound rule in Windows firewall
	- As needed, if installed on AWS, AWS security group must allow traffic on port 8080

**Other**
- No other applications present requiring system-installed Java runtime environment (JRE)
	- Including CIS-CAT Pro Assessor
- The main operating system drive must be selected for installation

------------------
# About the Installation #
The installation process will create two services that should remain running to support the application. On initial installation and upgrade, it can take several minutes for these services to start. These services are:

- MariaDB
- CCPD Windows
	
By default the installation will be placed C:\Program Files\CCPD. It is not recommended practice to manually modify contents within the structure. See below for additional notes on some of the structure. 

| Folder         |    Description |
| -----------------------| ------------- |
| ccpd_imports | Contains configuration assessment results only in ARF XML format produced by CIS-CAT Pro Assessor. Reports failing to import will move to the `error` folder, while successfully imported reports will move to the `processed`folder. It is possible to manually place reports in the `input` folder for CIS-CAT Pro Dashboard import.|
| certificates | By default, contains only self-signed certificates user-selected/created to support HTTPS during installation. You may optionally store an organizational certificate here, but it is not required. If, during upgrades, Members modify communication protocols, folder contents will not be cleared.|
| conf | Contains the configuration file that supports Dashboard functionality. Modifications to this file are recommended only throught the installation application. If manual changes occur, the services must be restarted and formatting errors may cause functionality in the Dashboard to not function properly. Users other than system or administrator are prevented from viewing this file. |
| content | Contains the supported CIS Benchmark content for CIS-CAT Pro Dashboard. The CIS Benchmarks provided within the build will be the latest supported content at the time of the Dashboard release. The content will be updated and overwritten with the latest on a Dashboard upgrade. CIS-CAT Pro Dashboard officially supports CIS Benchmark automated assessment content delivered with the application in datastream format. |
| logs | The log folder contains assessor and ciscatpro (dashboard) logs. For the purpose of troubleshooting issues, CIS Product Support may ask for these files. |

The installer establishes Java environment variables specifically for use with CIS-CAT Pro Dashboard. Therefore, it is recommended that no other application requiring a java runtime environment (jre) exists on the CIS-CAT Pro Dashboard host server.

------------------

# Installation Instructions #

For an initial CIS-CAT Pro Dashboard installation, follow the basic steps below. CIS-CAT has observed an initial installation effort on a prepared server to complete in less than 10 minutes. As the installation process will effect the Java home environment variables on the machine, CIS-CAT recommends that other applications requiring a system-installed java run time environment (JRE) are not present on the same host.

CIS-CAT Pro Dashboard requires a CIS SecureSuite license. Before initiating the installation process, download your organization's [SecureSuite license](https://cis-cat-pro-dashboard.readthedocs.io/en/latest/source/SecureSuite%20License/).

1. Place your [SecureSuite license](https://cis-cat-pro-dashboard.readthedocs.io/en/latest/source/SecureSuite%20License/) on the CIS-CAT Pro Dashboard server
2. Download the latest CIS-CAT Pro Dashboard from [CIS WorkBench](https://workbench.cisecurity.org/files), select the tag `CIS-CAT Dashboard` 
3. Place the application on a host server that **has not** previously had CIS-CAT Pro Dashboard or CIS-CAT Pro Assessor installed
4. Verify downloaded file is unblocked by right-clicking on file and selecting `properties` 
5. Launch the downloaded executable from any hard drive location as an administrator
6. Select Standard or Custom Installation
	- **Standard:** Navigates through only required options for most streamlined installation. 
	- **Custom:** Navigates through required and optional, advanced settings. During navigation, selected optional settings can be skipped.
7. Select `Yes` if prompted for permission to proceed with installation
8. Review installer screens below for additional information, if necessary

## Welcome ##
The initial screen on a first time installation.

![](img/scr2_CISCATProDashboardInstallerWelcomeCustom.png)

## License ##
A valid CIS issued SecureSuite license is required. The application may fail to load or some functions may not work as expected without a valid file. The license is primarily used for the remote assessment functionality.

[TODO-jenna says will change - new img will be needed]: #
![](img/scr3_SelectLicenseFile.png)

## Installation Destination ##
Select the main operating system drive for installation. For most Microsoft Windows environments, this will be `C:\Program Files\CCPD`.

![](img/scr4_SelectDestinationDirectory.png)

## Email (Custom Option) ##

The email configuration information is optional and presented only if selected on the Welccome screen during the first installation or upgrade. Email configuration is required for self-service "forgto password" requests.

CIS-CAT Pro Dashboard supports SMTP servers. By default, an unsecured mail server is assumed and configured to at `localhost` on port `25`. 

**Gmail Example**

![](img/scr5_EmailConfigurationGmailStandard.png)

scr5_EmailConfigurationGmailAdvanced.png

**Outlook Example**

![](img/scr5_EmailConfigurationOutlookStandard.png)


![](img/scr5_EmailConfigurationOutlookAdvanced.png)

## Active Directory - LDAP/S (Custom Option) ##

LDAP(S) is an optional configuration. If configured, CIS-CAT Pro Dashboard will only use the active directory users. LDAP/Active Directory will be used to manage user authentication and permissions within CCPD.

LDAP/AD roles and user properties such as firstname, lastname and email will be imported. If the user doesn't exist in CCPD, the username will be created on login and granted with a basic user role (ROLE\_USER) by default along with LDAP Roles.

**Requirements:**
- LDAP/AD email address is required to contain a valid value
- LDAP/AD group name must be uppercase

If some users were previously created in CCPD before the LDAP integration, make sure the username matches with the one in LDAP (uid) or AD (sAMAccountName, also called "User logon name").

The api user needs to be created in LDAP/AD in order to generate an authentication token to import Asset Report Format (ARF) results from CIS-CAT Assessor.

Once LDAP/AD authentication is integrated to CCPD, the database authentication will be automatically disabled.


![](img/scr6_LDAPConfiguration1.png)
![](img/scr6_LDAPConfiguration2.png)

**Example Active Directory Configuration**


| Configuration         |    Description |
| -----------------------| ------------- |
| Manager DN | Example: CN=Administrator,CN=Users,DC=corp,DC=cisecuritytest,DC=org |
| Manager Password | Credential for the Manager DN |
| Server | LDAP URL example: ldap://127.0.0.1:389  LDAPS URL example: ldaps://ldap.ciscat.ccp.sbp:636 |
| Group Search Base | Base directory for group search. Example: DC=corp,DC=cisecuritytest,DC=org |
| Group Search Filter | The pattern to be used for the user search. {0} is the user’s DN. Example: OpenLDAP: uniquemember={0} and AD: member={0} |
| Group Search Filter | The pattern to be used for the user search. {0} is the user’s DN. Example: OpenLDAP: uniquemember={0} and AD: member={0} |
| Group Role Attribute | The ID of the attribute which contains the role name for a group. Example: CN |
| Search Base | Base directory for search. Example: DC=corp,DC=cisecuritytest,DC=org |
| Search Filter | Filter expression used in search. Example: OpenLDAP: (uid={0}) or AD: sAMAccountName={0} |
| Password Attribute Name | Example: userPassword|


## Communication Protocol - HTTP(S) Setup ##
CIS-CAT Pro Dashboard will receive inbound configuration assessment result data from CIS-CAT Pro Assessor and optionally connect to select targets for a single, ad-hoc configuration assessment using the remote assessment features. Select the communication protocol that supports your organization policy. It is possible to select a self-signed certificate or HTTP while in the initial stages of testing or proving the concept of utilizing the Dashboard. A different protocol can be selected by executing the installer and selecting the option to modify existing functionality.

HTTPS
	- CIS-CAT generated self-signed certificate 
		![](img/scr7_HttpHttpsConfiguration.png)
	- Existing organization certificate
		![](img/scr7_HttpHttpsConfigurationExisting.png)
HTTP
This communication protocol transmits data in clear text.

![](img/scr7_HttpHttpsConfigurationNoCert.png)


## Set Database Password ##
The MariaDB that supports CIS-CAT Pro Dashboard has a native admin user with the username `root`. Set a strong password with the following requirements:

- Minimum 8 characters
- Contains at least one character in `!#$%^`
- Does NOT contain any special characters other than `!#$%^`

![](img/scr9_SetupDatabaseAdmin.png)

## Final Installation Process ##

The duration of the final steps of the installation can be 2 to 5 minutes. The initial services to support CIS-CAT Pro Dashboard take some time to start. The services installed are:

- CCPD Windows
- MariaDB

![](img/scr10_InstalllingStartingServices.png)

Once the installation detects that CIS-CAT Pro Dashboard is ready for use, the `Installation Complete` screen will be presented.

![](img/scr11_Complete.png)

Select `Open CIS-CAT Pro Dashboard` or `Finish & Open Dashboard` to login to CIS-CAT Pro Dashboard.

Depending on the communication protocol selection during installation, the CIS-CAT Pro Dashboard URL will be:

- HTTP: http://localhost:8080/CCPD/
- HTTPS: https://localhost:8080/CCPD/

## Login to Dashboard ##

    username: admin 
    password: @admin123

You'll be prompted to change your password upon first login.

---------------------------

# Upgrade Process #
Each release of CIS-CAT Pro Dashboard v3.x will contain upgrades to the main CIS-CAT application and embedded components. Upgrades are applied utilizing the latest installer included in the downloaded CIS-CAT Pro Dashboard.

The installer will detect a previous installation and prompt to update only the application or update/modify configuration changes. If no changes are required, updating only the application is the most efficient. Follow the basic steps below. 

**NOTE:** There is no upgrade or migration path from CIS-CAT Pro Dashboard version 2.x to version 3.x. Please read our FAQ and our [blog](https://www.cisecurity.org/insights/blog/cis-cat-pro-is-now-even-better-heres-how-weve-improved-it) to learn more about CIS-CAT Pro changes.

1. Download the latest CIS-CAT Pro Dashboard from [CIS WorkBench](https://workbench.cisecurity.org/files), select the tag `CIS-CAT Dashboard`
2. Place the application on a host server that **has** previously had CIS-CAT Pro Dashboard v3.x installed
3. Verify downloaded file is unblocked by right-clicking on file and selecting `properties` 
4. Launch the downloaded executable from any hard drive location as an administrator
5. Select Standard or Custom Installation
	- **Update application only:** applies existing configuration, updates CIS-CAT application. No options to modify existing configurations.
	- **Update application and/or configuration settings:** applies existing configuration with options to modify some settings, updates CIS-CAT application. Select **optional** Email or LDAP configuration to modify or initiate these functions.
6. Select `Yes` if prompted for permission to proceed with installation

------------------
# Installation Error #

Occasionally, a CIS-CAT Pro Dashboard installation or upgrade may result in an error.

- **Check Services:** Navigate to Windows Services manager. You will find `MariaDB` and `CCPD Windows` listed; start them if needed and try again after a few minutes.
- **Retry Installer:** Close and re-launch CCPD Installer. The installer will guide you through any necessary configuration.

If you are unsuccessful, collect logs that have been generated for you and open a support ticket. See further information below.


# Obtaining Installer Logs #
During the installation, the Installer will create logs. 

The installer logs will be created in a directory within the temporary directory of the operating system. 
Each installation attempt will create an individual log with a timestamp. 
You can access these logs at any time throughout the installation process by clicking the **Installer Logs** button or by navigating directly to the logs location at: `C:\Users\loggedinUser\AppData\Local\Temp`.

![](img/scrAll_InstalllerLogs.png)

Additionally, support may require any logs generated at this location: `C:\Program Files\CCPD\logs\ccpdlogs`. 

If you need assistance, please provide the above log files on a [support ticket](https://www.cisecurity.org/support/).

------------------


# CIS-CAT Pro Assessor Integration #

CIS-CAT Pro Dashboard is a companion tool to CIS-CAT Pro Assessor. The Dashboard can serve as a central repository for configuration assessment results generated from CIS-CAT Pro Assessor. The Dashboard can also be an way to validate different machines in an easy-to-view way. CIS-CAT Pro Dashboard is designed to import configuration results generated from CIS-CAT Pro Assessor either manually or via an API. Manually imported results must be in XML Asset Reporting Format (ARF) while automated imports do not require a physical file and are imported via a REST API. Consult the [CIS-CAT Pro Assessor configuration guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#cis-cat-pro-dashboard-integration) to learn how to automatically configure reports to load into the Dashboard.

Authentication must be established with CIS-CAT Pro Assessor to enable automatic imports via API.

## Establish Authentication with Assessor ##
Authentication is established with a generated Authentication Token from CIS-CAT Pro Dashboard. By default, Dashboard establishes a user named apiuser which has ROLE_API.  The default password for this user is @apiuser123. Other users may be configured with the ROLE_API. Only a user with this role can generate the token.

![](http://i.imgur.com/l2HSbC1.png)

Place the generated token in the assessor-cli.properties file for the Assessor that will post to the Dashboard. This file is typically located in the config folder of the Assessor v4. See the [Assessor Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#cis-cat-pro-dashboard-integration) for more information.
  

**Generate the Token**

 1. Login as an administrator and navigate to the user management page for the apiuser
 2. Generate the token

## Dashboard API ##

### Upload Report API ###
CIS-CAT Pro Dashboard utilizes an API to upload assessment reports (ARF,XML) generated by CIS-CAT Pro Assessor v4. The API utilizes a POST_URL feature. The API can also be called from a script (python, powershell etc...). The API definition can assist organizations, where necessary, in building their own, organization-approved scripts to upload reports into the Dashboard.

**Description**


- **Url**: ```http(s)://[MY-DASHBOARD-SERVER]/CCPD/api/reports/upload```
- **Method:** ```POST```
- **Header:** <br/>
  **'Authorization':** ```'Bearer=[MY_DASHBOARD_AUTHENTICATION_TOKEN]'``` <br/>
  **NOTE:** ```[MY_DASHBOARD_AUTHENTICATION_TOKEN]``` is the token generated from the Dashboard with the a user assigned with ROLE_API. For more details, please see [Establish authentication with Assessor](#establishAuthWithAssessor) section.<br/>
  **'Content-type'**: ```multipart/form-data``` <br/>
  **NOTE:** In the below example of the Python script, content-type is automatically generated. There is no need to specify it.
- **POST Data Params:** <br/>
  **'ciscat-report'**: String content of the XML report generated by the Assessor <br/>
  **'report-name'**: A given name of the report. For example, the name can follow the Assessor naming convention as following: ```hostname_benchmark-timestamp-ARF.xml```.
- **Responses code:** <br/>
  **200:** Assessment report successfully uploaded<br/>
  **400:** Unexpected failure with details on response status message<br/>
  **401:** Assessment failed to upload because of an Authentication Failure.  Please ensure your authentication token is correct. <br/>
  **500:** Assessment failed to upload with details on response status message

**Example of Python script:**

Below is a script to upload of a single report into the Dashboard:

Assuming ```Hostname_CIS_Microsoft_Windows_10_Enterprise_Release_1803_Benchmark-20190805T135433Z-ARF.xml``` is the name of the report file generated by CIS-CAT Pro Assessor and located in ```./reports``` directory.<br/>The generated token is ```eertaa2pg2h7vb3ms97kdjebakr22v15``` and the Dashboard URL is ```https://mydashboard/CCPD/api/reports/upload```


	import sys
	import json
	import requests
	import http
	import datetime
	
	print(str(datetime.datetime.today()) + " *********************** Start dashboard upload script ***********************")
	
	apiHeaders = {'Authorization': 'Bearer=eertaa2pg2h7vb3ms97kdjebakr22v15'}
	
	with open('./reports/Hostname_CIS_Microsoft_Windows_10_Enterprise_Release_1803_Benchmark-20190805T135433Z-ARF.xml', 'rb') as f:
	    filecontent = f.read()
	requests.post("https://mydashboard/CCPD/api/reports/upload", headers=apiHeaders,  data={'ciscat-report': filecontent ,'report-name':'Hostname_CIS_Microsoft_Windows_10_Enterprise_Release_1803_Benchmark-20190805T135433Z-ARF.xml'})

	print(str(datetime.datetime.today()) + " *********************** End dashboard upload script ***********************")

**NOTE:** In order to troubleshoot authorization/upload issues, SSL certificate verification can be ignored using ```requests.post(...,verify=False)```


------------------

# CIS WorkBench Integration #

This feature is an optional service provided to members to receive automatic notifications on new CIS-CAT Pro releases. 

**Setting up the connection is an admin only ability. Additionally, the application requires a direct internet connection, a proxy will not work.**

When the connection is active, inbox alerts will appear within CIS-CAT Pro Dashboard when a new CIS-CAT Pro release is available.

Retrieve the new release using links in the alert message from within CIS-CAT Pro Dashboard without logging directly into CIS WorkBench.

CIS utilizes [OAuth 2.0](https://oauth.net/2/) authorization framework to establish a connection between the two applications.

A one-way API is established from an instance of CIS-CAT Pro Dashboard to CIS WorkBench.

Each connection or integration is unique per Dashboard installation, which allows organizations with multiple instances of Dashboard to establish a communication between CIS-CAT Pro Dashboard and CIS WorkBench.

CIS-CAT Pro Dashboard will check CIS WorkBench daily for the availability of a new release of CIS-CAT Pro. Establishing this connection will not allow CIS to collect any assessment results from your organization.

## Establish a connection with CIS WorkBench ##
Under the settings menu, an option called Systems Integrations is available to users with the admin role.

Select System Integrations menu item:

![](https://i.imgur.com/HfHZQ0g.png)

In System Integrations, select the **Connect** button:

![](https://i.imgur.com/PG4AxDt.png)

Select Continue to CIS WorkBench:

![](https://i.imgur.com/9ylrwiY.png)

Enter CIS WorkBench credentials and select Authorize:

![](https://i.imgur.com/EFYFETG.png)

Review the screen and Select Authorize:

![](https://i.imgur.com/3A2tpw4.png)

**NOTE:** The switch button appears grayed out because "Downloads of new CIS-CAT Pro updates" is the only service offered so far. In the future, members will have the option to opt-in/out from multiple services.

The connection is successfully made:

![](https://i.imgur.com/vIyIvw1.png)


## Test connection between CIS-CAT Pro Dashboard and CIS WorkBench ##
Test button is available to verify the connection between CIS-CAT Pro Dashboard and CIS WorkBench.

When a connection is active, test the connection by pressing **Test** button:

![](https://i.imgur.com/gCZYSfw.png)

If successful, a message will show on the screen.

If not, instructions will be provided in an error message.

## Disconnect from CIS WorkBench ##
Select Disconnect:

![](https://i.imgur.com/11eJySi.png)

Select Disconnect again in the popup:

![](https://i.imgur.com/Zej4j5f.png)

The disconnection is successfully made:

![](https://i.imgur.com/vF4arRf.png)

Now CIS-CAT Pro Dashboard and CIS WorkBench are disconnected.

Although your connection is no longer active between CIS-CAT Pro Dashboard and CIS WorkBench, **an active API client exists on your organization’s profile on the CIS WorkBench**. We keep this API client to allow you to reconnect easily.
 
However, if you no longer want to utilize the service, please open a ticket at the [CIS Support Portal](https://www.cisecurity.org/support/) in order to delete the API client.
