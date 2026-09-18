# P-1 — Authentication Brute-Force Evidence

## Scenario

P-1 tested repeated failed authentication attempts followed by successful authentication activity in the isolated SOC lab.

The scenario was performed on both Windows and Ubuntu systems.

---

## Windows Evidence

### Detection Events

Windows Security Event ID `4625` was used to identify failed logon attempts.

The lab recorded multiple failed logon attempts for the `vboxuser` account, followed by successful logon events using Event ID `4624`.

### Observed Pattern

```text
Multiple Failed Logons
        ↓
Event ID 4625
        ↓
Repeated Attempts
        ↓
Successful Logon
        ↓
Event ID 4624
        ↓
SOC Investigation
```

---

## Ubuntu Evidence

Ubuntu SSH authentication logs contained multiple:

```text
Failed password
```

events during the controlled authentication test.

These events were forwarded to Splunk for investigation.

---

## Evidence Screenshots

Add the screenshots collected during the P-1 exercise to this folder.

Recommended screenshot names:

```text
P1-windows-failed-logins.png
P1-windows-successful-login.png
P1-ubuntu-ssh-failed-login.png
P1-splunk-detection-result.png
P1-alert.png
```

---

## Evidence Purpose

These screenshots should demonstrate:

- Failed authentication events
- Successful authentication activity
- Splunk search results
- Detection-rule results
- Alert generation

---

## Lab Classification

**Scenario:** P-1 — Authentication Brute-Force  
**Environment:** Isolated SOC Lab  
**Activity Type:** Controlled Simulation

> The activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world attack.
