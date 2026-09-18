# P-5 — PowerShell Execution Policy Bypass Evidence

## Scenario

P-5 tested controlled PowerShell execution-policy bypass activity in the isolated SOC lab.

The purpose was to verify whether Windows process-creation telemetry could capture the activity and make it available for investigation in Splunk.

---

## Detection Source

The primary telemetry used for the investigation was:

```text
Windows Security Event ID 4688
```

Event ID `4688` records process creation activity.

---

## Detection Indicator

The controlled P-5 activity was identified using:

```text
P5-Simulation
```

The analyst should also inspect the available command-line information for:

```text
-ExecutionPolicy Bypass
```

---

## SPL Detection Query

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4688 "P5-Simulation"
```

---

## Investigation

The analyst reviews the Event ID `4688` event for:

- Event timestamp
- Host
- User account
- New process name
- Creator process
- Command-line information
- PowerShell execution parameters

The `-ExecutionPolicy Bypass` parameter is treated as an investigation indicator and should be evaluated together with the surrounding telemetry.

---

## Telemetry Limitation

PowerShell Script Block Logging Event ID `4104` and Sysmon telemetry were available locally during the lab but were not successfully forwarded to Splunk.

Therefore, the P-5 investigation in Splunk was primarily based on the available Event ID `4688` process-creation evidence.

---

## Detection Result

The controlled P-5 activity was searchable in Splunk using the detection query.

The available Windows process-creation telemetry provided evidence for investigating the simulated PowerShell activity.

---

## Recommended Screenshots

Screenshots for this scenario will be stored separately in:

```text
screenshots/P5/
```

Recommended screenshots:

```text
P5-powershell-command.png
P5-event-4688.png
P5-splunk-search-result.png
P5-alert.png
```

---

## SOC Evidence Flow

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
Detection Search
        ↓
Analyst Investigation
```

---

## Lab Classification

**Scenario:** P-5 — PowerShell Execution Policy Bypass  
**Environment:** Isolated SOC Lab  
**Platform:** Windows 10  
**Primary Telemetry:** Windows Security Event ID 4688  
**Activity Type:** Controlled Simulation

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
