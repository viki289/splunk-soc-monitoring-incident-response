# Splunk SOC Monitoring, Detection & Incident Response

## 📌 Project Overview

This project demonstrates a practical Security Operations Center (SOC)
environment built using Splunk in an isolated lab.

The lab includes Windows 10 and Ubuntu 24.04 endpoints sending security
and system logs to a centralized Splunk server for monitoring, detection,
investigation, and incident response.

---

## 🏗️ Architecture

```text
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
```

Logs are forwarded to Splunk over TCP port `9997`.

---

## 🛠️ Technologies & Tools

- Splunk Enterprise
- Splunk Universal Forwarder
- Windows 10
- Ubuntu 24.04
- SPL (Search Processing Language)
- MITRE ATT&CK
- Windows Event Logs
- Linux Authentication Logs
- ClamAV
- PowerShell

---

## 🔍 Security Scenarios

The project covers controlled cybersecurity lab simulations:

| Scenario | Security Activity |
|---|---|
| P-1 | Authentication Brute-Force |
| P-2 | Phishing URL Simulation |
| P-3 | EICAR Test Artifact Detection |
| P-4 | Suspicious Process Execution |
| P-5 | PowerShell Execution Policy Bypass |
| P-6 | Scheduled Task / Cron Persistence |
| P-7 | Sudo Privilege-Related Activity |
| P-8 | Rapid File-Change Activity |
| P-9 | IOC Threat Hunting |
| P-10 | Cross-Scenario Investigation |

---

## 🚨 Detection & Monitoring

The Splunk environment contains detection rules and alerts covering:

- Failed authentication attempts
- Phishing simulation indicators
- EICAR test artifact detection
- Process creation
- PowerShell activity
- Scheduled-task and cron persistence
- Sudo activity
- Rapid file-change activity
- IOC investigation
- Cross-scenario correlation

---

## 🔎 Investigation Process

```text
Alert Generation
       ↓
Log Analysis
       ↓
SPL Investigation
       ↓
Timeline Reconstruction
       ↓
IOC Investigation
       ↓
MITRE ATT&CK Mapping
       ↓
Severity Assessment
       ↓
Containment
       ↓
Eradication
       ↓
Recovery
       ↓
Lessons Learned
```

---

## 📊 Key Outcomes

- Centralized Windows and Linux log collection
- Splunk-based SOC monitoring
- Real-time detection alerts
- SPL-based security investigation
- Detection engineering
- IOC threat hunting
- Incident response documentation
- MITRE ATT&CK mapping
- Security-event timeline analysis

---

## 📂 Repository Structure

```text
splunk-soc-monitoring-incident-response/
│
├── detection-rules/
│   ├── P1-failed-login.md
│   ├── P2-phishing-detection.md
│   ├── P3-eicar-detection.md
│   ├── P4-suspicious-process.md
│   ├── P5-powershell-detection.md
│   ├── P6-persistence-detection.md
│   ├── P7-privilege-escalation.md
│   └── P8-file-change-detection.md
│
├── evidence/
│   ├── P1-authentication/
│   ├── P2-phishing/
│   ├── P3-eicar/
│   ├── P4-suspicious-process/
│   ├── P5-powershell/
│   ├── P6-persistence/
│   ├── P7-privilege-escalation/
│   └── P8-file-change/
│
├── screenshots/
│   ├── P1/
│   ├── P2/
│   ├── P3/
│   ├── P4/
│   ├── P5/
│   ├── P6/
│   ├── P7/
│   └── P8/
│
├── spl-queries/
│   └── detection-queries.md
│
└── README.md
```

---

## 📖 Documentation

Detailed detection logic, SPL queries, investigation evidence,
screenshots, and scenario documentation are available in the repository.

### Detection Rules

The `detection-rules` directory contains the documented detection logic
for scenarios P-1 through P-8.

### SPL Queries

The `spl-queries` directory contains the SPL searches used for detection,
investigation, and threat hunting.

### Evidence

The `evidence` directory contains scenario-specific investigation
documentation.

### Screenshots

The `screenshots` directory contains visual evidence collected from the
SOC lab.

---

## ⚠️ Lab Disclaimer

All activities were performed in an isolated and authorized lab
environment for cybersecurity training and detection engineering.

The scenarios were controlled simulations and should not be interpreted
as real-world attacks or compromises.

No production systems or external targets were involved.

---

## 👨‍💻 Author

**Vivek Maurya**
