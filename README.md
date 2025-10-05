# SOC Automation Project

## Objective

This project focuses on building an automated Security Operations Center (SOC) environment to detect and respond to threats. It involves setting up a Windows 11 VM with Sysmon for logging, deploying Wazuh as a SIEM for monitoring and alerting, integrating TheHive for incident case management, and using Shuffle for workflow automation. The setup simulates detection of malicious activities like Mimikatz execution, automates hash analysis with VirusTotal, and sends alerts to analysts, enhancing incident response efficiency.

### Skills Learned

- Proficiency in deploying and configuring virtual machines and cloud environments.
- Understanding of endpoint monitoring tools like Sysmon and SIEM systems like Wazuh.
- Experience with incident management platforms such as TheHive and its dependencies (Cassandra, Elasticsearch).
- Automation of security workflows using tools like Shuffle, including webhook integrations and API connections.
- Creation of custom detection rules, log analysis, and integration with threat intelligence services like VirusTotal.
- Knowledge of threat simulation (e.g., using Mimikatz) and automated alerting via email.

### Tools Used

- Oracle VirtualBox for creating Windows 11 virtual machines.
- Sysmon for advanced Windows event logging.
- Wazuh as the SIEM for log collection, analysis, and alerting.
- TheHive for incident response and case management.
- Apache Cassandra and Elasticsearch as backend databases for TheHive.
- Shuffle.io for orchestrating security automation workflows.
- VirusTotal for hash-based threat intelligence.
- Mimikatz for simulating credential dumping attacks.
- Ubuntu 24.04 for hosting Wazuh and TheHive servers.

## Steps

### 1. Set up and download Windows 11 with Sysmon

