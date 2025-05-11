# Active-Directory Lab

## Objective


The Active-Directory Lab project is aimed to deepen my expertise in cybersecurity and system administration by building a secure home lab that integrates Splunk for SIEM, Kali Linux for offensive security testing, and Atomic Red Team for simulating real-world attacks—enabling hands-on experience with domain environments, event telemetry, and threat detection.

### Skills Learned

- Active Directory Administration: Set up and managed a secure domain environment, including user/group management and domain controller configuration.

- SIEM Integration: Ingested and analyzed Windows event logs using Splunk to detect suspicious activity.

- Threat Simulation: Deployed Atomic Red Team to emulate real-world attack techniques and test detection capabilities.

- Offensive Security Testing: Utilized Kali Linux to simulate adversarial behavior and validate detection logic.

- Telemetry Generation: Produced meaningful security telemetry through attack simulations for use in detection engineering.

- Log Analysis & Correlation: Developed an understanding of event flow from endpoint to SIEM, improving log parsing and correlation strategies.

- Security Monitoring: Built alert logic based on attack techniques mapped to MITRE ATT&CK.

- Lab Infrastructure Setup: Created a self-contained home lab using virtualization to simulate enterprise environments safely.

### Tools Used

- Windows Server 2022 – for Active Directory domain setup and event generation
- Active Directory – to manage users, groups, policies, and domain services
- Splunk – for ingesting, analyzing, and alerting on security telemetry (SIEM)
- Kali Linux – for conducting offensive security tests and simulating attacker behavior
- Atomic Red Team – to emulate real-world attack techniques and generate detection-relevant telemetry
- Sysmon – for enhanced system-level logging and detailed event collection
- PowerShell – for invoking Atomic Red Team tests
- VirtualBox – for building and isolating the lab environment in a virtualized setting
- Ubuntu Server – for setting up a Splunk server for log ingestion from Windows environments 

## Part 1: Create a logical Diagram for mapping out lab environment

