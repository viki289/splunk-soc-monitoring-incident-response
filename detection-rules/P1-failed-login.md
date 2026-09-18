# P-1 — Multiple Failed Login Attempts

## Overview

This detection identifies repeated failed authentication attempts against a user account.

In this SOC lab, the scenario simulates multiple incorrect login attempts and demonstrates how Splunk can detect the activity from Windows Security Event Logs.

---

## Windows Detection

### What are we detecting?

Windows Security Event ID `4625` is generated when a logon attempt fails.

The detection looks for **5 or more failed login attempts** for the same account.

### SPL Query

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4625
| stats count as failed_attempts min(_time) as first_failure max(_time) as last_failure by host Account_Name
| where failed_attempts>=5
