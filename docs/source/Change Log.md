![](http://i.imgur.com/5yZfZi5.jpg)

**CIS-CAT Pro Dashboard Change Log**

# 3.0.1 #
December 21, 2022

**Benchmarks**

- Alma Linux 9 v1.0.0
- Microsoft IIS 10 v1.2.0
- Microsoft Office Enterprise v1.0.0
- NGINX v2.0.0
- Oracle Cloud Infrastructure Container Engine for Kubernetes(OKE) Benchmark v1.2.0
- Oracle Linux 9 v1.0.0 
- Red Hat OpenShift Container Platform v4 v1.3.0
- Rocky Linux 9 v1.0.0

The following CIS Benchmarks included in CIS-CAT Pro Dashboard have moved to end of life and are no longer officially supported. See the [Assessor Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/) for more information on CIS Benchmarks that have reached end of life.

- Amazon Linux v2.0.0

** Security **

- Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/cp/GwThzTEn) for more information.

** Application **

- none

** Documentation **

- Updated [CIS Benchmark Support guide](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Benchmark%20Coverage/) with updated content


# 3.0.0 #
December 12, 2022

**Read our [blog to learn more about these changes](https://www.cisecurity.org/insights/blog/cis-cat-pro-is-now-even-better-heres-how-weve-improved-it).**

**Benchmarks**

- See [CIS Benchmark Support guide](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Benchmark%20Coverage/) for supported CIS Benchmarks in datastream format.

** Security **

- The ccpd-config.yml (stored in “conf” folder) supporting the CIS-CAT Pro Dashboard operation now limits read/write privileges to only privileged Microsoft Windows or Linux users.

** Application **

- System requirements for installation modified to require and support only
	- One Dashboard Host server: Ubuntu Linux 20.04 OR Microsoft Windows Server 2016/2019
- Downloaded file changed:
	- Microsoft Windows:  CIS-CAT-Dashboard-v3.0.0-windows.zip
	- Ubuntu Linux:  CIS-CAT-Dashboard-v3.0.0-linux.zip
- Installation process streamlined:
	- All standard components embedded (Database - MariaDB, JRE - openJDK 8, Tomcat 9)
	- Valid CIS SecureSuite license required. Alerts when license not valid (expired/null)
	- Standard (minimum - streamlined) or Custom (advanced options) installation options
	- Options within installer to generate self-signed certification to support HTTPS
	- Port availability validation of required installation ports based on selected options (Ex: 8080, 443, 3306, etc.)
- The configuration assessment import process has significantly been improved. On average, configuration reports will import in less than 30 seconds.
- LDAPS, allowing for encryption of LDAP data such as user credentials, for Active Directory services now supported.
- Single system remote assessment functionality now embedded as standard feature (replaces deprecated Assessor v4 Service). Currently supported only for SSH and Microsoft Windows over HTTP. See how to configure target endpoints with **[WinRM over HTTP](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#macos-sessions)**.
- Dashboard functions to support vulnerability assessment have been removed. CIS-CAT now exclusively performs and supports configuration assessments primarily for CIS Benchmarks with automated assessment content. Please see our [knowledge base article](https://cisecurity.atlassian.net/l/cp/CLRHc4H4) for more information.
- Integration to CIS WorkBench has been temporarily disabled in version 3 of Dashboard. This feature will return in 2023 and coordinate with new Dashboard retrieval method in CIS WorkBench.

** Documentation **

- Updated all installation requirements and instructions
- The README.txt has been updated to represent Dashboard v3.0.0 information

# Archive - Version 2.x #

CIS-CAT Pro Dashboard v2.3.2 - FINAL version 2 series.**
November 15, 2022

Due to critical security vulnerabilities in the end of life CIS-CAT Pro Dashboard version 2 and the availability of version 3 (planned December 2022), CIS has released one last version of Dashboard version 2 series. CIS understands that some organizations will need time to adopt version 3 of Dashboard when it becomes available in December 2022.
There have been no changes to the Deployment or User Guides.

Version 2.3.2 will be the final release of CIS-CAT Pro Dashboard version 2 series. Dashboard version 3.0.0 will replace the 2.x versions in early Q4 2022, but will not be backwards compatible. A clean install of Dashboard version 3.0.0 will be required as there will be no upgrade or data migration options available from any previous 2.x version.

**[Read our knowledgebase article to learn more.](https://cisecurity.atlassian.net/l/cp/mF6o97vs)**

** Application **

- N/A

** Security **

- Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/cp/F18Ag1af) for more information.


** Documentation **

- N/A


**CIS-CAT Pro Dashboard v2.3.1**
September 21, 2022

Version 2.3.1 will be the final release of CIS-CAT Pro Dashboard version 2 series. Dashboard version 3.0.0 will replace the 2.x versions in early Q4 2022, but will not be backwards compatible. A clean install of Dashboard version 3.0.0 will be required as there will be no upgrade or data migration options available from any previous 2.x version.

**[Read our knowledgebase article to learn more.](https://cisecurity.atlassian.net/l/cp/mF6o97vs)**

** Application **

- Palo Alto configuration assessment reports now import successfully.


** Security **

- Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/cp/SwQhuzoA) for more information.


** Documentation **

- Updated Deployment and User Guides to include End of Life information.


** CIS-CAT Pro Dashboard v2.3.0 **
May 3, 2022

** Application **

- Configuration exceptions in `Approved` status where a Target Primary ID is present can now be edited by a user assigned ROLE_ADMIN from the `Configuration Exception Search` page under the `Reports` Menu. Upon submission, configuration report scores will be recalculated. Edits do not require exception workflow approval and will be effective immediately. 


** Security **

- Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/c/PPB351PN) for more information.
	- Upgrade Grails Framework from v4.0.11 to v5.1.7, which facilitated upgrade to vulnerable Spring Framework libraries


** Documentation **

- Updated User Guide to include information on how to edit an exception.

--------------------
** CIS-CAT Pro Dashboard v2.2.6 **
April 5, 2022

** Application **

- None

** Security **

-   Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/c/w3C5QBPi) for more information.


** Documentation **

-   None


----------
** CIS-CAT Pro Dashboard v2.2.5 **
March 22, 2022

** Application **

- Increased performance of assessment report import duration issue when low score alerts are utilized.
- CVE and CVSS data from the National Vulnerability Database (NVD) for 2022 are now available to support the CIS-CAT Assessor vulnerability reports. Ensure to update the NVD data from the Dashboard menu.

** Security **

- The README.txt file now contains information about third party dependent libraries that may appear on vulnerability reports.

** Documentation **

-   None

----------
** CIS-CAT Pro Dashboard v2.2.4 **
February 17, 2022

** Application **

- Resolved an issue of where importing assessment reports took an excessive amount of time. The import process speed has been improved.
- An export error corrected for configuration report XML format.

** Security **

-   Resolved security vulnerability present in embedded, third party dependencies. 


Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/c/yNXeaPPw) for more information regarding the security updates.

