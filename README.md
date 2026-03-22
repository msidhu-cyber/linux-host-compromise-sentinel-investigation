# Linux Host Compromise Investigation – Microsoft Sentinel

## 🎯 Lab Objective

This project simulates a realistic post-compromise investigation scenario involving a cloud-hosted Linux virtual machine monitored using Microsoft Sentinel.

The objective was to replicate attacker behaviour following successful remote access, design behavioural detection logic, and conduct a structured SOC investigation aligned with real-world incident response workflows.

---

## 🧪 Simulated Attack Scenario

A threat actor gained initial access to a Linux host through successful SSH authentication from an external IP address.

Following authentication, several post-compromise behaviours were simulated to mirror real adversary tradecraft:

- Privilege enumeration and escalation attempts using **sudo / su**
- Creation of additional service accounts to maintain access
- SSH persistence via modification of **authorized_keys**
- Scheduled task (cron) abuse to enable covert execution
- Access attempts to sensitive credential storage (**/etc/shadow**)
- Repeated remote session establishment indicating sustained access

These activities were intentionally generated to emulate realistic host compromise patterns observed in enterprise environments.

---

## 🛰️ Detection Engineering Approach

Custom KQL hunting queries were developed in Microsoft Sentinel to perform **behavioural correlation** across multiple Linux Syslog signals.

The detection strategy focused on identifying suspicious activity sequences rather than relying on isolated alert triggers.

Key detection logic included correlation of:

- Successful SSH authentication events
- Subsequent privilege escalation activity
- Account manipulation or service account creation
- Persistence indicators such as cron execution or SSH key modification
- Interaction with sensitive system files

This behavioural detection methodology improves alert fidelity by highlighting attacker intent and progression.

---

## 🔎 Investigation Methodology

A structured SOC investigation workflow was followed to validate potential compromise:

1. Validate authentication source IP reputation and session patterns  
2. Expand investigation timeline to identify post-login activity  
3. Analyse privilege escalation behaviour and command execution  
4. Identify persistence mechanisms including cron jobs and SSH key changes  
5. Review access to sensitive credential storage locations  
6. Assess activity consistency with expected administrative behaviour  

This investigative approach aligns with real SOC triage practices for suspected host compromise scenarios.

---

## 🛡️ Incident Response Actions

Following confirmation of suspicious behaviour, containment actions were simulated:

- Removal of unauthorized SSH persistence keys  
- Locking of suspicious or potentially compromised service accounts  
- Verification and removal of scheduled persistence tasks  
- Review of authentication telemetry for additional compromise indicators  
- Restoration of secure remote access configuration  
- Shutdown of the virtual machine to simulate host isolation  

These steps demonstrate practical incident response procedures used in enterprise security operations.

---

## 📊 Skills Demonstrated

- Microsoft Sentinel threat hunting  
- KQL detection engineering  
- Linux host security log analysis  
- Privilege escalation investigation  
- Persistence technique identification  
- Behaviour-based detection strategy  
- SOC incident triage and response workflow  

---

## 🧠 Key Learning Outcomes

This lab reinforced several critical SOC analyst competencies:

- Attackers rarely stop at initial access — behavioural analysis is essential  
- Expanding investigation timelines helps uncover full compromise scope  
- Persistence mechanisms can be subtle but high-impact indicators  
- Effective detection requires correlation across multiple telemetry sources  
- Proper containment and environment hardening are key phases of response  

---

## 🔗 Tools & Technologies

- Microsoft Sentinel  
- Azure Linux Virtual Machine  
- Syslog ingestion via Azure Monitor Agent (AMA)  
- Kusto Query Language (KQL)  
- SSH authentication telemetry  

---

## 📌 MITRE ATT&CK Techniques Observed

- **T1078 — Valid Accounts**  
- **T1548 — Abuse Elevation Control Mechanism**  
- **T1098 — Account Manipulation**  
- **T1053 — Scheduled Task / Cron**  
- **T1003 — OS Credential Dumping**  
- **T1087 — Account Discovery**

---

## 📈 Detection Improvement Opportunities

Future detection engineering enhancements could include:

- Correlation of failed authentication bursts prior to successful login  
- Geo-anomaly detection for external SSH authentication sources  
- Behaviour baselining for privileged command execution  
- Integration with endpoint telemetry for deeper host visibility  
- Automated incident enrichment using Sentinel playbooks  

This reflects continuous detection improvement practices used in mature SOC environments.

---

## 🧩 SOC Analyst Reflection

This investigation highlighted the importance of analysing attacker behaviour progression rather than focusing solely on initial alerts.

The exercise strengthened practical skills in behavioural threat hunting, log correlation, and structured incident containment — core competencies required for modern SOC analysts.
