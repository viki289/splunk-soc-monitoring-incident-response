# P-3 — EICAR Test Artifact Evidence

## Scenario

P-3 tested detection of the EICAR antivirus test artifact using ClamAV in the isolated SOC lab.

The EICAR file is a safe test artifact used to verify antivirus detection and SOC monitoring.

---

## Detection Source

The EICAR test artifact was detected by ClamAV and generated the following signature:

```text
Eicar-Test-Signature
```

The detection was ingested into Splunk with:

```text
sourcetype=clamav:eicar
```

---

## SPL Detection Query

```spl
index=ubuntu_logs sourcetype="clamav:eicar" "Eicar-Test-Signature"
```

---

## Test Artifact

The genuine EICAR test file used during the lab was:

```text
eicar.com
```

MD5:

```text
44d88612fea8a8f36de82e1278abb02f
```

---

## Initial Test Observation

An initial manually entered EICAR string contained transcription errors.

ClamAV did not detect that malformed test string.

A genuine EICAR test artifact was subsequently used and ClamAV successfully detected it.

This demonstrated the importance of validating the test artifact when troubleshooting detection results.

---

## Splunk Evidence

The ClamAV detection was successfully forwarded to Splunk and could be searched using the P-3 detection query.

The investigation returned matching EICAR detection events.

---

## Alert

The configured real-time alert was:

```text
P3 - Malware Detection - Ubuntu EICAR
```

The alert was used to demonstrate automated detection of the test artifact.

---

## Recommended Screenshots

The screenshots for this scenario will be stored separately in:

```text
screenshots/P3/
```

Recommended screenshots:

```text
P3-clamav-eicar-detection.png
P3-splunk-search-result.png
P3-alert.png
P3-eicar-file.png
```

---

## Investigation Result

The genuine EICAR test artifact was successfully detected by ClamAV and the resulting telemetry was available in Splunk.

The activity was confirmed as a controlled antivirus test and not a real malware infection.

---

## Lab Classification

**Scenario:** P-3 — EICAR Test Artifact Detection  
**Environment:** Isolated SOC Lab  
**Detection Source:** ClamAV  
**Splunk Sourcetype:** `clamav:eicar`  
**Activity Type:** Controlled Security Test

> EICAR is a benign antivirus test artifact used for security testing. This lab activity was intentionally generated for cybersecurity training and detection-engineering purposes.