#### 1.1. Download Windows 11 installation media
![Ref 1: Download Windows 11 Installation Media](https://i.imgur.com/example1.jpg)  
Downloading the Windows 11 ISO using the official media creation tool.

#### 1.2. Create VM in Oracle Virtual Box and select Windows 11 ISO
![Ref 2: Create VM in Oracle VirtualBox](https://i.imgur.com/example2.jpg)  
Configuring a new virtual machine and selecting the Windows 11 ISO.

#### 1.3. Set up Windows 11
![Ref 3: Set up Windows 11](https://i.imgur.com/example3.jpg)  
Completing the Windows 11 installation process, showing the desktop.

#### 1.4. Download Sysmon version 15.15 and sysmonconfig.xml by Olaf
![Ref 4: Download Sysmon](https://i.imgur.com/example4.jpg)  
Downloading Sysmon and the configuration file from Olaf Hartong's GitHub.

#### 1.5. Open powershell and go to directory of Sysmon
![Ref 5: Open PowerShell for Sysmon](https://i.imgur.com/example5.jpg)  
Navigating to the Sysmon directory in PowerShell.

#### 1.5.1. Install Sysmon
![Ref 6: Install Sysmon](https://i.imgur.com/example6.jpg)  
Executing the Sysmon installation command with the configuration file.

### 2. Set up Cloud Environment for Wazuh and TheHive

#### 2.1. Deploy Wazuh Server with 2vCPUs and 8GB Ram
##### 2.1.1. Setup with Ubuntu v24.04
![Ref 7: Setup Wazuh with Ubuntu](https://i.imgur.com/example7.jpg)  
Setting up the Wazuh server VM with Ubuntu 24.04.

##### 2.1.2. Set up Firewall
![Ref 8: Set up Firewall for Wazuh](https://i.imgur.com/example8.jpg)  
Configuring firewall rules on the Wazuh server.

##### 2.1.3. Update & Upgrade
![Ref 9: Update and Upgrade Wazuh](https://i.imgur.com/example9.jpg)  
Running apt update and upgrade commands.

##### 2.1.4. Install Wazuh 4.12
![Ref 10: Install Wazuh](https://i.imgur.com/example10.jpg)  
Installing Wazuh version 4.12.

#### 2.2. Deploy TheHive VM with 2vCPUs and 8gb Ram
##### 2.2.1. Setup with Ubuntu v24.04
![Ref 11: Setup TheHive with Ubuntu](https://i.imgur.com/example11.jpg)  
Setting up the TheHive VM with Ubuntu 24.04.

##### 2.2.2. Add Firewall
![Ref 12: Add Firewall for TheHive](https://i.imgur.com/example12.jpg)  
Configuring firewall rules on the TheHive server.

##### 2.2.3. Install Dependencies
![Ref 13: Install Dependencies for TheHive](https://i.imgur.com/example13.jpg)  
Running the command to install required packages.

##### 2.2.4. Install Java
![Ref 14: Install Java](https://i.imgur.com/example14.jpg)  
Adding the Java repository and installing Java.

##### 2.2.5. Install Apache Cassandra
![Ref 15: Install Apache Cassandra](https://i.imgur.com/example15.jpg)  
Installing Apache Cassandra.

##### 2.2.6. Install Elastic Search
![Ref 16: Install Elastic Search](https://i.imgur.com/example16.jpg)  
Installing Elasticsearch.

##### 2.2.7. Install TheHive
![Ref 17: Install TheHive](https://i.imgur.com/example17.jpg)  
Installing TheHive packages.

##### 2.2.8. Install packages
![Ref 18: Install Additional Packages for TheHive](https://i.imgur.com/example18.jpg)  
Building dependency trees for TheHive.

### 3. Wazuh and TheHive Configuration

#### 3.1. TheHive
##### 3.1.1. Go to Cassandra
![Ref 19: Go to Cassandra](https://i.imgur.com/example19.jpg)  
Editing cassandra.yaml using nano.

##### 3.1.2. Change Cluster Name from test -> SOCAUTO
![Ref 20: Change Cassandra Cluster Name](https://i.imgur.com/example20.jpg)  
Updating the cluster name to SOCAUTO.

##### 3.1.3. Change listen address to TheHive server IP
from local -> 1**.**.***.**
![Ref 21: Change Listen Address](https://i.imgur.com/example21.jpg)  
Updating the listen address.

##### 3.1.4. Change the rpc_address to TheHive server IP
from local -> 1**.**.***.**
![Ref 22: Change RPC Address](https://i.imgur.com/example22.jpg)  
Updating the RPC address.

##### 3.1.5. Change seed_provider To TheHive server IP
from 1**.*.*.* -> 1**.**.***.**
![Ref 23: Change Seed Provider](https://i.imgur.com/example23.jpg)  
Updating the seed provider.

##### 3.1.6. Stop cassandra, remove file, start cassandra then check status
![Ref 24: Manage Cassandra Service](https://i.imgur.com/example24.jpg)  
Stopping, removing files, starting, and checking Cassandra status.

##### 3.1.7. Configure Elasticsearch
![Ref 25: Configure Elasticsearch](https://i.imgur.com/example25.jpg)  
Editing elasticsearch.yml.

##### 3.1.8. Change cluster.name
![Ref 26: Change Elasticsearch Cluster Name](https://i.imgur.com/example26.jpg)  
Updating the cluster name to SOCAUTO.

##### 3.1.9. Change network host to TheHive server IP
from 1**.**.***.** to 1**.**.***.**
![Ref 27: Change Network Host](https://i.imgur.com/example27.jpg)  
Updating the network host.

##### 3.1.10. Remove node-2 from initial_master_nodes
![Ref 28: Remove Node-2](https://i.imgur.com/example28.jpg)  
Removing node-2 from master nodes.

##### 3.1.11. Start Elasticsearch, enable elastic search and then check the status
![Ref 29: Manage Elasticsearch Service](https://i.imgur.com/example29.jpg)  
Starting, enabling, and checking Elasticsearch status.

##### 3.1.12. Go to TheHive to conf using nano
/etc/thehive/applications.conf
![Ref 30: Configure TheHive](https://i.imgur.com/example30.jpg)  
Editing the TheHive configuration file.

##### 3.1.13. Change the localhost to TheHive server IP
from local_IP to 1**,**.***.**
![Ref 31: Change Localhost](https://i.imgur.com/example31.jpg)  
Updating localhost to the server IP.

##### 3.1.14. Change the Cluster Name to what you want
![Ref 32: Change TheHive Cluster Name](https://i.imgur.com/example32.jpg)  
Setting the desired cluster name.

##### 3.1.15. Change the second local_IP to TheHive server IP
![Ref 33: Change Second Local IP](https://i.imgur.com/example33.jpg)  
Updating the second local IP.

##### 3.1.16. Change application.baseURL to theHive server IP
from local_IP to 1**,**.***.**
![Ref 34: Change Base URL](https://i.imgur.com/example34.jpg)  
Updating the base URL.

##### 3.1.17. Now Start, enable and check the Status of theHive
![Ref 35: Manage TheHive Service](https://i.imgur.com/example35.jpg)  
Starting, enabling, and checking TheHive status.

#### 3.2. Wazuh
##### 3.2.1. Deploy Wazuh agent in the windows 11 VM
![Ref 36: Deploy Wazuh Agent](https://i.imgur.com/example36.jpg)  
Overview of deploying the Wazuh agent.

##### 3.2.2. Set up Wazuh agent using Windows MSI 32/64
![Ref 37: Set up Wazuh Agent](https://i.imgur.com/example37.jpg)  
Selecting the Windows MSI package.

##### 3.2.3. Download and install Wazug agent
![Ref 38: Download and Install Wazuh Agent](https://i.imgur.com/example38.jpg)  
Running the installation in PowerShell.

##### 3.2.4. Start wazuh agent
![Ref 39: Start Wazuh Agent](https://i.imgur.com/example39.jpg)  
Starting the Wazuh service.

##### 3.2.5. Agent status: ACTIVE
![Ref 40: Agent Status Active](https://i.imgur.com/example40.jpg)  
Verifying the Wazuh agent status.

##### 3.2.6. Configure ossec.conf file, replace application with sysmon-operational
![Ref 41: Configure ossec.conf for Sysmon](https://i.imgur.com/example41.jpg)  
Replacing "application" with "sysmon-operational".

##### 3.2.7. Download and run Mimicatz on Windows11 VM
note: Mimikatz is a software that gets passwords
![Ref 42: Download and Run Mimikatz](https://i.imgur.com/example42.jpg)  
Executing Mimikatz to simulate an attack.

##### 3.2.8. Configure ossec.conf file to allow log all
![Ref 43: Configure ossec.conf for Log All](https://i.imgur.com/example43.jpg)  
Enabling log all in ossec.conf.

##### 3.2.9. Configure filebeat.yml under filebeat.modules to be set to true
![Ref 44: Configure filebeat.yml](https://i.imgur.com/example44.jpg)  
Setting Filebeat modules to true.

##### 3.2.10. Create an index for the archive logs
![Ref 45: Create Index Pattern](https://i.imgur.com/example45.jpg)  
Setting up an index pattern for archive logs.

##### 3.2.11. Create rule to detect mimikatz activities
rule: if a filename named mimikatz.exe get detected under the sysmonEvent1 called process creations then trigger this rule
![Ref 46: Create Mimikatz Detection Rule](https://i.imgur.com/example46.jpg)  
Defining the Mimikatz detection rule.

##### 3.2.12. Check to see if logs appear in the Wazuh-alerts
![Ref 47: Check Wazuh Alerts for Mimikatz](https://i.imgur.com/example47.jpg)  
Verifying Mimikatz logs in Wazuh alerts.

### 4. Go to Shuffle.io and create a new workflow

#### 4.1. Configure the ossec.conf file from Wazuh VM
![Ref 48: Configure ossec.conf for Shuffle](https://i.imgur.com/example48.jpg)  
Adding webhook integration to ossec.conf.

#### 4.2. Start the shuffle webhook
![Ref 49: Start Shuffle Webhook](https://i.imgur.com/example49.jpg)  
Configuring and starting the webhook.

#### 4.3. Check alerts for confirmation that it works
![Ref 50: Check Alerts in Shuffle](https://i.imgur.com/example50.jpg)  
Confirming alerts are received in Shuffle.

#### 4.4. Create shuffle tool and Configure
note: What this does is in the field of hashes it will perform the regex then pull whatever data or value it contains
![Ref 51: Create Shuffle Tool for Regex](https://i.imgur.com/example51.jpg)  
Setting up a regex capture group tool.

#### 4.5. Create a Virustotal instance and configure and connect to the regex
![Ref 52: Create VirusTotal Instance](https://i.imgur.com/example52.jpg)  
Configuring a VirusTotal action and connecting it to the regex.

#### 4.6. Check the Explore runs to see if there’s new logs
note: we have successfully logged SHA256 and a virustotal report
![Ref 53: Check Explore Runs in Shuffle](https://i.imgur.com/example53.jpg)  
Verifying new logs including SHA256 hash and VirusTotal report.

### 5. Create an organization in TheHive to use for Shuffle

#### 5.1. Add a normal and service user
##### 5.1.1. Normal User
![Ref 54: Add Normal User in TheHive](https://i.imgur.com/example54.jpg)  
Creating a normal user account.

##### 5.1.2. Service User
![Ref 55: Add Service User in TheHive](https://i.imgur.com/example55.jpg)  
Creating a service user for API authentication.

##### 5.1.3. Add TheHive instance in the workflow
###### 5.1.3.1. Authenticate with service API by the service user
![Ref 56: Authenticate TheHive in Shuffle](https://i.imgur.com/example56.jpg)  
Integrating TheHive with the service API key.

##### 5.1.4. Test out TheHive logs
![Ref 57: Test TheHive Logs](https://i.imgur.com/example57.jpg)  
Executing the workflow to test logging.

##### 5.1.5. Login to TheHive using normal Account
###### 5.1.5.1. Check alerts
![Ref 58: Check Alerts in TheHive](https://i.imgur.com/example58.jpg)  
Accessing TheHive and checking alerts.

###### 5.1.5.2. Create an email instance is Shuffle to alert the Analyst
![Ref 59: Create Email Instance in Shuffle](https://i.imgur.com/example59.jpg)  
Setting up an email action to alert the analyst.

###### 5.1.5.3. Test email in the automation
![Ref 60: Test Email Automation](https://i.imgur.com/example60.jpg)  
Running the workflow to test email notifications.

### 6. Everything works! : Here’s the final Images
![Ref 61: Final Verification Images](https://i.imgur.com/example61.jpg)  
Screenshots confirming the entire automation workflow is functioning successfully.

---

*Note: Replace the example image URLs (e.g., https://i.imgur.com/example1.jpg) with actual Imgur or uploaded image URLs.*
