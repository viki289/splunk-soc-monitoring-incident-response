# P-4 — Suspicious Process Evidence

## Scenario

P-4 tested controlled process execution activity in the isolated SOC lab.

The scenario used PowerShell to launch `notepad.exe` in order to verify that Windows process-creation telemetry could be collected and detected in Splunk.

---

## Detection Source

The primary detection source was Windows Security Event ID:

```text
4688
```

Event ID `4688` records process creation activity.

---

## Process Activity

The controlled activity involved:

```text
Creator Process: PowerShell
Target Process: notepad.exe
Account: vboxuser
Event ID: 4688
```

---

## SPL Detection Query

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4688 "notepad.exe"
```

---

## Investigation

The analyst reviewed the process-creation event to identify:

- Process name
- Creator process
- User account
- Host
- Event timestamp

The event showed `notepad.exe` being launched by PowerShell as part of the controlled P-4 simulation.

---

## Detection Result

The P-4 process-creation activity was successfully searchable in Splunk.

The configured P-4 detection alert was triggered during the controlled lab exercise.

The activity was confirmed as a benign simulation.

---

## Recommended Screenshots

Screenshots for this scenario will be stored separately in:

```text
screenshots/P4/
```

Recommended screenshots:

```text
P4-process-creation-event.png
P4-splunk-search-result.png
P4-alert.png
P4-powershell-notepad.png
```

---

## SOC Evidence Flow

```text
PowerShell
    ↓
notepad.exe
    ↓
Windows Event ID 4688
    ↓
Universal Forwarder
    ↓
Splunk
    ↓
Detection Rule
    ↓
P-4 Alert
    ↓
Analyst Investigation
```

---

## Lab Classification

**Scenario:** P-4 — Suspicious Process Detection  
**Environment:** Isolated SOC Lab  
**Platform:** Windows 10  
**Primary Telemetry:** Windows Security Event ID 4688  
**Activity Type:** Controlled Simulation

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
