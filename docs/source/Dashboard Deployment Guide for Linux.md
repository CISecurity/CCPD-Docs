![](http://i.imgur.com/5yZfZi5.jpg)

------------------------------
# Environment Requirements #

The following environment characteristics are required.

**Server**

- A single Ubuntu 20.04 server
	- 8GB RAM
	- Minimum 10 GB disk space allocated to the main OS location
	- 2 vCPUs, 4 cores each
- Server does NOT currently host CIS-CAT Pro Dashboard v2.x 

The application does not heavily utilize processor and memory. Assessment result import process will increase the memory and processing usage. CIS-CAT recommends conducting assessment result imports via the API during low peak business hours to avoid disrupting other business activities.


Load balanced configurations are not supported.

**Browser**

- Google Chrome

Other browsers maybe produce unexpected behavior.

**Traffic and Ports**

- Internet available on the server during installation
- Port 3306 is available for Maria database installation
- Traffic allowed on port 8080 and 443
	- As needed, if installed on AWS, AWS security group must allow traffic on port 8080

**Other**

- No other applications present requiring system-installed Java runtime environment (JRE)
	- Including CIS-CAT Pro Assessor
- The main operating system drive must be selected for installation

# Installation Instructions #

For an initial CIS-CAT Pro Dashboard installation on Ubuntu Linux, follow the basic steps below. CIS-CAT has observed an initial installation effort on a prepared server to complete in less than 10 minutes. As the installation process will effect the Java home environment variables on the machine, CIS-CAT recommends that other applications requiring a system-installed java run time environment (JRE) are not present on the same host.

CIS-CAT Pro Dashboard requires a CIS SecureSuite license. Before initiating the installation process, download your organization's [SecureSuite license](https://cis-cat-pro-dashboard.readthedocs.io/en/latest/source/SecureSuite%20License/).

1. Place your [SecureSuite license](https://cis-cat-pro-dashboard.readthedocs.io/en/latest/source/SecureSuite%20License/) on the CIS-CAT Pro Dashboard server
2. Download the latest CIS-CAT Pro Dashboard zip file from [CIS WorkBench](https://workbench.cisecurity.org/files), select the tag `CIS-CAT Dashboard` 
3. Place the zipped file on a host server that **has not** previously had CIS-CAT Pro Dashboard or CIS-CAT Pro Assessor installed
4. Unzip the files
5. Launch the installer shell script from any hard drive location as `root`
		sudo ./CIS-CAT_Pro_Dashboard_Installer.sh
6. Select Standard or Custom Installation
	- **Standard:** Navigates through only required options for most streamlined installation. 
	- **Custom:** Navigates through required and optional, advanced settings. During navigation, selected optional settings can be skipped.

![](img/Linux_Installer_Welcome.png)


** License **

A valid CIS issued SecureSuite license is required. The application may fail to load or some functions may not work as expected without a valid file. Offline license validation is performed utilizing only the license.xml file obtained from the CIS WorkBench.

![](img/Linux_Installer_License.png)


** Installation Destination **

Select the main operating system drive for installation. For most Ubuntu environments, this will be `/usr/local/CCPD`. Ensure to allocate the system recommended space for this location.

![](img/Linux_Installer_Destination.png)



** Email (Custom Option) **

The email configuration information is optional and presented only if selected on the Welccome screen during the first installation or upgrade. Email configuration is required for self-service "forgot password" requests.

CIS-CAT Pro Dashboard utilizes the Grails mail plugin that supports SMTP servers. By default, an unsecured mail server is assumed and configured to at `localhost` on port `25`. This can be modified by expanding the advanced properties for email setup.

** Active Directory - LDAP/S (Custom Option) **

LDAP(S) is an optional configuration. If configured, CIS-CAT Pro Dashboard will only authenticate with the active directory users and default CIS-CAT Dashboard users will be disabled. LDAP/Active Directory will be used to manage user authentication and permissions within CCPD.

LDAP/AD roles and user properties such as firstname, lastname and email will be imported. If the user doesn't exist in CCPD, the username will be created on login and granted with a basic user role (ROLE\_USER) by default along with LDAP Roles.

**Requirements:**

- LDAP/AD email address is required to contain a valid value
- LDAP/AD group name must be uppercase
- LDAP/AD must contain a user called api user to support token generation
- LDAPS configuration must add the certificate to Dashboard's utilized java truststore
- LDAPS requires port 636 availability

![](img/Installer_LDAP.png)

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


**Need this?***

####LDAP/AD Requirements####
The email address is a required field, make sure that LDAP/AD user email field is set properly.

The entire group name needs to be in uppercase in LDAP/AD. 

If some users were previously created in CCPD before the LDAP integration, make sure the username matches with the one in LDAP (uid) or AD (sAMAccountName, also called "User logon name").  

The api user needs to be created in LDAP/AD in order to generate an authentication token to import Asset Report Format (ARF) results from CIS-CAT Assessor. 

Once LDAP/AD authentication is integrated to CCPD, the database authentication will be automatically disabled.


####Installer Logs
During the installation, the Installer will create logs. The logs will be created in a directory within the temporary directory of the operating system. Each finished installation will create an individual log with a timestamp. If you have trouble with the installation, please provide this log file on a [support ticket created on our support portal](https://www.cisecurity.org/support/). 

The permissions on the configuration file (ccpd-config.yml) and the logs directory for CIS-CAT Pro Dashboard need to allow the tomcat user to read and/or write.

<a name="confAndDeploymentManual"></a>
##Configuration and Deployment - Manual##
<b>This section describes how to configure and deploy the Dashboard manually.  For instructions on how to configure and deploy the Dashboard using the Installer, see [Configuration and Deployment - Installer](#confAndDeploymentInstaller).</b>

At this point, it is prudent to deploy the CIS-CAT Pro Dashboard application (the "war") included in the downloadable bundle.  The initial deployment of the web application can then be tested via direct connection to the application server on port `8080`, without the web server.  This can help identify any application or application server misconfigurations prior to web server installation/configuration.



**Proxy information- do we need?**

The `ServerName` should be the `<public url of application server>`

Execute the following commands to enable the proxy module:

    sudo a2enmod proxy
    sudo a2enmod proxy_ajp
    sudo a2enmod proxy_http
    sudo service apache2 restart

Execute the following commands to enable the reverse proxy to Tomcat:

    sudo a2ensite ccpd.conf
    sudo service apache2 reload

The Apache HTTP server should now be configured to serve requests to CIS-CAT Pro Dashboard.  The application should be available at the URL entered into your `ccpd-config.yml`: `http://<public url http server>/CCPD`

### Securing Web Traffic ###
The steps above will have the CIS-CAT Pro Dashboard application running over normal HTTP on port `80`.  This presents a risk as data, including user credentials, will be transmitted in clear text.  It is recommended that traffic be secured using HTTPS.  The following article explains how to create a self-signed certificate and apply it to a web server in Ubuntu 18.04: [https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-18-04)

**NOTE:** 
After completing the steps in the article, you will have to change your connector in ccpd.conf to use port 443 instead of port 80.  Also, when you chose a common name in the certificate creation process, the name must match the DNS name portion of the serverURL in ccpd-config.yml.  i.e.  if your serverURL is https://www.example.com/CCPD, then the common name in the certificate must be www.example.com

### Ensuring Trust ###
In the browser's URL bar, navigate to the CIS-CAT Pro Dashboard application.  Click on the HTTPS certificate chain (next to URL address). In the Google Chrome browser, if the user sees a "Not Secure" label next to the URL, the certificate is not trusted.  Click on the "Not Secure" link to display the certificate information:

- Click the "Details" link to display the "Security Overview" information.
- Click on the "View Certificate" button to display the certificate details.

The certificate information needs to be exported, and added to the servers trust store.  On the "details" tab of the certificate information, click the "Copy to File..." button.  The "certificate export wizard" will be displayed.

- Click the "Next" button to navigate to the second screen, the export type selection:

Select the "DER encoded binary X.509 (.CER)" radio button.  This selection should be the default.  Click "Next" to continue.

Select or browse to a location to where the `.cer` file will be saved.  Clicking "Next" and finally "Finish" to complete the wizard and save the file to the selected location/filename.  This file will need to be transferred via SCP, S/FTP to the application server hosting the CIS-CAT Pro Dashboard application.  Note the location to which the file is transferred.  For the purposes of this User's Guide, assume the location of the `ccpd_cert.cer` file is `/home/ubuntu/ccpd_cert.cer`.

#### Importing the certificate into the java trust store ####
To POST reports to Dashboard from Assessor using the `POST Reports to URL` option with HTTPS, a certificate must be imported to the java trust store.

- Locate JRE, JDK, or openJDK used to launch Tomcat on the Tomcat/Dashboard server
- Note the location of the `cacerts` file prior to importing certificate to `keytool`
	- For example, if OpenJDK is located at `usr/lib/jvm/jdk-11.0.9.101`, then `cacerts` file will be located in `usr/lib/jvm/jdk-11.0.9.101\lib\security\cacerts`
- Use java `keytool` application to import the certificate:

   	 	# Navigate to the $JAVA_HOME folder's bin directory
   		 cd /usr/lib/jvm/jdk-11.0.9.101/bin
     
   	 	# Execute keytool
    	sudo keytool -import -alias ccpd -keystore jre/lib/security/cacerts -file /home/ubuntu/ccpd_cert.cer

- Enter keystore credentials at prompt.  By default, this credential is `changeit`.
- Answer `yes` to import the certificate into the trust store
 		
		# The user will be asked for confirmation
    	Trust this certificate? [no]:

- Restart application server to incorporate trust store









