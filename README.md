# Advanced Threat Detection & Incident Response Automation with ELK Stack

**Overview:**  
Automate SOC workflows by deploying a centralized ELK logging platform, detecting brute‑force and C2 attacks, and integrating an alert-driven ticketing system.

## 🏗️ Step 1: Centralized Logging Platform  
1. **Architecture Design**  
   - Draw.io logical diagram of VMs, network segments, and ELK components  
2. **VM Deployment**  
   | VM            | Role                     | OS          |
   |---------------|--------------------------|-------------|
   | Ubuntu ELK    | Elasticsearch & Kibana   | Ubuntu 22.04|
   | Ubuntu Fleet  | Fleet Server             | Ubuntu 22.04|
   | Ubuntu Agents | Log shippers             | Ubuntu 22.04|
   | Windows 10    | Sysmon + Elastic Agent   | Windows 10  |
   | Windows Server| Domain controller & logs | Windows 2022|
   | Kali Linux    | Attack platform          | Kali Linux  |
3. **ELK & Agent Installation**  
   - Installed Elasticsearch & Kibana; accessed via `http://<ELK_IP>:5601`  
   - Deployed Elastic Agent & Sysmon on Windows hosts  
   - Configured Fleet Server and ingested Sysmon & Defender logs  

## 🔐 Step 2: Secure Access & Brute‑Force Detection  
1. **Service Enablement**  
   - RDP on `Win22-Agent`, SSH on `Ubuntu-Agent`  
2. **Attack Simulation**  
   - Ran Crowbar brute‑force against RDP/SSH from Kali  
3. **Alerting & Dashboards**  
   - Created detection rules for Event IDs (4625, 4624)  
   - Built Kibana dashboards to track success/failure trends  

## 🕹️ Step 3: Mythic C2 Simulation  
1. **Mythic Deployment**  
   - Installed Mythic C2 on `Ubuntu-Mythic`  
2. **Attack Flow Diagram**  
   - Phases: Initial Access → Discovery → Evasion → Execution → C2 → Exfiltration  
3. **Detection**  
   - Configured alerts & dashboards for each phase  
   - Mapped ATT&CK IDs (T1136.001, T1059.001, etc.)  

## 🎟️ Step 4: Automated Ticketing & Response  
1. **osTicket Integration**  
   - Deployed osTicket; configured webhook in Kibana  
   - Alerts auto-create tickets for triage  
2. **Endpoint Defense**  
   - Enabled Elastic Defender; blocked suspicious executables  
   - Automated isolation of compromised hosts  
3. **Incident Workflow**  
   - **Isolate → Investigate → Contain → Remediate → Recover → Document → Learn**  

## 🔑 Key Takeaways  
- **Scalable Logging:** ELK + Elastic Agent for comprehensive telemetry  
- **Real‑Time Detection:** Brute‑force & C2 alerts with custom rules  
- **Automated Response:** Ticketing and endpoint isolation streamline SOC operations  
- **ATT&CK Alignment:** Visibility into attacker techniques across the kill chain  


