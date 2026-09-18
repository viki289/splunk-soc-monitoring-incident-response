# P-1 — Multiple Failed Login Attempts

## Detection Objective

Detect repeated failed authentication attempts against a user account.

## Windows Detection

```spl
index=wineventlogs sourcetype="WinEventLog:Security" EventCode=4625
| stats count as failed_attempts min(_time) as first_failure max(_time) as last_failure by host Account_Name
| where failed_attempts>=5