![Copy of ActiveDirectoryProjectDiagram2](https://github.com/user-attachments/assets/810ba3df-60eb-4851-9274-6bfe81e30f8e)
<br>
My lab environment consists of two computers: a blue machine serving as the target system running Windows 10, and a red machine functioning as the attacker system running Kali Linux. Additionally, there are two servers: one running Windows Server 2022 configured as a domain controller with Active Directory, and another running Ubuntu Server hosting my Splunk instance. Both the Windows 10 target and the Windows Server have Sysmon installed for data collection, along with the Splunk Universal Forwarder to transmit logs to the Splunk server. All machines are configured with static IP addresses.

## Part 2: Install Virtual Machines on VirtualBox

![VBoxMachines](https://github.com/user-attachments/assets/ece6e81b-d9c2-4aed-922c-417a253a7ca7)
<br>
- Windows 10
- Kali Linux
- Ubuntu Server
- Windows Server 2022
<p>I configured the network settings to use a NAT Network, allowing all machines to operate on the same virtual network.</p>

## Part 3: Install and configure Splunk Enterprise on Ubuntu Server/Install and configure Sysmon and Splunk Forwader on Windows 10 Target Machine and Windows Server

<p>"I downloaded and installed Splunk Enterprise v9.4.2 on my Ubuntu Server, configuring it to start automatically on boot.</p>

![image](https://github.com/user-attachments/assets/0aa42e14-0a52-4e6d-a246-22a990ec5ad1)

<p>I installed and configured Sysmon on both the Windows 10 target machine and the Windows Server to improve system-level logging and enhance visibility for security event monitoring.</p>

<p>I also installed the Splunk Universal Forwarder on both the Windows 10 target machine and the Windows Server to transmit log data to the Splunk server.</p>

## Part 4: Install and configure Active Directory on Windows Server and Promote it to a Domain Controller

<p>Installed and configured Active Directory on the Windows Server, then promoted the server to a domain controller.</p>

![image](https://github.com/user-attachments/assets/fa2d9a3c-fc41-4c10-9b2c-209b24ab4eed)

<p>I then created two Organizational Units, HR and IT, each containing a single user account.</p>

![image](https://github.com/user-attachments/assets/5c928b1f-370f-47e3-91da-7492bb6f223d)

![image](https://github.com/user-attachments/assets/12b512dd-664f-451d-91c7-c4a20fe07f11)

![image](https://github.com/user-attachments/assets/ade56b50-e550-411e-a08a-b5a5a50193e7)

Join Target Windows PC to new Domain:
<br>
<p>I successfully joined the Windows 10 machine to the newly created domain.</p>

![image](https://github.com/user-attachments/assets/d3433c29-348f-4bdc-a46e-54cc4ad359e5)

<p>I also enabled Remote Desktop Protocol (RDP) to facilitate testing with brute-force tools.</p>

## Part 5: Use Kali Linux to perform a Brute Force Attack on newly created users and view telemetry via Splunk/Setup and Install Atomic Red Team and run Atomic Tests

<p>I installed a Kali Linux tool called Crowbar and used the built-in 'rockyou' wordlist, extracting the first 20 entries into a file named passwords.txt. To ensure a successful login for the scenario, I appended the correct password to the end of the file. I then used Crowbar to perform a brute-force attack against the RDP service, targeting the previously created user account tsmith.</p>

![KaliLinuxCrowbar](https://github.com/user-attachments/assets/15e25cc7-19d2-430a-be57-733f22396bb7)

<p>In Splunk I search for events related to the user tsmith:</p>

![image](https://github.com/user-attachments/assets/85ecc4f6-77c0-41ed-ba78-26f57116206a)

<p>The search returned 23 results, 20 of which correspond to EventCode 4625. According to Ultimate Windows Security, this event indicates a failed login attempt, which aligns with the passwords.txt file containing 21 passwords, one of which is correct. The results show these failed login attempts occurring around the same time, suggesting a brute-force attack.</p>

![image](https://github.com/user-attachments/assets/72d10336-e844-4a55-90dd-0a100c49fde8)

<p>There was one successful login attempt, indicated by EventCode 4624, which signifies that an account was successfully logged on.</p>

![image](https://github.com/user-attachments/assets/e4816cd0-1aad-4372-8ee0-6ca8bdfb8e2a)

<p>Expanding the event shows that the source of the login was from my kali linux machine.</p>

![image](https://github.com/user-attachments/assets/64656e27-a424-4cad-84c6-d390a458be0e)

<p>I installed Atomic Red Team on my Windows target machine and used the MITRE ATT&CK framework to explore various attack scenarios for testing. I selected the 'Create Account: Local Account (T1136.01)' technique, which simulates adversaries creating a local account to maintain persistent access to victim systems.</p>

![image](https://github.com/user-attachments/assets/785ca092-e029-4928-b0b8-355304fa6829)

<p>In Splunk, the search results for NewLocalUser shows 12 results.</p>

![image](https://github.com/user-attachments/assets/9ba59b57-7929-4c36-bb86-fb83e4a6267e)

## Part 6: Build Detection Rules & Alerts

<p>Now that I can create telemetry within my lab I can know focus on creating alerts in Splunk to flag malicious behaviors.</p>
<p>I will use the brute force attack scenario I used earlier to test out an alert that detects such an attack.</p>
<p>I used a post from NetwerkLabs on <a href="https://netwerklabs.com/detect-brute-force-attacks-using-splunk/">Detecting brute force attacks using Splunk</a> to build out my alert.</p>
<p>I was able to come up with the following query:</p>

```
index="endpoint" EventCode=4625 | bin _time span=5m | stats count by Account_Name, Source_Network_Address, _time | where count >=10
```
Explanation:
- This query searches for log entries containing the event code 4625 indicating a failed log on attempt.
- bin _time span=5m: Buckets time into 5-minute intervals.
- stats count by Account_Name, Source_Network_Address, _time: Groups attempts by account and Source IP over each 5-minute window.
- where count >= 10: Only keeps records with 10 or more failed login attempts— which could be indicative of a brute force attempt.

Alert Configuration:

![image](https://github.com/user-attachments/assets/88d45153-5503-4094-9921-be3e4dc8ee9e)

After saving the alert, I ran the crowbar command from kali linux again to trigger the alert. 

The triggerd alert in Splunk:

![image](https://github.com/user-attachments/assets/72bc6d23-d36e-4a7e-b5ad-6db9cb741eac)
