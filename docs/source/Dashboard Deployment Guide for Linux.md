![](http://i.imgur.com/5yZfZi5.jpg)

------------------------------
# Environment Requirements #

- [Server](#server)
- [Browser](#browser)
- [Traffic and Ports](#traffic)
- [Other considerations](#other)


The following environment characteristics are required.

<a name="server"></a>
**Server**

- A single Ubuntu 20.04 server
	- 8GB RAM
	- Minimum 10 GB disk space allocated to the main OS location
	- 2 vCPUs, 4 cores each
	- Ubuntu Minimal not supported as standard packages needed to support MariaDB and Tomcat are not present
- Server does NOT currently host CIS-CAT Pro Dashboard v2.x 

The application does not heavily utilize processor and memory. Assessment result import process will increase the memory and processing usage. CIS-CAT recommends conducting assessment result imports via the API during low peak business hours to avoid disrupting other business activities.

<a name="browser"></a>
**Browser**

- Google Chrome

Other browsers maybe produce unexpected behavior.

<a name="traffic"></a>
**Traffic and Ports**

- **Internet available on the server during installation***
- Port 3306 is available for Maria database installation
- Traffic allowed on port 8080 (HTTP) and 443(HTTPS)
	- As needed, if installed on AWS, AWS security group must allow traffic on port 8080/443

\* Ubuntu 20.04 must have certain packages installed. **Internet is required** at the time of initial installation so the correct packages can be confirmed. The internet connection can be disabled after installation.

<a name="other"></a>
**Other Considerations**<br>

_No other applications present requiring system-installed Java runtime environment (JRE)._

CIS-CAT Pro Dashboard v3 deploys with embedded openJDK and sets the Java Home variable on the host system. If other applications require a system installed Java (like CIS-CAT Assessor), the additional application may not function. CIS-CAT Pro Assessor will offer embedded Java for all operating systems in Q1 2023. If you are utilizing a version of CIS-CAT that contains the embedded Java then this will not cause a Java conflict. 

_Additional host system memory and processing resources may be needed when Dashboard host also hosts CIS-CAT Assessor._

If you have determined that there is no Java conflict, the host system's resources must also be considered if the system will host CIS-CAT Pro Assessor and Dashboard. CIS-CAT Pro Dashboard includes an embedded Apache Tomcat and Maria Database. Recommended server resources are 2 vCPUs (4 cores each), 10 GB of free disk space, and 8GB of RAM. Should this host server also host CIS-CAT Assessor or other applications, additional power and memory may be needed. Additionally, it is best practice for a host server containing a web application to only host the application it supports.

# Installation Instructions #

For an initial CIS-CAT Pro Dashboard installation on Ubuntu Linux, follow the basic steps below. CIS-CAT has observed an initial installation effort on a prepared server to complete in less than 10 minutes. As the installation process will effect the Java home environment variables on the machine, CIS-CAT recommends that other applications requiring a system-installed java run time environment (JRE) are not present on the same host.

CIS-CAT Pro Dashboard requires a CIS SecureSuite license. Before initiating the installation process, download your organization's [SecureSuite license](https://cis-cat-pro-dashboard.readthedocs.io/en/latest/source/SecureSuite%20License/). Obtain the CIS-CAT Pro Dashboard application from the [CIS WorkBench](https://cis-cat-pro-dashboard.readthedocs.io/en/latest/source/About%20Dashboard/#obtain-dashboard).

- [Prepare for Installation](#PrepareInstallation)
- [License](#License)
- [Installation Destination](#InstallDestination)
- [Email (Optional Custom Option)](#Email)
- [Active Directory - LDAP/S (Optional Custom Option](#LDAP)
- [Communication Protocol - HTTP(S) Setup](#HTTPS)
- [Set Database Password](#DBpass)
- [Final](#Final)
- [Login to Dashboard](#login)

<a name="PrepareInstallation"></a>
**Prepare for Installation**

1. Place your [SecureSuite license](https://cis-cat-pro-dashboard.readthedocs.io/en/latest/source/SecureSuite%20License/) on the CIS-CAT Pro Dashboard server
2. Download the latest CIS-CAT Pro Dashboard zip file from [CIS WorkBench](https://workbench.cisecurity.org/files), select the tag `CIS-CAT Dashboard` 
3. Place the zipped file on a host server that **has not** previously had CIS-CAT Pro Dashboard or CIS-CAT Pro Assessor installed
4. Unzip the files
5. Navigate to the directory where the installer is located.
6. Apply execute permission for the script as a user with `sudo` privileges
		sudo chmod +x CCPD_unix_Installer.sh 
5. Launch the installer shell script from any hard drive location as a user with `sudo` privileges
		sudo ./CCPD_unix_Installer.sh
	- Using -c after the script name will force command line installation
6. Select Standard or Custom Installation
	- **Standard:** Navigates required options only for most streamlined installation. 
	- **Custom:** Navigates required and selected optional, advanced settings. During navigation, selected optional settings can still be skipped.

  
![](img/Linux_Installer_Welcome.png)
  


<a name="License"></a>
** License **

A valid CIS issued SecureSuite license is required. The application may fail to load or some functions may not work as expected without a valid file. Offline license validation is performed utilizing only the license.xml file obtained from the CIS WorkBench.

![](img/Linux_Installer_License.png)

<a name="InstallDestination"></a>
** Installation Destination **

Select the main operating system drive for installation. For most Ubuntu environments, this will be `/usr/local/CCPD`. Ensure to allocate the system recommended space for this location.

![](img/Linux_Installer_Destination.png)

<a name="Email"></a>
** Email (Custom Option) **

The email configuration information is optional (NOT REQUIRED) and presented only if selected on the Welcome screen during the first installation or upgrade. Email configuration is required for self-service "forgot password" requests. Self-service password reset is not a required functionality as password resets can be managed by a system administrator. No other functionality or alerts utilize the email setup. All alerts will be sent to the Dashboard "Inbox".

CIS-CAT Pro Dashboard utilizes the Grails mail plugin that supports SMTP servers. Expand the advanced properties for additional email setup.

<a name="LDAP"></a>
** Active Directory - LDAP/S (Custom Option) **

LDAP(S) is an optional configuration. If configured, CIS-CAT Pro Dashboard will only authenticate with the active directory users and default CIS-CAT Dashboard users will be disabled. LDAP/Active Directory will be used to manage user authentication and permissions within CCPD.

LDAP/AD roles and user properties such as firstname, lastname and email will be imported. If the user doesn't exist in CCPD, the username will be created on login and granted with a basic user role (ROLE_USER) by default along with LDAP Roles.

**Requirements for LDAP/AD setup on system:**

- Email address is required to contain a valid value
- Group name must be uppercase
- Must contain a user called api user to support token generation
- Users created prior to LDAP integration, must have a username matching with the one in LDAP (uid) or AD (sAMAccountName, also called "User logon name")
- Port 389 availability
- SSL unchecked

**Additional Requirements for LDAPS**

- Certificate added to Dashboard's utilized java truststore
- Port 636 availability
- SSL selected

**Configuration Parameters **

| Configuration         |    Description |
| -----------------------| ------------- |
| Manager DN | Example: CN=Administrator,CN=Users,DC=corp,DC=cisecuritytest,DC=org |
| Manager Password | Credential for the Manager DN |
| Server | LDAP URL example: ldap://127.0.0.1:389  LDAPS URL example: ldaps://ldap.ciscat.ccp.sbp:636 |
| Group Search Base | Base directory for group search. Example: DC=corp,DC=cisecuritytest,DC=org |
| Group Search Filter | The pattern to be used for the user search. {0} is the user’s DN. Example: OpenLDAP: uniquemember={0} and AD: member={0} |
| Group Role Attribute | The ID of the attribute which contains the role name for a group. Example: CN |
| Search Base | Base directory for search. Example: DC=corp,DC=cisecuritytest,DC=org |
| Search Filter | Filter expression used in search. Example: OpenLDAP: (uid={0}) or AD: sAMAccountName={0} |
| Password Attribute Name | Example: userPassword|

<a name="HTTPS"></a>
** Communication Protocol - HTTP(S) Setup **

CIS-CAT Pro Dashboard will receive inbound configuration assessment result data from CIS-CAT Pro Assessor. Any protocol supports use of the API imports. 

Select the communication protocol that supports your organization policy. While in a testing phase, some Members have found it useful to start quickly with HTTP. Changes to protocol can be done by executing the installer application any time after initial install.

HTTPS protocol is recommended for production use. The installation will assist in creating a self-signed organizational certificate. It is also possible for organizations to utilize an organizational certificate. HTTPS requires port 443 to be available. The installation validates the availability of this port and will provide an alert if its unavailability is detected.

**Supported protocols:**

- HTTPS - Self-Signed
	- Requires port 443 availability
	- Certificate created using the installer
	- Certificate stored in `certificates` folder of root installation
	- Certificate password does NOT contain an @ or $ character
	- Valid for 90 days from creation
		- Alias (can be any description of the certificate), could place expiry date as part of description
		- Chrome browser warns of expiration
		- Update self-signed cert by executing installer and selecting `Update application and/or configuration settings`
	- CIS-CAT Pro Assessor commands must ignore SSL warnings if importing to Dashboard via API. See [Configuration Options](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Configuration%20Options/).
	
- HTTPS - Organizational Certificate

	- Requires port 443 availability
	- Obtain your organization's certificate from your Certificate Authority. The CIS-CAT Dashboard installation stores self-signed certificates to installationLocation\CCPD\certificates.
	- Create certificate service request (CSR) to generate a keystore file in .jks or .p12 format
		- Use tool of choice. [Some Members have found this site useful](https://www.digicert.com/kb/csr-ssl-installation/tomcat-keytool.htm#create_csr_keytool).
		- The name of the keystore file (often referred to as common name or alias, some Members use the Fully Qualified Domain Name for this value) and `password` screen entries **must** match the CSR and what is installed into your keystore
		- A new keystore is recommended. The CSR must come from the keystore planned for use.
	- Trust the certificate utilizing the command line during/post installation or via Google Chrome post installation (see trusting the certificate)
	- Ensure to specify a list of names covered by the SSL certificate in the Subject Alternative Name (SAN) in Google Chrome
	- Server may need to restarted to complete incorporation

- HTTP
	- Transmits data in clear text (typically chosen for quick startup during testing or proof of concept)
	- No certificate needed
	- CIS-CAT Pro Assessor commands must ignore SSL warnings if importing to Dashboard via API. See [Configuration Options](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Configuration%20Options/).	

![](img/Linux_Installer_HTTPS_SelfSign.png)
![](img/Linux_Installer_HTTPS_OrgCert.png)
![](img/Linux_Installer_HTTP.png)

<a name="DBpass"></a>		
** Set Database Password **

The MariaDB that supports CIS-CAT Pro Dashboard has a native admin user with the username `root`. Set a strong password with the following requirements:

- Minimum 14 characters
- Does not start with a character
- At least 1 lowercase letter
- At least 1 uppercase letter
- At least 1 number
- At least 1 of these special characters: `!#$%^` with no other special characters allowed


![](img/Linux_Installer_DBPass_new.png)

<a name="Final"></a>
** Final Installation Process **

The duration of the final steps of the installation can be 2 to 5 minutes. The initial services to support CIS-CAT Pro Dashboard take some time to start. The services installed are:

- CCPD Windows
- MariaDB

Once the installation detects that CIS-CAT Pro Dashboard is ready for use, the `Installation Complete` screen will be presented.

![](img/Linux_Installer_ServicesStarting.png)

Right click on the link to open CIS-CAT Pro Dashboard.

Depending on the communication protocol selection during installation, the CIS-CAT Pro Dashboard URL will be:

- HTTP: http://localhost:8080/CCPD/
- HTTPS: https://localhost/CCPD/

<a name="login"></a>
## Initial Dashboard Login ##

    username: admin 
    password: @admin123

You'll be prompted to change your password upon first login.

---------------------------

# Upgrade Process #

Each release of CIS-CAT Pro Dashboard v3.x will contain upgrades to the main CIS-CAT application and embedded components. Upgrades are applied utilizing the latest installer included in the downloaded CIS-CAT Pro Dashboard. On upgrade, the application will verify that the version installing is newer than the installed version and fail if this scenario is detected.

The installer will detect a previous installation and prompt to update only the application or update/modify configuration changes. If no changes are required, updating only the application is the most efficient. Follow the basic steps below. 

**NOTE:** There is no upgrade or migration path from CIS-CAT Pro Dashboard version 2.x to version 3.x. Please read our FAQ and our [blog](https://www.cisecurity.org/insights/blog/cis-cat-pro-is-now-even-better-heres-how-weve-improved-it) to learn more about CIS-CAT Pro changes.

1. Download the latest CIS-CAT Pro Dashboard zip file from [CIS WorkBench](https://workbench.cisecurity.org/files), select the tag `CIS-CAT Dashboard`
2. Place the zipped file on the CIS-CAT Dashboard host server where CIS-CAT Pro Dashboard v3.x is installed
3. Unzip the files
4. Launch the installer shell script
5. Select Standard or Custom Installation
	- **Update application only:** applies existing configuration, updates CIS-CAT application. No options to modify existing configurations.
	- **Update application and/or configuration settings:** applies existing configuration with options to modify some settings, updates CIS-CAT application. Select **optional** Email or LDAP configuration to modify or initiate these functions.

------------------
# Installation Errors #

Occasionally, a CIS-CAT Pro Dashboard installation or upgrade may result in an error.

- **Check Services:** Verify that `MariaDB` and `CIS-CAT Pro Dashboard` are started; start them if needed and try again after a few minutes.
- **Retry Installer:** Close and re-launch CCPD Installer. The installer will guide you through any necessary configuration.

If you are unsuccessful, collect logs that have been generated for you and open a support ticket. See further information below.

**Below are some error messages that may be received:**

- An error occurred starting up the CIS-CAT Pro Dashboard and/or MariaDB services. CIS-CAT Pro Dashboard is not working as intended.
	- CIS-CAT Pro Dashboard service isn't running after 10 minutes of waiting.
- An error occurred starting up the CIS-CAT Pro Dashboard and/or MariaDB services. MariaDB is not working as intended.
	- MariaDB service isn't running after 10 minutes of waiting.
- An error occurred starting up the CIS-CAT Pro Dashboard and/or MariaDB services. CIS-CAT Pro Dashboard is not working as intended. MariaDB is not working as intended.
	- CIS-CAT Pro Dashboard service and MariaDB service aren't running after 10 minutes of waiting.

** Obtaining Installer Logs **

During the installation, the Installer will create logs. The logs will be removed when the installation application is closed. If you receive an error during installation, please capture the Installer log before closing the application. Installation logs are created at `/tmp`. View this log for information regarding the installation or submit this file with your CIS Technical Support ticket when issues involve installation.
 

Additionally, CIS Technical Support may require any logs generated at this location: `/usr/local/CCPD/ccpdlogs`. 

Attach log files to your [Technical Support ticket](https://www.cisecurity.org/support/).

# Uninstall#

The Uninstaller application is located in the root directory of the original installation location. The uninstallation will remove all data and services supporting CIS-CAT Pro Dashboard. A restart is required to complete the uninstallation.

![](img/Linux_Installer_Uninstall.png)



# HTTPS Certificate Trust #

CIS-CAT Pro Dashboard is currently only supported using Google Chrome. Other browsers may produce unexpected behaviors. Self-signed certificates will produce warnings within the browser as they are not fully trusted. Organizational certificates will receive the below warning if they have not been added to the Java trust store.

To view the details of the certificate selected to support Dashboard, select the `Not secure` text to the left of the URL. Select 'Certificte is not valid' to review the certificate details. View the `Details` tab to view the information on the validity dates of the certificate. For self-signed certificates, the warning can be ignored by selecting `Advanced` and `Proceed to localost`. Per some organization's security policies, self-signed certificates are not permitted. 

![](img/Cert_notSecure.png)

![](img/Cert_valid.png)


To fully trust an organizational certificate issues from a certificate authority (CA) and to avoid browser trust warnings, add the certificate to the trust store. Ensure server is restarted to complete incorporation.