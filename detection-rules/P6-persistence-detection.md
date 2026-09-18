# P-6 — Persistence Detection

## Overview

This detection identifies controlled persistence activity created during the authorized SOC lab.

The P-6 scenario tested two persistence mechanisms:

- Windows Scheduled Task
- Ubuntu Cron Job

The purpose was to verify that persistence-related telemetry could be generated, forwarded to Splunk, searched, and investigated.

---

## Detection Objective

Detect the creation of the controlled Windows scheduled task and the execution of the controlled Ubuntu cron job.

---

## Windows Detection

Windows Scheduled Task creation generates Security Event ID `4698`.

### SPL Detection Query

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4698 "P6-Lab-persistence"
```

### Detection Indicator

The primary indicator is the controlled scheduled-task name:

```text
P6-Lab-persistence
```

The analyst should review the Event ID `4698` event to determine:

- Task name
- Task creation time
- User account
- Task action
- Target host

---

## Ubuntu Detection

The Ubuntu scenario used a controlled cron job that wrote timestamp information to a test file.

### SPL Detection Query

```spl
index=ubuntu_logs "CRON" "cron-Proof.txt"
```

### Detection Indicator

The primary indicator is:

```text
cron-Proof.txt
```

The analyst can review the event timestamp, host, user, and cron-related information.

---

## How the Detection Works

The detection searches the appropriate Splunk index for persistence-related activity.

### Windows

```text
Windows Scheduled Task
        ↓
Security Event ID 4698
        ↓
Universal Forwarder
        ↓
Splunk
        ↓
SPL Detection
        ↓
Analyst Investigation
```

### Ubuntu

```text
Cron Job
        ↓
System Log
        ↓
Universal Forwarder
        ↓
Splunk
        ↓
SPL Detection
        ↓
Analyst Investigation
```

---

## Lab Activity

During the controlled P-6 scenario, a Windows scheduled task named:

```text
P6-Lab-persistence
```

was created using the Windows Task Scheduler command-line utility.

The task was configured to execute `notepad.exe` at user logon.

On Ubuntu, a controlled cron entry was created that periodically wrote date information to:

```text
/home/ubuntu/P6-Test/cron-Proof.txt
```

The persistence artifacts were subsequently removed as part of the lab cleanup process.

---

## Detection Result

The Windows scheduled-task activity was observable through Security Event ID `4698`.

The Ubuntu cron activity generated log events containing the `CRON` indicator and the controlled test-file name.

These events provided evidence that persistence-related activity could be searched and investigated in Splunk.

---

## Investigation Steps

An analyst investigating persistence should review:

1. Persistence mechanism
2. Creation timestamp
3. User account
4. Host
5. Task or cron entry name
6. Command or action executed
7. Related process activity
8. Whether the persistence mechanism is authorized

The analyst should correlate the persistence event with other available endpoint and authentication telemetry.

---

## Security Significance

Scheduled tasks and cron jobs are legitimate system administration mechanisms, but they can also be used to maintain execution or recurring activity.

Therefore, detection of a scheduled task or cron job does not by itself prove malicious activity. The analyst should investigate the creator, command, timing, target system, and surrounding events.

---

## Lab Classification

**Scenario:** P-6 — Persistence Detection  
**Environment:** Isolated SOC Lab  
**Windows Telemetry:** Security Event ID 4698  
**Linux Telemetry:** Cron/System Logs  
**Activity Type:** Controlled Simulation  
**Result:** Persistence detection demonstrated

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
