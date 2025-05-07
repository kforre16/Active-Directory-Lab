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

## Steps Involved

1. Create a logical Diagram for mapping out lab environment<br><br>
![Copy of ActiveDirectoryProjectDiagram2](https://github.com/user-attachments/assets/810ba3df-60eb-4851-9274-6bfe81e30f8e)
<br>*Ref 1: Logical Diagram*<br><br>
<p>My lab environment includes 2 computers, the blue one represents a terget machine running Windows 10 and the red one representing an attacker machine running on kali linux. My lab also includes 2 servers, one running Windows Server 2022 acting as my domain controller with an Active Directory domain, and the other running Ubuntu Server acting as my Splunk server. Both the Windows 10 target machine and Windows Server will have Sysmon for collecting data on my machines and Splunk Universal Forwarder installed so it can send data to my Splunk Server. Each machine is set up with a static ip address.</p>

3. Set Up Virtual Lab Environment:
<br><br>
![VBoxMachines](https://github.com/user-attachments/assets/ece6e81b-d9c2-4aed-922c-417a253a7ca7)
<p>All 4 virtual machines set up</p>

4. Install and Configure Splunk Enterprise on Ubuntu Server:
<p>I installed Splunk Enterprise 9.4.2 on my Ubuntu server and configured it to run on start up.</p>

5. Install and Configure Splunk Forwarder:
<p>Deployed and configured the Splunk Universal Forwarder on both the Windows 10 target machine and the Windows Server 2022 domain controller to enable log forwarding to Splunk Enterprise.</p>

6. Install and Configure Sysmon:
<p>Installed and configured Sysmon on both the Windows 10 target machine and the Windows Server 2022 domain controller to enhance system-level logging and visibility for security event monitoring.</p>

7. Install and Configure Active Directory on Windows Server 2022:
<p>Installed Active Directory on my server then promoted it to a domain controller. I then proceeded to create 2 Organizational Units, HR and IT, each with 1 user. I was then able to connect my Windows 10 Machine to my new domain.</p>

8. Use Kali Linux to perform a brute force attack:
<p></p>

9. Run Atomic Red Team Tests:
<p>Executed adversary emulation techniques using Atomic Red Team to simulate real-world threats aligned with the MITRE ATT&CK framework.</p>


11. Ingest Attack Telemetry into Splunk:
Ensured that Sysmon and Windows Event logs captured Atomic Red Team activity and were properly ingested into Splunk.

12. Build Detection Rules & Alerts:
Created custom detection logic and alerts in Splunk to flag malicious behaviors and validate detections.

13. Analyze and Tune Detections:
Reviewed alert performance, fine-tuned queries, and validated telemetry against expected results.


