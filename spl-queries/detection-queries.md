# Splunk Detection & Investigation Queries

This file contains the core SPL searches used during the SOC lab for detection, investigation, and threat hunting.

All searches were executed against the authorized, isolated lab environment.

---

## P-1 — Windows Multiple Failed Login Attempts

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4625
| stats count as failed_attempts min(_time) as first_failure max(_time) as last_failure by host Account_Name
| where failed_attempts>=5
```

**Purpose:** Detect 5 or more failed Windows authentication attempts for an account.

---

## P-1 — Ubuntu Multiple Failed Login Attempts

```spl
index=ubuntu_logs "Failed password"
| stats count as failed_attempts min(_time) as first_failure max(_time) as last_failure by host
| where failed_attempts>=5
```

**Purpose:** Detect repeated SSH authentication failures on Ubuntu.

---

## P-2 — Phishing URL Simulation

### Windows

```spl
index=wineventlogs sourcetype="WinEventLog:Application" "example.com"
```

### Ubuntu

```spl
index=ubuntu_logs "Controlled phishing simulation URL accessed"
```

**Purpose:** Identify controlled phishing-simulation URL activity.

---

## P-3 — EICAR Test Artifact Detection

```spl
index=ubuntu_logs sourcetype="clamav:eicar" "Eicar-Test-Signature"
```

**Purpose:** Detect the EICAR test signature reported by ClamAV.

---

## P-4 — Suspicious Process Simulation

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4688 "notepad.exe"
```

**Purpose:** Investigate the controlled PowerShell-to-Notepad process chain.

---

## P-5 — Suspicious PowerShell Execution

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4688 "P5-Simulation"
```

**Investigation Indicator:**

```text
-ExecutionPolicy Bypass
```

**Purpose:** Identify the controlled PowerShell execution-policy bypass simulation.

---

## P-6 — Windows Scheduled Task Persistence

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4698 "P6-Lab-persistence"
```

**Purpose:** Detect creation of the controlled Windows scheduled task.

---

## P-6 — Ubuntu Cron Persistence

```spl
index=ubuntu_logs "CRON" "cron-Proof.txt"
```

**Purpose:** Detect the controlled cron persistence activity.

---

## P-7 — Ubuntu Privilege Escalation Investigation

```spl
index=ubuntu_logs "sudo" "p7" "/usr/bin/id"
```

**Purpose:** Investigate sudo activity associated with the controlled privilege-related scenario.

---

## P-8 — Abnormal File Change Detection

```spl
index=wineventlogs EventCode=4663
| search Object_Name="*P8-Test*"
| bin _time span=1m
| stats count as file_events dc(Object_Name) as unique_files by _time host Account_Name
| where file_events>=5 AND unique_files>=2
```

**Purpose:** Detect abnormal file activity involving multiple files within a short time window.

---

## P-9 — IOC Hunting

```spl
index=ubuntu_logs "eicar.com" OR "Eicar-Test-Signature" OR "sudo" OR "p7"
```

**Purpose:** Search for relevant indicators and activity during IOC investigation.

---

## P-10 — Cross-Scenario Investigation

```spl
index=wineventlogs OR index=ubuntu_logs
| table _time index host sourcetype EventCode user Account_Name process New_Process_Name Object_Name _raw
```

**Purpose:** Build a common investigation view across Windows and Ubuntu telemetry.

---

# Detection Workflow

```text
Endpoint Activity
        ↓
Log Generation
        ↓
Universal Forwarder
        ↓
Splunk Index
        ↓
SPL Detection Search
        ↓
Alert
        ↓
Analyst Investigation
```

---

# Primary Splunk Indexes

- `wineventlogs` — Windows Security/Application/System events
- `ubuntu_logs` — Ubuntu authentication/syslog data

---

# Lab Disclaimer

All activity represented in these searches was performed in an authorized and isolated cybersecurity lab environment.

The scenarios were controlled simulations for SOC detection, investigation, and incident-response training.

They should not be interpreted as a single real-world attack or compromise.

The queries are provided as documentation of the detection and investigation methods used in the lab.