** Documentation **

-   The Dashboard Windows Configuration Guide has been updated with working links in the "Creating a Self-Signed Certificate using Windows Powershell"

----------
** CIS-CAT Pro Dashboard v2.2.3 **
December 7, 2021

** Application **

-  None

** Security **

-  Resolved security vulnerabilities present in framework dependencies:
	-  Bootstrap
	-  Jquery
	-  Jquery UI

Please see the related [knowledge base article](https://cisecurity.atlassian.net/servicedesk/customer/portal/15/article/2416148561) for more information regarding the security updates.

** Documentation **

-   Update Windows and Linux Deployment Guide to remove Assessor v3 integration instructions.

------------------
** CIS-CAT Pro Dashboard v2.2.2 **
November 9, 2021

** Application **

-  None

** Security **

-  Dashboard users are now limited to:
	-  Modifying only their own Alert Opt In/Opt Out settings
	-  Deleting their own Alert messages
	-  Adding/deleting their own favorites (ie: favorite Benchmark on the Benchmark View graph)
-  Resolved a security vulnerabilities present in one embedded, third party dependencies. 

Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/c/7UBQbXCP) for more information regarding the security updates.

** Documentation **

-   None

---------------------
** CIS-CAT Pro Dashboard v2.2.1 **
September 23, 2021

** Application **


-  Resolved an issue causing some assessment reports to fail to import when several reports were automatically imported via the API.
-  Configuration assessment scores correctly updated on exception approval.
-  Dashboard users with expired password are now able to reset the password from the application.
-  Malformed files imported to the Dashboard via API will now properly move to error folder instead of stopping additional file imports.
-  Modified the "Create New User" screen with enforcement of the required data entry.
-  Rule level details in the Configuration Assessment Difference Report can now be expanded.
-  The Dashboard installer will now continue to work with supported, stable versions of Java (JRE, JDK, openJDK) of 8 and 11. 
-  Corrected an issue where a configuration result would fail to import when no system information was collected for a particular check.

