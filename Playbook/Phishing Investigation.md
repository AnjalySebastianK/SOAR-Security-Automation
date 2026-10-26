# SOAR Playbook: Phishing Investigation

## Objective

Investigate suspected phishing emails by collecting email evidence, enriching indicators, analysing user interaction, assessing risk, and generating response recommendations for analyst review.

> **Important:** This playbook does not automatically quarantine emails, block domains, disable accounts, or perform containment actions. All response actions require analyst approval.

---

# Trigger Conditions

The playbook starts when one or more of the following conditions occur:

```bash
User Reports Suspicious Email

Email Security Gateway Alert

Microsoft Defender Alert

Phishing URL Detection

Malicious Attachment Detection

Threat Intelligence Match

Spoofed Domain Detection

Credential Harvesting Alert

SIEM Correlation Rule Match
```

---

# Required Fields

The following fields must be available before investigation begins:

```bash
Message ID

Sender Email Address

Sender Domain

Recipient Email Address

Email Subject

Delivery Timestamp

URLs Present

Attachments Present

Alert Severity

Mail Gateway Event ID
```

---

# Stage 1: Incident Creation

## Automated Actions

```bash
Create Incident Record

Generate Unique Incident ID

Assign Status = Investigating

Capture Email Metadata

Record Detection Source
```

### Example

```bash
Incident ID: PHISH-2026-001

Alert:
Suspicious Email Detected

User:
john.smith@company.com

Status:
Investigating
```

---

# Stage 2: Email Evidence Collection

## Objectives

Gather all email-related evidence.

---

## Collect Metadata

```bash
Sender Address

Reply-To Address

Sender Domain

Recipient List

Email Subject

Timestamp

Message Headers

Authentication Results
```

---

## Header Analysis

Review:

```bash
SPF Validation

DKIM Validation

DMARC Validation

Message Routing Path

Originating IP Address
```

---

## Example

```bash
SPF = Failed

DKIM = Failed

DMARC = Failed

Risk Indicator = High
```

---

# Stage 3: IOC Enrichment

## Objectives

Analyse all indicators contained within the email.

---

## Extract IOCs

```bash
URLs

Domains

IP Addresses

Email Addresses

Attachments

File Hashes
```

---

## Threat Intelligence Queries

```bash
VirusTotal

Microsoft Threat Intelligence

AbuseIPDB

AlienVault OTX

Internal Threat Intelligence Feed
```

---

## Collect Intelligence

```bash
URL Reputation

Domain Reputation

IP Reputation

Attachment Reputation

Hash Reputation

Threat Intelligence Hits
```

---

## Example

```bash
URL Reputation: Malicious

Domain Age: 5 Days

Hash Detection: Malware

Risk Score: High
```

---

# Stage 4: User Interaction Investigation

## Objectives

Determine whether the user interacted with the phishing email.

---

## Collect User Activity

```bash
Email Opened

Link Clicked

Attachment Downloaded

Attachment Executed

Credentials Submitted

Browser Activity
```

---

## Important Questions

```bash
Did the user click the URL?

Did the user download a file?

Did the user provide credentials?

Did the user access a suspicious website?

Did additional users interact with the email?
```

---

## Example

```bash
Email Opened = Yes

URL Clicked = Yes

Attachment Downloaded = No

Credentials Submitted = Unknown
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

Risk Level
```

---

## Email Campaign Analysis

Check:

```bash
Other Recipients

Similar Messages

Matching Subjects

Repeated Sender Activity

Related Email Campaigns
```

---

## Endpoint Context

Query:

```bash
EDR Platform

Microsoft Defender

CrowdStrike

SentinelOne
```

Collect:

```bash
Processes

Downloads

Network Connections

Malware Detections
```

---

# Stage 6: Risk Scoring

## High-Risk Indicators

```bash
Credential Harvesting Site

Known Malicious URL

Known Malicious Domain

Malware Attachment

Executive User Targeted

Multiple Users Affected

User Clicked Link
```

---

## Medium-Risk Indicators

```bash
Domain Spoofing

Unknown Sender

Suspicious Attachment

Newly Registered Domain

URL Redirection
```

---

## Low-Risk Indicators

```bash
No User Interaction

Trusted Sender

No Malicious Indicators

Known Internal Communication
```

---

## Risk Calculation Example

```bash
Malicious URL = +40

User Clicked URL = +20

Malware Attachment = +30

Multiple Victims = +10

Total Score = 100

Risk Level = Critical
```

---

# Stage 7: Risk-Based Branching

## Low Risk

### Conditions

```bash
No User Interaction

Good Reputation Scores

No Threat Intelligence Matches
```

### Actions

```bash
Document Findings

Prepare Analyst Summary

Assign Tier 1 Review
```

---

## Medium Risk

### Conditions

```bash
Suspicious Domain

Unknown Sender

Limited User Interaction
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
Malicious URL

Malware Attachment

Credential Theft Indicators

Multiple Victims
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
Quarantine Email

Delete Email

Block Domain

Block URL

Disable User Account

Reset User Password

Force MFA Registration

Isolate Endpoint
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
Use Backup Source
          ↓
Create Warning Record
```

---

## Email Retrieval Failure

```bash
Message Not Found
       ↓
Retry Search
       ↓
Use Alternate Source
       ↓
Escalate To Analyst
```

---

## Missing Evidence

Examples:

```bash
Missing Headers

Missing URLs

Corrupted Attachments
```

Action:

```bash
Flag Investigation Gap

Mark Evidence Missing

Escalate For Analyst Review
```

---

## Security Tool Failure

```bash
EDR Unavailable
        ↓
Log Error
        ↓
Notify Platform Owner
        ↓
Continue Investigation
```

---

# Stage 10: Reporting

## Investigation Report

Generate:

```bash
Incident ID

Sender Information

Recipient Information

Email Subject

Extracted IOCs

Threat Intelligence Results

User Interaction Details

Risk Score

Investigation Findings

Recommended Actions
```

---

## Metrics Collected

```bash
Number Of Recipients

Clicked URLs

Downloaded Attachments

Threat Intelligence Hits

Investigation Duration

Approval Status
```

---

## Executive Summary Example

```bash
Incident:
Phishing Investigation

Sender:
alerts-secure-support.com

Victims:
12 Users

Risk:
Critical

Reason:
Malicious URL +
Credential Harvesting Site +
Multiple User Clicks

Recommended Action:
Analyst Review Required

Automated Response:
Not Executed
```

---

# End-to-End Workflow

```bash
Phishing Alert
       ↓
Create Incident
       ↓
Validate Required Fields
       ↓
Collect Email Evidence
       ↓
IOC Enrichment
       ↓
User Interaction Analysis
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

✓ No automatic account actions

✓ Human approval mandatory

✓ Email and IOC enrichment

✓ Threat intelligence integration

✓ User interaction analysis

✓ Risk-based decision making

✓ Comprehensive reporting

✓ Full audit trail

✓ Strong error handling
```

### Interview Summary

```bash
This SOAR phishing investigation playbook collects email evidence, enriches URLs, domains, IPs, and attachments using threat intelligence, analyses user interaction, calculates risk, and generates recommendations for analyst review. All remediation actions require explicit analyst approval to maintain governance and prevent false-positive response actions.
```
