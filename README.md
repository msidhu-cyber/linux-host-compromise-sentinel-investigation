# Linux Host Compromise Investigation – Microsoft Sentinel

## 🎯 Lab Objective

This project simulates a realistic post-compromise investigation scenario involving a cloud-hosted Linux virtual machine.

The lab focuses on identifying attacker behaviour following successful SSH authentication, including privilege escalation, persistence mechanisms, and sensitive system interaction.

The goal was to design detection logic, perform threat hunting, and execute structured SOC investigation workflows using Microsoft Sentinel.

---

## 🧪 Simulated Attack Scenario

A threat actor gained access to a Linux host through successful SSH authentication from an external IP address.

Following initial access, the attacker performed several actions commonly observed in real-world compromises:

- Privilege enumeration and escalation attempts (sudo / su usage)
- Creation of additional service accounts for persistence
- SSH persistence via authorised_keys modification
- Scheduled task (cron) abuse for covert execution
- Access to sensitive credential storage (/etc/shadow)
- Repeated remote session establishment indicating sustained access

These behaviours were intentionally generated to replicate attacker tradecraft aligned with MITRE ATT&CK techniques.

---

## 🛰️ Detection Engineering Approach

Custom KQL hunting queries were developed within Microsoft Sentinel to correlate:

- Successful SSH authentication events  
- Subsequent privilege-related system logs  
- Persistence indicators  
- Cron-based execution patterns  

Behavioural correlation logic enabled detection of:

- Suspicious login followed by privilege escalation  
- Account creation activity shortly after authentication  
- Indicators of long-term access persistence  
- Sensitive file access attempts  

This demonstrates the importance of contextual detection rather than reliance on single alert triggers.

---

## 🔎 Investigation Methodology

The investigation process followed a structured SOC workflow:

1. Validate authentication source and session patterns  
2. Expand timeline to identify post-login behaviour  
3. Analyse privilege usage and command execution  
4. Identify persistence techniques and lateral movement risk  
5. Confirm sensitive system interaction  
6. Contain simulated threat and restore system security posture  

---

## 🛡️ Response Actions

- Removal of malicious SSH authorised keys  
- Locking of compromised or suspicious accounts  
- Verification of cron persistence removal  
- Validation of system authentication logs  
- Restoration of secure access configuration  
- Shutdown of lab VM following investigation completion  

---

## 📊 Skills Demonstrated

- Microsoft Sentinel threat hunting  
- KQL detection engineering  
- Linux security event analysis  
- Privilege escalation investigation  
- Persistence technique identification  
- Incident triage and response workflow  
- Behaviour-based detection strategy  

---

## 🧠 Key Learning Outcomes

This lab reinforced critical SOC analyst competencies:

- Attackers rarely stop at initial access — behavioural analysis is essential  
- Timeline expansion is vital for uncovering true compromise scope  
- Persistence indicators can be subtle but high-impact  
- Effective detection requires correlation across multiple log signals  
- Proper containment and environment hardening is a key investigation phase  

---

## 🔗 Tools & Technologies

- Microsoft Sentinel  
- Azure Linux Virtual Machine  
- Syslog via AMA  
- KQL (Kusto Query Language)  
- SSH authentication telemetry  

---

## 📌 MITRE ATT&CK Techniques Observed

- T1078 – Valid Accounts  
- T1059 – Command Execution  
- T1098 – Account Manipulation  
- T1053 – Scheduled Task / Cron  
- T1003 – Credential Access  

---



---

## Detection Engineering Approach

During the investigation, custom behavioural hunting logic was developed to identify 
potential host compromise following successful SSH authentication.

KQL queries were designed to correlate multiple security signals including:

• Successful remote authentication events  
• Privilege escalation behaviour (sudo / su activity)  
• Creation of new service or persistence accounts  
• SSH key modification indicating backdoor access  
• Scheduled task (cron) abuse for covert execution  
• Access attempts to sensitive credential storage  

This correlation-based detection strategy improves alert fidelity by focusing on 
attacker behaviour patterns rather than isolated security events.
