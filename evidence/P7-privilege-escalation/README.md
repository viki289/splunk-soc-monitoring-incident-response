# P-7 — Privilege Escalation Evidence

## Scenario

P-7 tested controlled `sudo` privilege-related activity in the isolated SOC lab.

The purpose was to verify that Linux privilege-related activity could be logged, forwarded to Splunk, searched, and investigated.

---

## Detection Indicator

The controlled P-7 activity used the following indicators:

```text
sudo
p7
/usr/bin/id
```

These indicators were used to identify the controlled activity in the Ubuntu logs.

---

## SPL Detection Query

```spl
index=ubuntu_logs "sudo" "p7" "/usr/bin/id"
```

---

## Lab Activity

During the P-7 scenario, `sudo` was used to execute:

```text
/usr/bin/id
```

The activity was intentionally generated as part of the controlled SOC lab exercise.

---

## Investigation

The analyst reviews the event for:

- Event timestamp
- Ubuntu host
- User account
- `sudo` activity
- Command executed
- Authorization information
- Related activity before and after the event

The analyst should determine whether the privilege-related command was authorized and expected.

---

## Detection Result

The relevant `sudo` activity was searchable in Splunk using the P-7 detection query.

The event provided evidence that the controlled privilege-related activity was recorded in Ubuntu logs and made available for SOC investigation.

---

## Recommended Screenshots

Screenshots for this scenario will be stored separately in:

```text
screenshots/P7/
```

Recommended screenshots:

```text
P7-sudo-command.png
P7-ubuntu-log.png
P7-splunk-search-result.png
P7-alert.png
```

---

## SOC Evidence Flow

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

Unexpected or unauthorized `sudo` activity can therefore be an important investigation indicator.

The presence of `sudo` alone does not establish malicious activity. The analyst should review the user, command, timestamp, host, and surrounding events.

---

## Lab Classification

**Scenario:** P-7 — Privilege Escalation  
**Environment:** Isolated SOC Lab  
**Platform:** Ubuntu 24.04  
**Primary Indicator:** `sudo`  
**Command:** `/usr/bin/id`  
**Activity Type:** Controlled Simulation

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world compromise.
