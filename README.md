# Advanced Threat Detection & Incident Response Automation with ELK Stack

## Objective:  
The objective of this project is to build an end-to-end Security Operations Center (SOC) lab focused on advanced threat detection and incident response automation using the ELK Stack. This includes setting up a centralized logging infrastructure, simulating real-world cyberattacks such as brute-force and command-and-control (C2) attacks using tools like Crowbar and Mythic, detecting them via Elastic Security, and automating alert response through a ticketing system (osTicket). The project aims to enhance skills in log analysis, detection engineering, attack simulation, and response orchestration — empowering analysts to handle threats effectively in a real-world SOC environment.

## 🏗️ Step 1: Centralized Logging Platform  
1. **Architecture Design**  
   - Draw.io logical diagram of VMs, network segments, and ELK components
   
   ![1  Block Diagram](https://github.com/user-attachments/assets/c234a80b-6c80-4301-91ab-d6bb0d9d488e)

2. **VM Deployment**  
   | VM            | Role                     | OS          |
   |---------------|--------------------------|-------------|
   | Ubuntu ELK    | Elasticsearch & Kibana   | Ubuntu 22.04|
   | Ubuntu Fleet  | Fleet Server             | Ubuntu 22.04|
   | Ubuntu Agents | Log shippers             | Ubuntu 22.04|
   | Windows 10    | Sysmon + Elastic Agent   | Windows 10  |
   | Windows Server| Domain controller & logs | Windows 2022|
   | Kali Linux    | Attack platform          | Kali Linux  |

![2  Virtual Machines](https://github.com/user-attachments/assets/8c090246-0600-473a-8efb-009273510a01)

3. **ELK & Agent Installation**  
   - Installed Elasticsearch & Kibana; accessed via `http://<ELK_IP>:5601`  
   - Deployed Elastic Agent & Sysmon on Windows hosts  
   - Configured Fleet Server and ingested Sysmon & Defender logs  

![10  Ingested Logs](https://github.com/user-attachments/assets/a563eb8f-0c7c-43c8-b8b3-9781d982a299)

## 🔐 Step 2: Secure Access & Brute‑Force Detection  
1. **Service Enablement**  
   - RDP on `Win22-Agent`, SSH on `Ubuntu-Agent`  
2. **Attack Simulation**  
   - Ran Crowbar brute‑force against RDP/SSH from Kali  
3. **Alerting & Dashboards**  
   - Created detection rules for Event IDs (4625, 4624)  
   - Built Kibana dashboards to track success/failure trends

### RDP Dashboard
![16  RDP Dashboard](https://github.com/user-attachments/assets/2bbc7dc3-f8da-4cf0-bab8-7d0bf5aff69d)

### SSH Dashboard
![15  SSH Dashboard](https://github.com/user-attachments/assets/1d0a0577-10eb-4d41-baee-6df682a75072)

## 🕹️ Step 3: Mythic C2 Simulation  
1. **Mythic Deployment**  
   - Installed Mythic C2 on `Ubuntu-Mythic`
     
   ####  ![17  Mythic](https://github.com/user-attachments/assets/1b0d57a5-e0fd-4860-99bb-167cab16352e)

3. **Attack Flow Diagram**  
   - Phases: Initial Access → Discovery → Evasion → Execution → C2 → Exfiltration
     
#### 1. Phase-1 Initial Access 

![18  Phase-1](https://github.com/user-attachments/assets/a790166e-d896-463b-ada3-4a3c143fa602)

#### 2. Phase-2 Discovery 
![19  Phase-2](https://github.com/user-attachments/assets/ad96189d-4d33-41be-bb35-35f15ca1e1b5)

#### 3. Phase-3 Defender Evasion 
![20  Phase-3](https://github.com/user-attachments/assets/6c5918e8-c2f2-438d-b82a-3ed852bdd180)

#### 4. Phase-4 Execution 
![21  Phase-4](https://github.com/user-attachments/assets/f515c3dc-e571-4360-9988-7c575b6d576f)

#### 5. Phase-5 Command & Control 
![22  Phase-5](https://github.com/user-attachments/assets/9cfca8fb-5b76-47ec-b98c-a35a647675d4)

#### 6. Phase-6 Exfiltration 
![23  Phase-6](https://github.com/user-attachments/assets/40bcece7-eeae-4a33-bac1-645696b86470)

3. **Detection**  
   - Configured alerts & dashboards for each phase  
   - Mapped ATT&CK IDs (T1136.001, T1059.001, etc.)  

![27  Alerts](https://github.com/user-attachments/assets/021084cc-0dd3-4b94-baa0-59bcedc82fc5)

![27 1 Alerts](https://github.com/user-attachments/assets/4a271cc6-8983-4024-b81b-5d243e2156ae)

## 🎟️ Step 4: Automated Ticketing & Response  
1. **osTicket Integration**  
   - Deployed osTicket; configured webhook in Kibana  
   - Alerts auto-create tickets for triage
     
![OsTicket alert](https://github.com/user-attachments/assets/6eadb12f-6c2b-4cc0-8de1-3353048a36db)

2. **Endpoint Defense**  
   - Enabled Elastic Defender; blocked suspicious executables  
   - Automated isolation of compromised hosts

![32  Elastic Endpoint ](https://github.com/user-attachments/assets/5cc3cf37-df3b-421b-8ae6-e45b747ff249)
   
3. **Incident Workflow**  
   - **Isolate → Investigate → Contain → Remediate → Recover → Document → Learn**

### Alert Triggered 
![31  Malware alert](https://github.com/user-attachments/assets/ce0c9f6f-390b-4458-b825-801c373e0128)

### Host Isolated
![Screenshot 2024-10-21 105017](https://github.com/user-attachments/assets/47b2119f-88ff-4e96-b846-8d74b2855e88)

### Threat Remediated
![34  Isolated](https://github.com/user-attachments/assets/4d658dcd-25fa-4124-a439-df745fc94ab5)

## 🔑 Key Takeaways  
- **Scalable Logging:** ELK + Elastic Agent for comprehensive telemetry  
- **Real‑Time Detection:** Brute‑force & C2 alerts with custom rules  
- **Automated Response:** Ticketing and endpoint isolation streamline SOC operations  
- **ATT&CK Alignment:** Visibility into attacker techniques across the kill chain  


