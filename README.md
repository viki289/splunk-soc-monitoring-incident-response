# Splunk SOC Monitoring, Detection & Incident Response

## 📌 Project Overview

This project demonstrates a practical Security Operations Center (SOC)
environment built using Splunk in an isolated lab.

The lab includes Windows 10 and Ubuntu 24.04 endpoints sending security
and system logs to a centralized Splunk server for monitoring, detection,
investigation, and incident response.

## 🏗️ Architecture

Windows 10 Endpoint
        │
        ├── Splunk Universal Forwarder
        │
        ▼
     Splunk Server
        ▲
        │
Ubuntu 24.04 Endpoint
        │
        └── Splunk Universal Forwarder

Logs are forwarded to Splunk over TCP port 9997.

## 🛠️ Technologies & Tools

- Splunk Enterprise
- Splunk Universal Forwarder
- Windows 10
- Ubuntu 24.04
- SPL (Search Processing Language)
- MITRE ATT&CK
- Windows Event Logs
- Linux Authentication Logs

## 🔍 Security Scenarios

The project covers controlled lab simulations including:

- Authentication brute-force
- Phishing URL simulation
- EICAR malware testing
- Suspicious process execution
- PowerShell activity
- Scheduled task / cron persistence
- Sudo privilege escalation
- Ransomware-like file activity
- IOC threat hunting
- Cross-scenario investigation

## 🚨 Detection & Monitoring

The Splunk environment contains real-time detection rules and alerts
covering authentication, phishing, malware, process activity,
PowerShell, persistence, privilege escalation, and suspicious
file-change behavior.

## 🔎 Investigation Process

1. Alert generation
2. Log analysis
3. SPL-based investigation
4. Timeline reconstruction
5. IOC investigation
6. MITRE ATT&CK mapping
7. Severity assessment
8. Containment
9. Eradication
10. Recovery
11. Lessons learned

## 📊 Key Outcomes

- Centralized Windows and Linux log collection
- SOC monitoring dashboard
- Real-time detection alerts
- SPL-based investigation
- Incident response documentation
- Threat hunting and IOC analysis
- MITRE ATT&CK mapping

## ⚠️ Lab Disclaimer

All activities were performed in an isolated and authorized lab
environment for cybersecurity training and detection engineering.

No production systems, external targets, or real threat actors were
involved.

## 📚 Documentation

Detailed investigation findings, evidence, screenshots, detection
logic, and incident response documentation will be provided in this
repository.

## 👨‍💻 Author

Vivek Maurya
