# Network-Reconnaissance-Detection-Incident-Response-Lab
SOC project for incident response

## Overview
This project simulates a real-world SOC (Security Operations Center) scenario where a network reconnaissance attack is performed using Nmap from a Kali Linux machine and detected using Windows Firewall logs. The attack is analyzed and mitigated using firewall rules.

The goal is to demonstrate:
- Network reconnaissance detection
- Log analysis using Windows firewall logs
- Incident response workflow (Detect → Analyze → Respond)
- Firewall-based mitigation techniques

---

## Lab Environment

- 🖥️ Attacker: Kali Linux  
- 🖥️ Target: Windows 11  
- 📊 Logging: Windows Firewall Logging  
- 🛠️ Tools Used:
  - Nmap (Network scanning)
  - Windows Firewall
  - PowerShell

---

## Attack Simulation

A network scan was performed from Kali Linux using Nmap:

```bash
nmap -sS -sV -T4 192.168.1.67

or aggressive scan:

nmap -A 192.168.1.67

This simulates a reconnaissance attack where an attacker tries to discover:

Open ports
Running services
System exposure

Tool used: Nmap

## Detection Method

Detection was performed using Windows Firewall logs.

Log Location:
%systemroot%\System32\LogFiles\Firewall\pfirewall.log
Indicators of Reconnaissance:
Multiple connection attempts from same IP
Sequential port scanning behavior
DROP / REJECT entries in logs
High frequency TCP SYN requests
## Incident Analysis

From log analysis, the following were identified:

Attacker IP: 192.168.1.71
Targeted Ports: 21, 22, 80, 135, 445, 3389
Behavior: Network reconnaissance (port scanning)
## Incident Response (Mitigation)

A firewall rule was created to block the attacker:

New-NetFirewallRule -DisplayName "Block Nmap Scanner" `
-Direction Inbound `
-RemoteAddress 192.168.1.71 `
-Action Block

This successfully stopped further scanning activity.

## Optional Analysis Tools

For deeper analysis:

Windows Event Logs
Wireshark packet analysis (Wireshark)
Splunk dashboards (Splunk)
## Key Learning Outcomes
Understanding reconnaissance attacks (network scanning)
Log-based threat detection
SOC incident response workflow
Firewall-based threat mitigation
Basic Blue Team security operations

## Conclusion

This project demonstrates how SOC analysts detect and respond to reconnaissance attacks using log analysis and firewall controls. It simulates a real-world attack scenario and shows the full incident response lifecycle: detection, analysis, and mitigation.
