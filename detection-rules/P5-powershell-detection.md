# P-5 — PowerShell Execution Policy Bypass Detection

## Overview

This detection identifies a controlled PowerShell execution-policy bypass activity in the authorized SOC lab.

The scenario was designed to verify whether Windows process-creation telemetry could capture PowerShell activity containing the `-ExecutionPolicy Bypass` parameter and whether the event could be searched in Splunk.

---

## Detection Objective

Detect PowerShell process execution associated with the P-5 simulation and identify the use of the `-ExecutionPolicy Bypass` parameter.

The detection uses Windows Security Event ID `4688`, which records process creation activity.

---

## SPL Detection Query

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4688 "P5-Simulation"
```

---

## Investigation Indicator

The analyst should inspect the process command-line information for:

```text
-ExecutionPolicy Bypass
```

The presence of this parameter is an investigation indicator because it changes the PowerShell execution-policy behavior for the launched process.

---

## How the Detection Works

The SPL query searches the Windows Security logs for:

- `index=wineventlogs` — Windows event data
- `sourcetype="WinEventLog:Security"` — Windows Security logs
- `EventCode=4688` — Process creation event
- `"P5-Simulation"` — Identifier associated with the controlled lab activity

After finding the event, the analyst reviews the available process and command-line fields.

---

## Lab Activity

During the controlled P-5 scenario, PowerShell execution-policy bypass activity was intentionally generated in the isolated SOC lab.

The investigation was based on Windows Event ID `4688` process-creation telemetry.

The report notes that PowerShell Script Block Logging Event ID `4104` and Sysmon telemetry were available locally but were not successfully forwarded to Splunk.

Therefore, the P-5 investigation in Splunk was limited to the available Event ID `4688` command-line evidence.

---

## Detection Result

The P-5 activity was identified using Windows process-creation telemetry.

The relevant Event ID `4688` event could be searched in Splunk using the detection query above.

---

## Investigation Steps

The analyst should review:

1. Event timestamp
2. Hostname
3. User account
4. New process name
5. Creator process name
6. Command-line information
7. Execution-policy parameters

The analyst should then determine whether the activity was expected administrative behavior or requires additional investigation.

---

## SOC Workflow

```text
PowerShell Activity
        ↓
ExecutionPolicy Bypass
        ↓
Windows Event ID 4688
        ↓
Universal Forwarder
        ↓
Splunk
        ↓
SPL Detection Search
        ↓
Analyst Investigation
```

---

## Telemetry Limitation

The lab demonstrated an important data-collection limitation.

PowerShell Script Block Logging Event ID `4104` and Sysmon events were present locally but were not successfully forwarded to Splunk.

As a result, the Splunk investigation relied primarily on Event ID `4688` command-line evidence.

---

## Security Significance

PowerShell execution-policy bypass activity should be reviewed in context.

The presence of `-ExecutionPolicy Bypass` alone does not establish that a compromise occurred. Analysts should correlate the event with the user, host, process tree, command line, timing, and other available security telemetry.

---

## Lab Classification

**Scenario:** P-5 — PowerShell Execution Policy Bypass  
**Environment:** Isolated SOC Lab  
**Activity Type:** Controlled Simulation  
**Primary Telemetry:** Windows Security Event ID 4688  
**Result:** Detection and investigation demonstrated

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
