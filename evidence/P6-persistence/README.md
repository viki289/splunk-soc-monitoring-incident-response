# P-6 — Persistence Detection Evidence

## Scenario

P-6 tested controlled persistence mechanisms in the isolated SOC lab.

Two persistence methods were tested:

- Windows Scheduled Task
- Ubuntu Cron Job

The purpose was to verify that persistence-related activity could be logged, forwarded to Splunk, searched, and investigated.

---

## Windows Scheduled Task

A controlled Windows scheduled task named:

```text
P6-Lab-persistence
```

was created during the lab exercise.

The task was configured to execute:

```text
notepad.exe
```

at user logon.

---

## Windows Detection Source

The primary Windows telemetry was:

```text
Windows Security Event ID 4698
```

Event ID `4698` records scheduled-task creation activity.

---

## Windows SPL Detection Query

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4698 "P6-Lab-persistence"
```

---

## Ubuntu Cron Activity

A controlled cron job was created on Ubuntu.

The cron activity wrote date information to:

```text
/home/ubuntu/P6-Test/cron-Proof.txt
```

---

## Ubuntu SPL Detection Query

```spl
index=ubuntu_logs "CRON" "cron-Proof.txt"
```

---

## Investigation

The analyst reviews the persistence-related events for:

- Task or cron name
- Host
- User account
- Creation or execution time
- Command/action
- Related process activity

The analyst should determine whether the persistence mechanism is authorized and expected.

---

## Detection Result

The Windows scheduled-task activity was observable through Event ID `4698`.

The Ubuntu cron activity generated log events containing the `CRON` indicator and the controlled test-file name.

The persistence artifacts were removed during lab cleanup.

---

## Recommended Screenshots

Screenshots for this scenario will be stored separately in:

```text
screenshots/P6/
```

Recommended screenshots:

```text
P6-windows-scheduled-task.png
P6-event-4698.png
P6-ubuntu-cron.png
P6-splunk-search-result.png
P6-alert.png
```

---

## SOC Evidence Flow

### Windows

```text
Scheduled Task
      ↓
Event ID 4698
      ↓
Universal Forwarder
      ↓
Splunk
      ↓
Detection Rule
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
Detection Rule
      ↓
Analyst Investigation
```

---

## Lab Classification

**Scenario:** P-6 — Persistence Detection  
**Environment:** Isolated SOC Lab  
**Windows Telemetry:** Security Event ID 4698  
**Linux Telemetry:** Cron/System Logs  
**Activity Type:** Controlled Simulation

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
