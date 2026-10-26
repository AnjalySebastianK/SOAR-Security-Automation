# SOAR Playbook: Suspicious Login Investigation

## Objective

Investigate suspicious login activity by collecting authentication evidence, enriching IP reputation data, analysing user behaviour, and providing recommendations for analyst review.

> **Important:** This playbook does not perform automated containment or account actions. All response actions require analyst approval.

---

# Trigger Conditions

The playbook starts when one or more of the following conditions occur:

```bash
Impossible Travel Detection

Login From New Country

Login From Anonymous IP

Login Outside Normal Business Hours

Multiple Failed Logins Followed By Success

Login From High-Risk Location

MFA Failure Events

Privileged Account Login Anomaly

Identity Protection Alert

UEBA Alert
```

---

# Required Fields

The following fields must be present before investigation begins:

```bash
Username

User ID

Source IP Address

Timestamp

Location

Device Information

Authentication Method

Application Accessed

Login Result

Account Type

Alert Severity
```

---

# Stage 1: Incident Creation

## Automated Actions

```bash
Create Incident Record

Generate Unique Incident ID

Assign Status = Investigating

Capture Alert Metadata

Record Trigger Source
```

### Example

```bash
Incident ID: AUTH-2026-001

Alert:
Impossible Travel Login

User:
j.smith

Status:
Investigating
```

---

# Stage 2: IP Reputation Enrichment

## Objectives

Determine whether the login originated from a known suspicious source.

---

## Threat Intelligence Queries

Query:

```bash
VirusTotal

AbuseIPDB

Microsoft Threat Intelligence

Recorded Future

Internal Threat Intelligence Feed
```

---

## Collect IP Intelligence

```bash
IP Reputation Score

Geographical Location

ASN Information

VPN Usage

Proxy Detection

TOR Exit Node Status

Blacklist Presence

Threat Intelligence Hits
```

---

## Example

```bash
Source IP: 185.x.x.x

Country: Russia

TOR Exit Node: Yes

Abuse Score: 95%

Risk Level: High
```

---

# Stage 3: Authentication History Analysis

## Objectives

Review previous authentication activity for the user.

---

## Gather Historical Data

```bash
Previous Logins

Successful Logins

Failed Logins

MFA Activity

Location History

Device History

Application Usage

Known Trusted Devices
```

---

## Authentication Questions

```bash
Has the user logged in from this country before?

Has this device been seen before?

Have authentication failures increased recently?

Has MFA been bypassed?

Did login behaviour change suddenly?
```

---

## Example

```bash
Previous Login:
India

Current Login:
Russia

Known Device:
No

Recent Failures:
27
```

---

# Stage 4: Context Gathering

## User Context

Retrieve:

```bash
Department

Job Title

Manager

Privileged Access Status

Account Criticality
```

---

## Asset Context

Retrieve:

```bash
Hostname

Operating System

Managed Device Status

Asset Criticality

Endpoint Security Status
```

---

## Recent Security Activity

Query:

```bash
SIEM

EDR

Identity Provider

VPN Logs

Cloud Audit Logs
```

---

# Stage 5: Risk Scoring

## Risk Factors

### High-Risk Indicators

```bash
TOR Node

Known Malicious IP

Impossible Travel

Privileged Account

MFA Failure

Credential Stuffing Indicators

Anonymous Proxy Usage
```

---

### Medium-Risk Indicators

```bash
New Country

Unknown Device

After-Hours Login

Multiple Failed Attempts
```

---

### Low-Risk Indicators

```bash
Known Device

Known Location

Successful MFA

No Additional Alerts
```

---

## Risk Calculation Example

```bash
Impossible Travel = +30

Unknown Device = +20

High-Risk IP = +30

MFA Failure = +20

Total Score = 100

Risk Level = Critical
```

---

# Stage 6: Risk-Based Branching

## Low Risk

### Conditions

```bash
Known Device

Known Location

Valid MFA

Good IP Reputation
```

### Actions

```bash
Document Findings

Prepare Analyst Summary

Route To Tier 1 Analyst
```

---

## Medium Risk

### Conditions

```bash
Unknown Device

Unusual Location

Minor Authentication Anomalies
```

### Actions

```bash
Collect Additional Logs

Generate Investigation Package

Escalate To Tier 2 Analyst
```

---

## High Risk

### Conditions

```bash
Known Malicious IP

Impossible Travel

Privileged Account

Multiple Detection Sources
```

### Actions

```bash
Generate High Severity Incident

Notify SOC Team

Require Immediate Analyst Review
```

---

# Stage 7: Analyst Approval Required

## Approval Gate

Before any response action is executed:

```bash
Account Disablement

Password Reset

Session Revocation

MFA Enforcement

Network Blocking

Device Isolation
```

Must receive:

```bash
Tier 2 Approval

Incident Response Approval

SOC Manager Approval
```

Depending on severity.

---

## Approval Workflow

```bash
Investigation Complete
           ↓
Prepare Incident Summary
           ↓
Analyst Review
           ↓

Approve Action?
      ↓      ↓

    YES      NO
     ↓        ↓

Recommend  Close
Response     Case
```

---

# Stage 8: Error Handling

## Threat Intelligence Failure

```bash
Threat Feed Unavailable
          ↓
Retry Three Times
          ↓
Use Secondary Threat Feed
          ↓
Generate Warning
```

---

## SIEM Query Failure

```bash
Log Retrieval Failed
        ↓
Retry Request
        ↓
Use Backup Query
        ↓
Escalate To Analyst
```

---

## Missing Data

```bash
Missing Username

Missing IP

Incomplete Logs
```

Action:

```bash
Mark Investigation Incomplete

Request Manual Review

Flag Evidence Gap
```

---

## Integration Failure

```bash
EDR Not Reachable
          ↓
Create Error Record
          ↓
Notify Security Platform Team
```

---

# Stage 9: Reporting

## Investigation Report

Automatically generate:

```bash
Incident ID

Username

Source IP

Location

Risk Score

Authentication History

Threat Intelligence Results

Evidence Collected

Analyst Notes

Recommended Actions
```

---

## Metrics Collected

```bash
Investigation Duration

Number Of Alerts

Risk Classification

Authentication Failures

Enrichment Sources Queried

Approval Status
```

---

## Executive Summary Example

```bash
Incident:
Suspicious Login Investigation

User:
john.smith

Risk:
High

Reason:
Impossible Travel +
Known Malicious IP +
Failed MFA

Recommended Action:
Analyst Review Required

Automated Response:
Not Executed
```

---

# End-to-End Workflow

```bash
Suspicious Login Alert
           ↓
Create Incident
           ↓
Validate Required Fields
           ↓
IP Reputation Enrichment
           ↓
Authentication History Analysis
           ↓
Context Gathering
           ↓
Risk Scoring
           ↓
Risk-Based Branching
           ↓
Analyst Approval Stage
           ↓
Generate Report
           ↓
Close Investigation
```

---

# Key Design Principles

```bash
✓ No automated containment

✓ Human approval mandatory

✓ Comprehensive authentication review

✓ Multiple threat intelligence sources

✓ Risk-based investigation paths

✓ Full audit trail

✓ Error handling and retries

✓ Detailed reporting and case documentation
```

### Interview Summary

```bash
This SOAR playbook investigates suspicious logins by enriching IP reputation, analysing authentication history, gathering contextual evidence, calculating risk, and producing recommendations. All response actions require analyst approval, ensuring strong governance and reducing the risk of false-positive containment actions.
```
