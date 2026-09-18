# P-3 — EICAR Test Artifact Detection

## Overview

This detection identifies the EICAR test artifact reported by ClamAV.

The EICAR file is used as a safe antivirus test artifact in the authorized SOC lab to verify that malware-detection telemetry can be generated, forwarded to Splunk, searched, and alerted on.

---

## Detection Objective

Detect the ClamAV signature:

```text
Eicar-Test-Signature
```

## SPL Detection Query

```spl
index=ubuntu_logs sourcetype="clamav:eicar" "Eicar-Test-Signature"
```
