# P-2 — Phishing Simulation Evidence

## Scenario

P-2 tested a controlled phishing URL simulation in the isolated SOC lab.

The activity was intentionally generated to verify that phishing-related indicators could be logged, forwarded to Splunk, searched, and investigated.

---

## Windows Evidence

The Windows simulation generated a synthetic application event using `eventcreate.exe`.

The event contained the controlled phishing URL indicator:

```text
https://example.com/loging
```

The event was recorded as Windows Event ID `1000`.

> The Windows event was synthetic telemetry generated for the lab. It was not organic browser telemetry.

---

## Ubuntu Evidence

The Ubuntu simulation used `logger` to generate a controlled log entry containing:

```text
https://example.com/login
```

The event was forwarded to Splunk for investigation.

---

## Detection Queries

### Windows

```spl
index=wineventlogs sourcetype="WinEventLog:Application" "example.com"
```

### Ubuntu

```spl
index=ubuntu_logs "Controlled phishing simulation URL accessed"
```

---

## Investigation Result

The controlled phishing indicators were searchable in Splunk.

No test-file download following the simulated phishing URL was identified during the lab investigation.

---

## Evidence Screenshots

Recommended screenshots for this scenario:

```text
P2-windows-phishing-event.png
P2-ubuntu-phishing-event.png
P2-splunk-search-result.png
P2-alert.png
```

Screenshots will be stored separately in the `screenshots/P2/` folder.

---

## Lab Classification

**Scenario:** P-2 — Phishing Simulation  
**Environment:** Isolated SOC Lab  
**Activity Type:** Controlled Simulation

> This activity was intentionally generated for cybersecurity training and detection-engineering purposes. It does not represent a real-world phishing attack.
