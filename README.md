# Active-Directory Lab

## Objective


The Active-Directory Lab project is aimed to To deepen my expertise in cybersecurity and system administration by building a secure home lab that integrates Splunk for SIEM, Kali Linux for offensive security testing, and Atomic Red Team for simulating real-world attacks—enabling hands-on experience with domain environments, event telemetry, and threat detection.

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
- PowerShell – for automation, script-based administration, and data manipulation
- VirtualBox – for building and isolating the lab environment in a virtualized setting
- Ubuntu Server – for setting up a Splunk server for log ingestion from Windows environments 

## Part 1

Create a logical Diagram for mapping out lab environment<br><br>
![Copy of ActiveDirectoryProjectDiagram2](https://github.com/user-attachments/assets/810ba3df-60eb-4851-9274-6bfe81e30f8e)
<br>*Ref 1: Logical Diagram*<br><br>
<p>My lab environment includes 2 computers, the blue one represents a terget machine running Windows 10 and the red one representing an attacker machine running on kali linux. My lab also includes 2 servers, one running Windows Server 2022 acting as my domain controller with an Active Directory domain, and the other running Ubuntu Server acting as my Splunk server. Both the Windows 10 target machine and Windows Server will have Sysmon for collecting data on my machines and Splunk Universal Forwarder installed so it can send data to my Splunk Server. Each machine is set up with a static ip address.</p>

## Part 2

Install Virtual Machines on VirtualBox:
<br><br>
![VBoxMachines](https://github.com/user-attachments/assets/ece6e81b-d9c2-4aed-922c-417a253a7ca7)
<br>*Ref 2: Installed Machines*
<br>
- Windows 10
- Kali Linux
- Ubuntu Server
- Windows Server 2022
<p>I also set my network settings to NAT Network so all my machines run on the same network.</p>

## Part 3

**Install and configure Splunk Enterprise on Ubuntu Server:**
<br>
<p>I downloaded the Splunk Enterprise v9.4.2 and installed it on my Ubuntu Server, configuring it to run Splunk on start up.</p>

![image](https://github.com/user-attachments/assets/0aa42e14-0a52-4e6d-a246-22a990ec5ad1)

**Install and configure Sysmon and Splunk Forwader on Windows 10 Target Machine and Windows Server:**
<br>
<p>I installed and configured Sysmon on both my Windows 10 target machine and Windows Server to enhance system-level logging and visibility for security event monitoring.</p>

<p>I also installed Splunk Forwader on both Windows 10 target machine and Winsows server to send log data to my Splunk server.</p>

## Part 4

Install and configure Active Directory on Windows Server and Promote it to a Domain Controller:
<br>
<p>Installed and configured Active Directory on my Windows server then promoted it to a domain controller.</p>

![image](https://github.com/user-attachments/assets/fa2d9a3c-fc41-4c10-9b2c-209b24ab4eed)

<p>I then proceeded to create 2 Organizational Units, HR and IT, each with 1 user.</p>

![image](https://github.com/user-attachments/assets/5c928b1f-370f-47e3-91da-7492bb6f223d)

![image](https://github.com/user-attachments/assets/12b512dd-664f-451d-91c7-c4a20fe07f11)

![image](https://github.com/user-attachments/assets/ade56b50-e550-411e-a08a-b5a5a50193e7)

Join Target Windows PC to new Domain:
<br>
<p>I was able to connect my Windows 10 Machine to my new domain.</p>

![image](https://github.com/user-attachments/assets/d3433c29-348f-4bdc-a46e-54cc4ad359e5)

<p>I also enabled rdp for the brute force tool usage.</p>

## Part 5

Use Kali Linux to perform a Brute Force Attack on newly created users and view telemetry via Splunk:
<br>
<p>I installed a kali linux tool called Crowbar. I used a kali linux wordlist called rockyou and transfered the first 20 lines to a passwords.txt file. For the scenario I want to create I have added the correct password at the end of the document to create a successful login. I used the command to utile the the rdp service and will be brute forcing the account tsmith I created earlier.</p>

![KaliLinuxCrowbar](https://github.com/user-attachments/assets/15e25cc7-19d2-430a-be57-733f22396bb7)

<p>In Splunk I search for events related to the user tsmith and find the following results.</p>
<p></p>

Setup and Install Atomic Red Team and run Atomic Tests:
<br>
<p>Installed Atomic Red Team on my Windows target machine. Used MITRE Attack to lookup different scenarios to test on my system. I chose the Create Account: Local Account (T1136.01) which Adversaries may create a local account to maintain access to victim systems.</p>
<p>The second test I chose was the Command and Scripting Interpreter: PowerShell (T1059.01) which Adversaries may abuse PowerShell commands and scripts for execution.</p>

## Part 6

Build Detection Rules & Alerts:
Created custom detection logic and alerts in Splunk to flag malicious behaviors and validate detections.
