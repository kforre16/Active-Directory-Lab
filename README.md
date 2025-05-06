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

1. Create a logical Diagram for mapping out lab environment 
![Copy of ActiveDirectoryProjectDiagram2](https://github.com/user-attachments/assets/810ba3df-60eb-4851-9274-6bfe81e30f8e)
*Ref 1: Network Diagram*

2. Set Up Virtual Lab Environment:
Installed and configured VirtualBox to host multiple virtual machines, simulating an enterprise-like network.

3. Deploy Ubuntu/Kali Linux:
Installed Kali Linux for offensive testing.

4. Deploy Ubuntu Server:
Installed and configured Splunk Enterprise to collect, index, and analyze security event data.

5. Deploy Windows Server 2022:
Installed Windows Server and configured it as a Domain Controller to establish an Active Directory domain.

6. Configure Active Directory:
Created users, groups, and organizational units (OUs); implemented group policies to simulate a realistic domain environment.

7. Install and Configure Splunk Forwarder:
Deployed and configured the Splunk Universal Forwarder on both the Windows 10 target machine and the Windows Server 2022 domain controller to enable log forwarding to Splunk Enterprise. 

8. Install and Configure Sysmon:
Installed and configured Sysmon on both the Windows 10 target machine and the Windows Server 2022 domain controller to enhance system-level logging and visibility for security event monitoring.

9. Run Atomic Red Team Tests:
Executed adversary emulation techniques using Atomic Red Team to simulate real-world threats aligned with the MITRE ATT&CK framework.

10. Ingest Attack Telemetry into Splunk:
Ensured that Sysmon and Windows Event logs captured Atomic Red Team activity and were properly ingested into Splunk.

11. Build Detection Rules & Alerts:
Created custom detection logic and alerts in Splunk to flag malicious behaviors and validate detections.

12. Analyze and Tune Detections:
Reviewed alert performance, fine-tuned queries, and validated telemetry against expected results.


