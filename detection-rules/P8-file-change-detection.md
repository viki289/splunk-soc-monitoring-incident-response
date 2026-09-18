# P-8 — File Change Detection

## Overview

This detection identifies rapid file activity generated during the controlled P-8 scenario in the authorized SOC lab.

The scenario simulated ransomware-like file changes to test whether repeated file-system activity could be detected and investigated using Splunk.

---

## Detection Objective

Detect a high volume of file events occurring within a short time period.

The detection uses Windows Security Event ID `4663`, which provides object-access activity.

The detection looks for:

- At least `5` file events
- At least `2` unique files
- Activity occurring within a `1-minute` time window
- Files matching the controlled `P8-Test` pattern

---

## SPL Detection Query

```spl
index=wineventlogs EventCode=4663
| search Object_Name="*P8-Test*"
| bin _time span=1m
| stats count as file_events dc(Object_Name) as unique_files by _time host Account_Name
| where file_events>=5 AND unique_files>=2
```

---

## How the Detection Works

The SPL query performs the following steps:

### 1. Search Windows File Events

```spl
index=wineventlogs EventCode=4663
```

Searches for Windows Security Event ID `4663`.

### 2. Filter Controlled Test Files

```spl
| search Object_Name="*P8-Test*"
```

Limits the results to objects associated with the controlled P-8 test activity.

### 3. Create One-Minute Time Windows

```spl
| bin _time span=1m
```

Groups file events into one-minute intervals.

### 4. Count File Events

```spl
| stats count as file_events
```

Counts the number of file events in each time window.

### 5. Count Unique Files

```spl
dc(Object_Name) as unique_files
```

Counts the number of distinct file objects observed.

### 6. Apply Detection Threshold

```spl
| where file_events>=5 AND unique_files>=2
```

Returns activity when both detection conditions are satisfied.

---

## Lab Activity

During the controlled P-8 scenario, rapid file changes were intentionally generated against test files associated with the P-8 exercise.

The purpose was to create a detectable pattern of repeated file-system activity rather than to simulate an actual ransomware infection.

---

## Detection Result

The Splunk detection searched for repeated Windows file-access events and applied the configured threshold.

The detection was designed to identify activity involving multiple test files within a short period.

---

## Investigation Steps

An analyst investigating the alert should review:

1. Event timestamp
2. Host
3. User account
4. Number of file events
5. Number of unique files
6. Affected file names
7. Process information, when available
8. Related events before and after the file activity

The analyst should determine whether the activity was expected, part of a controlled test, or requires additional investigation.

---

## SOC Workflow

```text
Rapid File Changes
        ↓
Windows Event ID 4663
        ↓
Universal Forwarder
        ↓
Splunk
        ↓
SPL Detection
        ↓
Threshold Evaluation
        ↓
P-8 Alert
        ↓
Analyst Investigation
```

---

## Detection Logic

| Condition | Threshold |
|---|---:|
| File events | 5 or more |
| Unique files | 2 or more |
| Time window | 1 minute |
| Event ID | 4663 |
| File pattern | `P8-Test` |

The alert is intended to highlight unusually rapid file activity involving multiple files.

---

## Security Significance

A sudden increase in file-system activity across multiple files can be an investigation indicator in some security incidents.

However, high-volume file activity can also result from legitimate applications, administrative operations, backups, software updates, or other normal system behavior.

Therefore, the alert should be investigated together with the affected host, user, process, file names, and surrounding telemetry.

---

## Lab Classification

**Scenario:** P-8 — File Change Detection  
**Environment:** Isolated SOC Lab  
**Platform:** Windows 10  
**Primary Telemetry:** Windows Security Event ID 4663  
**Detection Window:** 1 minute  
**Activity Type:** Controlled Simulation  
**Result:** Rapid file-activity detection demonstrated

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world ransomware incident.
