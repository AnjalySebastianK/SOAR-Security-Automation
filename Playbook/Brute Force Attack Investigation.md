# SOAR Playbook: Brute Force Attack Investigation

## Objective

Investigate suspected brute force authentication attacks by analysing login activity, enriching source IP intelligence, reviewing authentication history, assessing risk, and providing response recommendations for analyst review.

> **Important:** This playbook does not automatically lock accounts, block IP addresses, reset passwords, or perform containment actions. All response actions require analyst approval.

---

# Trigger Conditions

The playbook starts when one or more of the following conditions occur:

```bash
Multiple Failed Login Attempts

Password Spray Detection

Identity Protection Alert

VPN Authentication Alert

Active Directory Alert

Microsoft Defender Alert

Successful Login After Multiple Failures

Multiple Accounts Targeted

Geographically Distributed Login Attempts

Privileged Account Authentication Alert
```

---

# Required Fields

The following fields must be available before investigation begins:

```bash
Username

User ID

Source IP Address

Timestamp

Authentication Source

Authentication Result

Number Of Failed Attempts

Target System

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

Record Detection Source
```

### Example

```bash
Incident ID: BRUTE-2026-001

Alert:
Brute Force Authentication Attempt

User:
administrator

Status:
Investigating
```

---

# Stage 2: Authentication Evidence Collection

## Objectives

Collect detailed authentication evidence.

---

## Gather Authentication Data

```bash
Username

Source IP

Target System

Failed Login Count

Successful Login Count

Authentication Protocol

Authentication Source

Login Timestamps
```

---

## Authentication Log Analysis

Review:

```bash
Windows Event Logs

Active Directory Logs

VPN Logs

Cloud Authentication Logs

Identity Provider Logs
```

---

## Example

```bash
Failed Attempts: 145

Successful Login: Yes

Authentication Source:
VPN

Severity:
High
```

---

# Stage 3: IP Reputation Enrichment

## Objectives

Determine whether the source IP is associated with malicious activity.

---

## Threat Intelligence Queries

```bash
VirusTotal

AbuseIPDB

Microsoft Threat Intelligence

AlienVault OTX

Recorded Future

Internal Threat Feed
```

---

## Collect Intelligence

```bash
IP Reputation Score

Geolocation

Known Malicious Activity

TOR Exit Node Status

VPN Detection

Blacklist Status

Botnet Activity

Threat Intelligence Hits
```

---

## Example

```bash
IP Address:
185.x.x.x

Country:
Russia

Abuse Score:
98%

TOR Node:
Yes

Risk:
High
```

---

# Stage 4: Authentication History Analysis

## Objectives

Review previous authentication behaviour.

---

## Gather Historical Activity

```bash
Recent Successful Logins

Recent Failed Logins

Known Devices

Previous Login Locations

Authentication Patterns

MFA Success Records

Password Reset History
```

---

## Investigation Questions

```bash
Has this user experienced similar attacks?

Has this IP connected previously?

Has MFA been successful?

Was there a successful login after failures?

Are multiple accounts being targeted?
```

---

## Example

```bash
Previous Login:
India

Current Source:
Russia

Known Device:
No

Failed Attempts:
145

Successful Login:
Yes
```

---

# Stage 5: Context Gathering

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

Collect:

```bash
Hostname

Server Name

Criticality Rating

Operating System

Business Function
```

---

## Additional Security Context

Query:

```bash
SIEM

EDR Platform

Identity Provider

VPN Solution

Cloud Security Logs
```

Retrieve:

```bash
Related Alerts

Previous Incidents

Compromised Credentials

Suspicious Processes

Account Lockout Events
```

---

# Stage 6: Risk Scoring

## High-Risk Indicators

```bash
Successful Login After Failures

Known Malicious IP

Privileged Account

TOR Usage

Password Spray Indicators

Multiple Accounts Targeted

MFA Bypass Attempt
```

---

## Medium-Risk Indicators