** Security **

-  Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/c/HvCmoNP4) for more information.

** Documentation **

-   Preferred component section of the Configuration Guide specifies that if selecting components other than preferred components, OS compatibility with required components should be verified. 

-------------------
** CIS-CAT Pro Dashboard v2.2.0 **
July 1, 2021

** CIS-CAT Pro Updates **


-  NEW report: **Configuration Assessment Result Summary**
	-  Summary list of failing recommendations by benchmark profile and version and system count for each fail result
	-  System count results for most recent result data
	-  Excludes excepted results
	-  Export target details for selected report results to csv format
-  CIS Controls V8 Support
	-  Views no longer display CIS Controls V6 as V6 has reached end of life
	-  Configuration assessment views include Controls V8 reference when present on CIS Benchmarks. All CIS Benchmarks published after May 18, 2021 will include Controls V8 reference. Follow the [CIS-CAT Pro Assessor v4 Change Log](https://ccpa-docs.readthedocs.io/en/latest/Change%20Log/*change-log) for new Benchmark versions.
	-  Previously imported CIS official Benchmarks released in CIS-CAT Pro Assessor v4.7.0 will now show Controls 8 cross references to recommendations in the Controls View of a single assessment result.
-  Dashboard Installer updated to generate configuration file consistent with Oracle database 12c, 18c, 19c support (10c dialect removed and replaced with 12c)
-  Resolved error for Assessment result import for supported Oracle databases
-  The configuration assessment import process now correctly stores complex results enabling full display of result evidence when viewing a configuration assessment. Effective on new imports with Dashboard v2.2.0+.
-  Additional verification added to ensure each user can only change their own password in the user profile.


** Documentation Updates **

- Deployment Guide updates
	 - Windows and Linux Deployment guide indicates load balanced configurations are not currently supported.
	 - Oracle database supported versions as a database component for Dashboard include 12c, 18c, and 19c.
- Updated Windows Deployment Guide to indicate supported OS includes Windows 2019
- Updated Linux Deployment Guide to indicate supported OS includes Ubuntu 18.04


-------------------------------
** CIS-CAT Pro Dashboard v2.1.0 **
April 14,2021

** CIS-CAT Pro Updates **

-  Resolved an error with Active Directory and LDAP integration when using Dashboard v2.1.0+.
-  Improvements to HTML exported reports for an individual configuration report
	-  Now consistent with Assessor v4 HTML format
	-  Advanced evidence available in the report when results imported to Dashboard in versions 2.1.0+ (reports for assessment results imported prior to version 2.1.0 will be in old format) 	  
	-  Imported configuration results to Dashboard version 2.1.0+ now compressed and stored to enable fast HTML export without error
	-  Configuration results utilizing CIS' proprietary Embedded Check Language (ECL) AND imported prior to Dashboard version 2.1.0 is not supported (results from benchmarks where there is an absence of "oval" or "xccdf" in the filename)
-  Assessment results will now import successfully to Dashboard when mac addresses are > 60 characters, which adds support for infiniband devices.
-  Configuration assessment result screen now correctly include "unknown" and "error" results. Views streamlined and help text added.
-  Improved web application security by removing unneeded menu items, such as the Collections menu.
-  Security access for Dashboard users streamlined to include 3 security roles with pre-defined functional access.
-  Resolved issue with display of Target System IPs in Target System search results.
-  Resolved an issue with resetting the password.
-  Target System and Benchmark View graphs updated to allow selection of the check box when choosing data to display.


** Documentation Updates **

- User Guide updates
	 - Updated scoring information available in guide on configuration assessment view screen. Screen shots updated to show new "unknown" and "error" columns.
	 - Updated functionality on user roles
- Updated Windows Deployment Guide to indicate supported database component now includes Microsoft SQL Server 2019 to support storage of Dashboard data.


---------------------------
** CIS-CAT Pro Dashboard v2.0.0 **
January 20, 2021

** CIS-CAT Pro Updates **

- Baseline framework upgrade that includes:
	- Grails v4.0.4 which includes upgrades to Spring and Spring Boot
	- Spring Security v5.1.6
- 2021 vulnerability definitions, downloaded from NIST, are now supported.
- New CVE definitions will now correctly attach to existing vulnerability data in the database when utilizing the "Attach CVEs to Existing Definitions" button.
- Support and compatibility offered for Apache Tomcat 9 and Java Runtime Environment (JRE) 8 to 11.
- Unsupported files will be moved to the error folder when manually dropped into the legacy import folder.
- Purged assessment reports are no longer returned in assessment report result searches.

**NOTE:** This is a major upgrade to Dashboard. Please ensure to backup your database and deploy in a test environment. It is highly recommended to utilize the Dashboard Installer as formats of the configuration has changed due to the Grails upgrade. Please check the Windows and Linux Deployment guides for updates to `ccpd-config.yml` formatting.

** Documentation Updates **

 - Modifications to Linux and Windows Deployment Guide
	 - Application Server and java components contain more detail
	 - Support for Apache Tomcat 9 added
	 - Support for Java Runtime Environment 8 through 11
	 - Updated link for product support portal
	 - Additional detail added to Java configuration to ensure successful report exports from the Dashboard
 - IIS configuration instructions updated to support optional authentication with CIS WorkBench for receiving in-application alerts on new CIS-CAT Pro releases.
 
--------------------------------- 
** CIS-CAT Pro Dashboard v1.1.13 **
May 5, 2020

** CIS-CAT Pro Updates **

- Support added to facilitate import of configuration assessment results for CIS Benchmark VMWare ESXi 6.7.

** Documentation Updates **

 - Updated Java requirements to indicate that Java 8.251+ is not supported.

---------------------------
** CIS-CAT Pro Dashboard v1.1.12 **

** CIS-CAT Pro Updates **

- Multi-select configuration assessment report(s) for daily delete from database.
- In-Dashboard alerts will now occur for new versions of Assessor v4 Service.
- Full 2020 vulnerability definitions, downloaded from NIST, are now supported.
- Resolved error on target system delete when ad hoc assessment job records exist for deleted target.

** Documentation Updates **

 - Documentation and Dashboard installer updated to support recommended location of import directories as residing in the Tomcat structure.
 - User guide emphasizes requirement of direct internet connectivity when integrated with CIS Workbench and downloading updated NVD Data from NIST.
 - Corrected key tool file path mentioned in Linux Deployment section in guide.

-------------------------------
** CIS-CAT Pro Dashboard v1.1.11 **

** CIS-CAT Pro Updates **

- Ability to orchestrate a remote ad-hoc assessment for an individual target system with a selected CIS Benchmark.

- Delete buttons, such as assessment report delete, will now only allow users to click once. Deletion is assumed "in progress" when the button is disabled.

**IMPORTANT**: To use the remote ad-hoc assessment capability, installation of CIS-CAT Pro Assessor v4 Service v1.0.0+ is required.

-----------------------------------
** CIS-CAT Pro Dashboard v1.1.10 **

** CIS-CAT Pro Updates **

 - Members now have the option to receive an in-application alert when a new CIS-CAT Pro release has been uploaded to CIS WorkBench. Requires some setup in Dashboard Setting menu to configure an integration with CIS WorkBench.

**IMPORTANT**: To receive new release alerts, make sure the application has the **write privileges** to **ccpd-config.yml** file.

---------------------------
** CIS-CAT Pro Dashboard v1.1.9 **

** CIS-CAT Pro Updates **

 - The result import process has been modified to decompress and import result XML reports from CIS-CAT Pro Assessor v4 when sent via the API. Compressed reports will be sent when the Assessor v4 property is set to compress result XML reports.
 - The tag field on an individual target system is read only for users without the admin role.
 
** Documentation Updates **

 - More emphasis added on required UTF-8 encoding set for Tomcat configuration.
 - The supported version of Maria DB has been specified in the online documentation.
 - More emphasis on the type of MS SQL server User required for Dashboard installation.

----------------------------
** CIS-CAT Pro Dashboard v1.1.8 **

** CIS-CAT Pro Updates **

 - Support for NIST vulnerability JSON data feeds version 1.1 including the latest information. **Important: because of NIST XML Vulnerability Feed retirement, import of NVD feeds in XML format is no longer supported in the Dashboard.**
 - CIS Benchmark version number added to Configuration Exception Search, Individual Target - Configuration Tab, and Assessment Results List.
 - New auto complete function displays existing tags for selection in the tag field in the Exception popup and Dashboard Tag Chart.
 - Target system tag assignment is now only available to users with Admin role in individual Target screens.
 - Target Search screen now allows other criteria combination when searching by primary ID.
 - Dashboard Installer process now creates MySQL databases with UTF-8 character sets.
 - Help text added to Linux installer process regarding import folder permissions.
 
** Documentation Updates **

 - CIS-CAT Pro Dashboard Upload Report API defined. Located in Linux and Windows Deployment section as a subsection titled "Dashboard API."
 - Manual instructions for MySQL database installation updated to include accommodation for UTF-8 character sets.
 - Tomcat installation visual material now consistent with written instruction.
 
---------------------------------
** CIS-CAT Pro Dashboard v1.1.7 **

FUNCTIONAL ENHANCEMENTS

 - Enhanced process for adding and removing tags to target system allows for updates in bulk vs. single target system updates. Available on the Target search screen only to users with admin role. 
 - Search by IPv4 IP range has been added to the Target search screen.
 - New autocomplete function displays existing tags in the Target search screen tag field. Enter a space to show all tags.

SYSTEM ENHANCEMENTS

 - Target system deletion is now only available to users with admin role.
 - Target System Identifier deletion, edit, and creation is now only available to users with admin role.
 - Configuration and Vulnerability assessments deletion is now only available to users with admin role.
 - Configuration assessment and difference reports now show "no collected data" in the assessment section of a recommendation when the result is 'unknown' or 'not selected'.
 
DOCUMENTATION UPDATES

 - Linux/Windows deployment introduction modified to clearly define CIS-Supported components required for Dashboard operation.
 - Component documentation modified to indicate official support of Google Chrome web browser for CIS-CAT Pro Dashboard.
 
-------------------------------------

** CIS-CAT Pro Dashboard v1.1.6 **

SYSTEM ENHANCEMENTS

 - Supports MacOS 10.13 CIS Benchmark.
 - Updated, more consistent schema validation process upon vulnerability report import. Per existing functionality, reports failing validation will generate a Dashboard inbox alert and will be moved to the error directory.
 - New users will be assigned ROLE_USER and ROLE_BASIC_USER on default upon creation.

BUGS

 - Updated vulnerability validation process on import of a Windows 10 vulnerability assessment from CIS-CAT Pro Assessor v4. 
 - Resolved error on configuration assessment report display when no evidence is collected.
 - HTML reports display 4 digit Benchmark version numbers
 
DOCUMENTATION UPDATES

 - Dashboard and Assessor documentation configuration updated for tool integration. Instructions in the online Dashboard documentation is now more clearly defined by modifying some text and moving around sections of the instructions.
 - Linux Deployment instructions enhanced. Many clients required additional information regarding legacy/import folder permissions and configuration. 

-------------------------------------
** CIS-CAT Pro Dashboard v1.1.5 **

FUNCTIONAL ENHANCEMENTS

 - CIS Controls V7.0 support: For Benchmarks mapped to CIS Controls, users can view how recommendations relate to CIS Controls. See our upcoming blog to learn more. 
 - The CIS-CAT Pro Dashboard's HTML report has been modified in style to match the Assessor's HTML report for consistency purposes. 
 - For Dashboard Installer users, existing database settings will be detected and used instead of changed to CIS-CAT recommended settings.


SYSTEM ENHANCEMENTS

 - Oracle users upgrading from Dashboard versions prior to 1.1.3 will benefit from better database performance due to established indexing. Oracle users who have upgraded to Dashboard versions 1.1.3 or later to 1.1.5, will obtain the necessary indexes on upgrade. 
 - The Installer has been whitelisted with Symantec anti-virus. 

BUGS

 - Resolved an issue for SQL Server users when drilling down on the Benchmark View chart. 

----------------------------------------
** CIS-CAT Pro Dashboard v1.1.4 **

FUNCTIONAL ENHANCEMENTS

 - Installation and Upgrade Tool: A step-by-step embedded tool for the install/upgrade of dashboard that steps members through each process.
 - Graphs Viewable With or Without Internet Connectivity: CIS-CAT Pro Dashboard can now display assessment results in a graphical form whether your application server is on or off-line.

SYSTEM ENHANCEMENTS

 - MySQL database driver replaced by Maria DB driver (increase performance). **IMPORTANT: in ccpd-config.yml, "com.mysql.cj.jdbc.Driver" driverClassName needs to be replaced by "org.mariadb.jdbc.Driver". Can be done with the Installer or manually.**
 - Jobs run in succession (queue) to avoid simultaneous access to the database.

BUGS

 - Fixed reset password link and password expired redirection for users using a webserver. 
 - Fixed a bug when importing duplicate oval variables.
 - Fixed a bug when importing benchmark front-matter and rear-matter xml elements.

-----------------------------
** CIS-CAT Pro Dashboard v1.1.3 **

FUNCTIONAL ENHANCEMENTS

 - Implemented a Difference Report for comparing an assessment result with the previous assessment result.
 - Added ability to delete individual Configuration Assessments and Vulnerability Assessments.
 - Conversion abilities to convert existing data to the new data model.
 - Added ability to attach existing vulnerability assessments to NVD data updated after the import of the assessment.

SYSTEM ENHANCEMENTS

 - Delete target systems Performance improvements.
 - Added "Attach CVEs to Existing Definitions" button on the Vulnerabilities List.  This will allow NVD data to be imported after vulnerability assessments.
 - New Assessment Data Model which will offer performance improvements in: Import, Export, Delete functionality.
 - Support for WebLogic appliction server

BUGS

 - automated database changes required when updating from a version prior to v1.1.2.

-------------------------
** CIS-CAT Pro Dashboard v1.1.2 **

SYSTEM ENHANCEMENTS

 - Import Performance improvements.
 - Implemented a new way to identify duplicate imports, to maintain a smaller and more accurate version of content, especially OVAL content.

BUGS

 - Fixed a bug with imports sometimes misidentifing duplicate target systems
 - Fixed a bug with importing of older CIS content, such as AIX 6 results.

------------------------------------- 
** CIS-CAT Pro Dashboard v1.1.0 **

FUNCTIONAL ENHANCEMENTS

 - CCPD can now except custom target system identifiers from CIS-CAT Pro Assessor.  A custom element can be configured in CIS-CAT Pro Assessor to be passed to CCPD via the import functionality.
 - Group Exceptions - you can now add exceptions to entire groups or sub-groups of recommendations
 - Vulnerability Reports - you can now upload vulnerability reports from CIS-CAT Pro Assessor.  These reports also have exception funcitonality like the configuration assessment reports
 - Vulnerability Dashboard - you can view your vulnerability data over time using the Vulnerability Dashboard.
 - NVD Data Import - you can now import CVE and CVSS information directly from the NVD.  This data is used to support vulnerability report scoring

 
SYSTEM ENHANCEMENTS

 - Target System UI - redesigned to better present information,  including the profile level of each asseessment result.  added tabs for configuration results and vulnerability results.
 - Improved performance on Complete Report and Remediation Report exports.

BUGS

 - fixed a bug from 1.0.5 where importing subsequent ARF files would create additional Target System records


---------------------------------------
** CIS-CAT Pro Dashboard v1.0.5 **

FUNCTIONAL ENHANCEMENTS

 - Added Title information to the alert dialog
 - User Favorites - added a user favorites section where users can mark their favorite benchmarks or target systems.  The Benchmark Dashboard and Target System Dashboard now use user favorites to display the options available for graphing
 - Inbox UI Improvements
   - added an All/Unread toggle to the User Inbox to easily view only unread messages.  
   - added orange text to unread tasks in the User Inbox, to provide a visual distinction from other types of unread alerts.
   - added batch delete and mark read/unread to the User Inbox
 - Exception workflow - added alerting to recipient list when an exception is approved/rejected.  Previously the alert would just go to the requester, now it will go to everyone on the recipient list, which can be managed in the admin section
 - added security to exception end dating to only allow ROLE_ADMIN to end date exceptions
 - Exception End date alert - recipient list will be notified when an exception is end dated
 
SYSTEM ENHANCEMENTS

 - Target System Primary Identification customization - added ability to customize the primary identifier used for target systesms at an application level, and per target system.  By default, hostname will be the primary identifier of all target systems, but you can now change to use another identifier type, such as fqdn, mac-address, or a custom identifier.

BUGS

 - fixed bug where CCPD would not run using SQL Server 2014
 - fixed missing "Back" button on Target Systems Dashboarad when toggling between multi/single view
 - fixed bug preventing deletion of target systems
 
---------------------------------------- 
** CIS-CAT Pro Dashboard v1.0.4.1 **

FUNCTIONAL ENHANCEMENTS

 - Device View Dashboard - you can now search by device, or multiple devices, instead of having them all listed.

SYSTEM ENHANCEMENTS


BUGS

 - fixed bug where viewing assessment results would make the end time on the report 12:00am
 - fixed an import bug where missing oval definitions would cause an import to fail.

--------------------------
** CIS-CAT Pro Dashboard v1.0.4 **


FUNCTIONAL ENHANCEMENTS

 - Alerting functionality 
 - users will now receive configurable alerts for: Test Results imported,  Low Scoring Results imported, Errors importing Results
 - Exception Workflow  - when an exception is created it will go into a Pending status, and an task will be created to approve/reject the exception.  this defaults to users with ROLE_ADMIN, but is configurable
 - User Inbox - new inbox on the menu bar for alerts and workflow tasks
 - Exceptions View on Test Results - a new view was added to Test Results to show all exceptions that apply to that test result in a single list.
 - Exceptions by Target System - the target system screen now displays all exceptions that apply to that target
 - Exceptions Search - you can now search for exceptions by: Target System, Tag, Benchmark, Dates
 - User Tags - users can now be tagged, this allows for alerts to be sent to users by tag
 - Role Tags - Roles can now be tagged, no current functionality is effected by this.
 - Added hostname to the Target System Search, Remediation Report Search, Complete Results Search

SYSTEM ENHANCEMENTS

 - Added support for Oracle Databases
 - Added Support for SQL Server databases
 - Performance improvements for the import process
 - CCPD software version now appears on the title bar
 - Functional Area now applicable by action - the functional areas for security use to only be able to control access at the controller level,  administrators can now control access at the action level, whichi is much more granular

BUGS

 - fixed vulnerability where a basic user could become an administrator

----------------------------------
** CIS-CAT Pro Dashboard v1.0.3 **

FUNCTIONAL ENHANCEMENTS

 - Ability to Tag Users
 - Ability to Tag Roles
 - Ability to Search Users
 - Profile selected added to the Assessment Results List and Assessment Results Search pages.

SYSTEM ENHANCEMENTS

 - Performance improvements on Assessment Result Importing

BUGS

 - Fixed concurrency issues when uploading and importing Assessment Results simultaneously

-----------------------------
** CIS-CAT Pro Dashboard v1.0.2 **

FUNCTIONAL ENHANCEMENTS

 - Assessment Results Search page has been added to the Reports menu.  Users can now search for assessment results by: hostname, date range, benchmark, and tags.
 - Exceptions added in CCPD will now show in the HTML export document.
 - Added guidance on the dashboard screens to explain the data.
 - Months now appear by name instead of number on the Dashboard Graphs for improved readability.
 - Added a rule to prevent duplicate assessment results imports.
 - Added links to the CCPD User Guide, and The CIS WorkBench, in the main navigation menu at the top right of the application.

SYSTEM ENHANCEMENTS

 - Created an initialization service to process data fixes required for new releases, bypassing the need to manually run data scripts.
 - Made search criteria modular so that criteria and new searches can be added to the system easier.
 - Assessment Results List now uses a pre-calculated score, which improves performance.
 - Assessment Result import/export processes now use the weight from the XCCDF rule-result element of the TestResult, instead of the rule element of the Benchmark.
 - Made performance improvements to the Assessment Results View page.

BUGS

 - Users can now import assessment results from target systems with underscores in their hostname.
 - Users can no longer access user functionality when unauthenticated.
 - Dashboard scoring calculations to include recommendation weights and exceptions.
 - All users are now assigned ROLE_BASIC_USER which allows access to user functionality: profile, forgot password, password reset.
 - HTML export will now take the weight of a recommendation from the results rather than the benchmark, as the imported version could have different weights than the results.
 - Users with ROLE_API can no loger be added to other roles on the Show Role Screen.
 - Remediation Reports with no failed rules will now show a congratulatory message instead of a blank result.
 - Assessment Results can now be imported concurrently

-----------------------------
** CIS-CAT Pro Dashboard v1.0.1 **
 - Converted documentation to online documents available at: http://cis-cat-pro-dashboard.readthedocs.io
 - Fixed issues with CIS-CAT Pro Dashboard running on tomcat v8.5.11 including:
	 - user/role administration dialogs not working
	 - dashboards not showing
 - Fixed scoring inconsistency between the Assessment Results List, individual Assessment Results View screen, and the HTML export of the assessment results.  The inconsistancy  was the result of weighting of recommendations and exceptions added to recommendations

--------------------------------- 
** CIS-CAT Pro Dashboard v1.0 **
Initial Release
 