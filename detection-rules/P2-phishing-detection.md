# P-2 — Phishing URL Simulation Detection

## Overview

This detection identifies activity associated with a controlled phishing-URL simulation.

The scenario was performed in the authorized SOC lab to demonstrate how suspicious URL indicators can be detected through Windows Application Logs and Ubuntu syslog data.

---

## Windows Detection

### What are we detecting?

The Windows simulation generated an Application Log event containing a controlled phishing URL indicator.

### SPL Query

```spl
index=wineventlogs sourcetype="WinEventLog:Application" "example.com"

