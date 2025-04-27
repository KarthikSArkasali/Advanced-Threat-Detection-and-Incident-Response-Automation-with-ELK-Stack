# Advanced Threat Detection & Incident Response Automation with ELK Stack

## Objective:  
The objective of this project is to build an end-to-end Security Operations Center (SOC) lab focused on advanced threat detection and incident response automation using the ELK Stack. This includes setting up a centralized logging infrastructure, simulating real-world cyberattacks such as brute-force and command-and-control (C2) attacks using tools like Crowbar and Mythic, detecting them via Elastic Security, and automating alert response through a ticketing system (osTicket). The project aims to enhance skills in log analysis, detection engineering, attack simulation, and response orchestration — empowering analysts to handle threats effectively in a real-world SOC environment.

## 🏗️ Step 1: Centralized Logging Platform  
1. **Architecture Design**  
   - Draw.io logical diagram of VMs, network segments, and ELK components
   
   ![1  Block Diagram](https://github.com/user-attachments/assets/b0f06441-bae9-46f6-8062-9b5cd35325b7)

2. **VM Deployment**  
   | VM            | Role                     | OS          |
   |---------------|--------------------------|-------------|
   | Ubuntu ELK    | Elasticsearch & Kibana   | Ubuntu 22.04|
   | Ubuntu Fleet  | Fleet Server             | Ubuntu 22.04|
   | Ubuntu Agents | Log shippers             | Ubuntu 22.04|
   | Windows 10    | Sysmon + Elastic Agent   | Windows 10  |
   | Windows Server| Domain controller & logs | Windows 2022|
   | Kali Linux    | Attack platform          | Kali Linux  |

![2  Virtual Machines](https://github.com/user-attachments/assets/d4eca1b2-8765-499c-8ae0-68df7cf0c79d)

3. **ELK & Agent Installation**  
   - Installed Elasticsearch & Kibana; accessed via `http://<ELK_IP>:5601`  
   - Deployed Elastic Agent & Sysmon on Windows hosts

![6  Sysmon](https://github.com/user-attachments/assets/b734824a-b654-460d-8ce3-852a0d3a99f3)

![7  Elastic Agent](https://github.com/user-attachments/assets/b24aaaf1-c095-498f-ad8e-c90dde784a83)

   - Configured Fleet Server and ingested Sysmon & Defender logs  

![8  Fleet Server](https://github.com/user-attachments/assets/40c83393-9cce-4620-aeb5-640f996db905)

![10  Ingested Logs](https://github.com/user-attachments/assets/1f5eecd4-6a73-4dcd-9324-45ee49965264)


## 🔐 Step 2: Secure Access & Brute‑Force Detection  
1. **Service Enablement**  
   - RDP on `Win22-Agent`, SSH on `Ubuntu-Agent`  
2. **Attack Simulation**  
   - Ran Crowbar brute‑force against RDP/SSH from Kali

![12  RDP Brute Force](https://github.com/user-attachments/assets/17edb3f7-3568-43fa-8631-c2b6dcf37cbc)
     
3. **Alerting & Dashboards**  
   - Created detection rules for Event IDs (4625, 4624)  
   - Built Kibana dashboards to track success/failure trends

### RDP Dashboard
![16  RDP Dashboard](https://github.com/user-attachments/assets/82b4bdc2-5450-4a33-b250-bb6109ff3dad)

### SSH Dashboard
![15  SSH Dashboard](https://github.com/user-attachments/assets/25e69937-6b72-4283-b368-8f0e4eefb0fa)

## 🕹️ Step 3: Mythic C2 Simulation  
1. **Mythic Deployment**  
   - Installed Mythic C2 on `Ubuntu-Mythic`
     
   ####  ![17  Mythic](https://github.com/user-attachments/assets/51353bad-55a1-4700-bcd3-ba92bf26940c)

3. **Attack Flow Diagram**  
   - Phases: Initial Access → Discovery → Evasion → Execution → C2 → Exfiltration
     
#### 1. Phase-1 Initial Access 

![18  Phase-1](https://github.com/user-attachments/assets/bf52e2eb-aa61-4e5b-aab1-dd4aba04fa9e)

#### 2. Phase-2 Discovery 
![19  Phase-2](https://github.com/user-attachments/assets/c5549404-a559-4871-8fa6-bdb58e05207d)

#### 3. Phase-3 Defender Evasion 
![20  Phase-3](https://github.com/user-attachments/assets/8a206132-aeb6-4187-bd2d-b62070fab68c)

#### 4. Phase-4 Execution 
![21  Phase-4](https://github.com/user-attachments/assets/f6586aba-ec5a-4956-91a7-b85686bfe1d0)

#### 5. Phase-5 Command & Control 
![22  Phase-5](https://github.com/user-attachments/assets/e73efc61-74e1-450d-a07d-6b0584e0540e)

#### 6. Phase-6 Exfiltration 
![23  Phase-6](https://github.com/user-attachments/assets/3e23e166-a942-4d16-97b4-58074e7613e8)

3. **Detection**  
   - Configured alerts & dashboards for each phase

![25  Dashboard Attack](https://github.com/user-attachments/assets/929279ca-ea4d-4bf4-9003-e4526d9fab75)

   - Mapped ATT&CK IDs (T1136.001, T1059.001, etc.)  

![27  Alerts](https://github.com/user-attachments/assets/21aa194e-1f28-4fc3-99f2-6bdacaa79e40)

![27 1 Alerts](https://github.com/user-attachments/assets/93e406a8-fb36-4549-8b18-ad0acd47c13b)

## 🎟️ Step 4: Automated Ticketing & Response  
1. **osTicket Integration**  
   - Deployed osTicket; configured webhook in Kibana

![28  OSTICKET](https://github.com/user-attachments/assets/3214cb6d-0d9b-4e5d-8772-ff4e94ed9edf)

![29  Webhook](https://github.com/user-attachments/assets/63ec32d8-50b5-4906-8bab-fd16e50a728b)

   - Alerts auto-create tickets for triage
     
![OsTicket alert](https://github.com/user-attachments/assets/00127306-f869-4cf2-97f8-99ac4b8ffa40)

2. **Endpoint Defense**  
   - Enabled Elastic Defender; blocked suspicious executables  
   - Automated isolation of compromised hosts

![32  Elastic Endpoint ](https://github.com/user-attachments/assets/452cf769-9659-43a0-9061-5e123c50d728)
   
3. **Incident Workflow**  
   - **Isolate → Investigate → Contain → Remediate → Recover → Document → Learn**

### Alert Triggered 
![31  Malware alert](https://github.com/user-attachments/assets/9d1bfa10-7cc6-4104-a61b-72d4f88461b5)

### Host Isolated
![Screenshot 2024-10-21 105017](https://github.com/user-attachments/assets/9db787e7-8aad-4c23-aeb9-e1b1304b45ca)

### Threat Remediated
![34  Isolated](https://github.com/user-attachments/assets/0ddf3335-4cd7-4147-bac5-57b555ffdd0a)

## 🔑 Key Takeaways  
- **Scalable Logging:** ELK + Elastic Agent for comprehensive telemetry  
- **Real‑Time Detection:** Brute‑force & C2 alerts with custom rules  
- **Automated Response:** Ticketing and endpoint isolation streamline SOC operations  
- **ATT&CK Alignment:** Visibility into attacker techniques across the kill chain  