```bash
High Failed Login Count

Unknown Location

Unknown Device

Repeated Login Attempts
```

---

## Low-Risk Indicators

```bash
Internal Source

Known Device

Known Location

Successful MFA

Low Failed Login Count
```

---

## Risk Calculation Example

```bash
Successful Login After Failures = +40

Malicious IP = +30

Privileged Account = +20

TOR Usage = +10

Total Score = 100

Risk Level = Critical
```

---

# Stage 7: Risk-Based Branching

## Low Risk

### Conditions

```bash
Known Location

Known Device

Successful MFA

Good IP Reputation
```

### Actions

```bash
Document Findings

Generate Summary

Assign Tier 1 Review
```

---

## Medium Risk

### Conditions

```bash
High Failed Login Volume

Unknown Location

New Device
```

### Actions

```bash
Collect Additional Evidence

Expand Investigation

Assign Tier 2 Review
```

---

## High Risk

### Conditions

```bash
Successful Compromise Indicators

Known Malicious IP

Password Spray Activity

Privileged Account Involved
```

### Actions

```bash
Generate High Severity Incident

Notify SOC Team

Require Immediate Analyst Review
```

---

# Stage 8: Analyst Approval Required

## Approval Gate

The following actions require analyst approval:

```bash
Account Lockout

Disable Account

Password Reset

MFA Enforcement

IP Blocking

VPN Session Termination

Privilege Revocation
```

---

## Approval Workflow

```bash
Investigation Complete
          ↓
Generate Findings
          ↓
Analyst Review
          ↓

Approve Action?
     ↓      ↓

   YES      NO
    ↓        ↓

Recommend   Close
Response     Case
```

---

# Stage 9: Error Handling

## Threat Intelligence Failure

```bash
Threat Feed Unavailable
         ↓
Retry Three Times
         ↓
Use Secondary Source
         ↓
Generate Warning
```

---

## Authentication Log Failure

```bash
Unable To Retrieve Logs
           ↓
Retry Query
           ↓
Use Backup Logging Source
           ↓
Escalate To Analyst
```

---

## Missing Evidence

Examples:

```bash
Missing Username

Missing Authentication Logs

Missing Source IP

Incomplete Login History
```

Action:

```bash
Flag Evidence Gap

Mark Investigation Incomplete

Request Manual Review
```

---

## Integration Failure

```bash
Identity Provider Offline
           ↓
Create Error Record
           ↓
Notify Platform Team
```

---

# Stage 10: Reporting

## Investigation Report

Generate:

```bash
Incident ID

Username

Source IP

Failed Login Count

Successful Login Events

Authentication History

Threat Intelligence Results

Risk Score

Evidence Collected

Recommended Actions
```

---

## Metrics Collected

```bash
Failed Login Volume

Number Of Targeted Accounts

Successful Logins

Threat Intelligence Hits

Investigation Duration

Risk Classification

Approval Status
```

---

## Executive Summary Example

```bash
Incident:
Brute Force Attack Investigation

User:
administrator

Risk:
Critical

Reason:
Successful Login After Failures +
Known Malicious IP +
Privileged Account

Failed Attempts:
145

Recommended Action:
Analyst Review Required

Automated Response:
Not Executed
```

---

# End-to-End Workflow

```bash
Brute Force Alert
          ↓
Create Incident
          ↓
Validate Required Fields
          ↓
Authentication Evidence Collection
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
✓ No automated account lockouts

✓ No automated password resets

✓ Human approval mandatory

✓ Authentication-focused investigation

✓ Multiple threat intelligence sources

✓ Risk-based decision making

✓ Strong governance controls

✓ Full audit trail

✓ Comprehensive reporting

✓ Robust error handling
```

### Interview Summary

```bash
This SOAR brute force investigation playbook analyses authentication activity, enriches source IPs using threat intelligence, reviews login history, calculates risk based on attack indicators, and generates recommendations for analyst review. All containment and account actions require explicit human approval to minimise false positives and operational disruption.
```
