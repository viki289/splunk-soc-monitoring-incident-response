# P-4 — Suspicious Process Detection

## Overview

This detection identifies a controlled process-execution event in which PowerShell launches `notepad.exe`.

The activity was intentionally generated in the authorized SOC lab to verify that Windows process-creation telemetry can be collected by Splunk and used for security monitoring.

---

## Detection Objective

Detect the execution of `notepad.exe` when the creator process is PowerShell.

The detection uses Windows Security Event ID `4688`, which records process creation activity.

---

## SPL Detection Query

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4688 "notepad.exe"
```

---

## How the Detection Works

The SPL query searches the `wineventlogs` index for Windows Security events with:

- `EventCode=4688` — Process creation
- `notepad.exe` — Target process
- `WinEventLog:Security` — Windows Security event sourcetype

The query helps identify process execution activity that requires further analyst review.

---

## Lab Activity

During the controlled P-4 scenario, PowerShell was used to launch `notepad.exe`.

The Windows event recorded the process creation activity and provided process-related information for investigation.

The observed activity included:

- Target process: `notepad.exe`
- Creator process: PowerShell
- Account: `vboxuser`
- Event ID: `4688`

---

## Detection Result

The Splunk search successfully identified the controlled process-creation event.

The corresponding P-4 alert was triggered during the lab exercise, demonstrating that the configured detection rule could identify the simulated activity.

---

## Investigation

The analyst can review the Event ID 4688 fields to determine:

1. Which process was executed
2. Which process created it
3. Which user account initiated the activity
4. The execution time
5. The affected host

This information can be used to determine whether the process execution is expected or requires additional investigation.

---

## SOC Workflow

```text
PowerShell Execution
        ↓
notepad.exe Created
        ↓
Windows Event ID 4688
        ↓
Universal Forwarder
        ↓
Splunk
        ↓
SPL Detection
        ↓
P-4 Alert
        ↓
Analyst Investigation
```

---

## Security Significance

Process creation telemetry is useful for identifying potentially suspicious execution behavior.

PowerShell is a legitimate Windows administration tool, but its execution can also appear in attack activity. Therefore, PowerShell-created processes should be investigated in context rather than treated as malicious by default.

---

## Lab Classification

**Scenario:** P-4 — Suspicious Process Detection  
**Environment:** Isolated SOC Lab  
**Activity Type:** Controlled Simulation  
**Result:** Detection successfully demonstrated

> This event was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
