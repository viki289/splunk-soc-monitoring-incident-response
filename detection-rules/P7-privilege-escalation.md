# P-7 — Privilege Escalation Detection

## Overview

This detection identifies controlled `sudo` privilege-elevation activity performed during the authorized SOC lab.

The P-7 scenario was designed to verify whether Linux privilege-related activity could be collected, forwarded to Splunk, searched, and investigated.

---

## Detection Objective

Detect a controlled `sudo` command executed by the P-7 test user.

The lab activity used the following indicators:

```text
sudo
p7
/usr/bin/id
```

These indicators are used to identify the controlled P-7 activity in the Ubuntu logs.

---

## SPL Detection Query

```spl
index=ubuntu_logs "sudo" "p7" "/usr/bin/id"
```

---

## How the Detection Works

The SPL query searches the Ubuntu log index for events containing all three investigation indicators:

- `sudo` — privilege-related command execution
- `p7` — controlled lab user/identifier
- `/usr/bin/id` — command executed during the simulation

The query helps the analyst locate the relevant P-7 event in Splunk.

---

## Lab Activity

During the controlled P-7 scenario, `sudo` was used to execute:

```text
/usr/bin/id
```

The activity was intentionally generated to demonstrate privilege-related telemetry in the isolated SOC environment.

---

## Detection Result

The relevant `sudo` activity was searchable in Splunk using the P-7 detection query.

The event provided evidence that the controlled privilege-related activity was recorded in the Ubuntu logs and made available for SOC investigation.

---

## Investigation Steps

An analyst investigating privilege-related activity should review:

1. Event timestamp
2. Ubuntu host
3. User account
4. `sudo` activity
5. Command executed
6. Authentication or authorization information
7. Related activity before and after the event

The analyst should determine whether the privilege-related command was authorized and expected.

---

## SOC Investigation Workflow

```text
Sudo Command
      ↓
Ubuntu System Log
      ↓
Universal Forwarder
      ↓
Splunk
      ↓
SPL Detection Search
      ↓
P-7 Investigation
      ↓
Analyst Review
```

---

## Security Significance

`sudo` is a legitimate Linux administrative mechanism that allows authorized users to execute commands with elevated privileges.

However, unexpected or unauthorized `sudo` activity can be an important security investigation indicator.

Therefore, the presence of `sudo` alone does not establish malicious activity. The analyst should review the user, command, timestamp, host, and surrounding events.

---

## Lab Classification

**Scenario:** P-7 — Privilege Escalation  
**Environment:** Isolated SOC Lab  
**Platform:** Ubuntu 24.04  
**Primary Indicator:** `sudo`  
**Command:** `/usr/bin/id`  
**Activity Type:** Controlled Simulation  
**Result:** Privilege-related activity successfully demonstrated

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
