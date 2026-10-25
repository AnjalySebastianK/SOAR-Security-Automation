# Design SOAR Playbooks

## Overview

SOAR playbooks provide structured, repeatable, and automated workflows for handling security incidents. They enable Security Operations Centre (SOC) teams to reduce response times, improve consistency, and minimise manual effort.

This document contains SOAR playbook designs for:

1. Phishing Attack
2. Denial of Service (DoS) Attack
3. Brute Force Attack
4. Suspicious PowerShell Activity

---

# 1. Phishing Playbook

## Objective

Detect, investigate, contain, and remediate phishing emails while protecting users and preventing credential compromise.

---

## Trigger

```bash
Email Security Alert
User Reported Suspicious Email
SIEM Detection Rule
Defender for Office 365 Alert
```

---

## Automated Investigation

### Step 1: Collect Email Details

```bash
Extract Sender Address
Extract Subject Line
Extract URLs
Extract Attachments
Extract Recipient List
```

### Step 2: Threat Intelligence Checks

```bash
Check Sender Reputation
Check Domain Reputation
Check URL Reputation
Check Attachment Hash Reputation
```

### Step 3: Context Gathering

```bash
Identify Recipient Users
Check Similar Emails
Review User Click Activity
Review Previous Phishing Incidents
```

---

## Decision Logic

```bash
IF Email Reputation = Malicious
THEN Continue Containment

ELSE
Escalate For Manual Review
```

---

## Automated Response

```bash
Quarantine Email
Remove Similar Emails
Block Sender Domain
Block Malicious URLs
Create Incident Ticket
Notify Security Team
```

---

## Escalation Criteria

```bash
Executive User Targeted
Credential Submission Detected
Multiple Users Affected
Malware Attachment Detected
```

---

## Closure

```bash
Document Findings
Update Incident Record
Generate Report
Close Ticket
```

---

## Workflow

```bash
Phishing Alert
       ↓
Extract Email Data
       ↓
Threat Intelligence Check
       ↓
Assess Risk
       ↓
Quarantine Email
       ↓
Block Infrastructure
       ↓
Notify Users
       ↓
Generate Ticket
       ↓
Close Incident
```

---

# 2. Denial of Service (DoS) Playbook

## Objective

Detect and contain Denial of Service attacks to maintain service availability and minimise disruption.

---

## Trigger

```bash
Network Traffic Threshold Exceeded
WAF Alert
Firewall Alert
DDoS Protection Alert
SIEM Correlation Rule
```

---

## Automated Investigation

### Step 1: Gather Network Information

```bash
Source IP Addresses
Destination Systems
Attack Volume
Protocol Information
Connection Statistics
```

### Step 2: Threat Intelligence Enrichment

```bash
Check Source IP Reputation
Check Known Botnet Activity
Review Historical Attacks
```

### Step 3: Impact Assessment

```bash
Identify Affected Systems
Determine Business Impact
Review Service Availability
```

---

## Decision Logic

```bash
IF Traffic Volume > Threshold
THEN Initiate Containment

IF Critical Assets Impacted
THEN Escalate Immediately
```

---

## Automated Response

```bash
Block Malicious IPs
Apply Rate Limiting
Update Firewall Rules
Enable DDoS Protection Policies
Create Incident Ticket
```

---

## Escalation Criteria

```bash
Critical Service Outage
Web Application Unavailable
Attack Persists Beyond Threshold
Multiple Systems Impacted
```

---

## Workflow

```bash
DoS Alert
      ↓
Collect Traffic Data
      ↓
Threat Intelligence Lookup
      ↓
Assess Impact
      ↓
Apply Rate Limiting
      ↓
Block Malicious Sources
      ↓
Notify Response Team
      ↓
Create Incident Record
```

---

# 3. Brute Force Attack Playbook

## Objective

Identify repeated authentication failures and prevent account compromise.

---

## Trigger

```bash
Multiple Failed Login Attempts
VPN Alert
Active Directory Alert
Identity Protection Alert
SIEM Detection Rule
```

---

## Automated Investigation

### Step 1: Collect Authentication Data

```bash
Username
Source IP
Timestamp
Failed Login Count
Target System
```

### Step 2: Threat Intelligence Checks

```bash
IP Reputation
Geolocation Lookup
Blacklist Verification
Known Threat Actor Activity
```

### Step 3: User Context

```bash
Previous Login History
Account Privileges
MFA Status
Recent Password Changes
```

---

## Decision Logic

```bash
IF Failed Attempts > 10
THEN Generate High Severity Alert

IF Source IP Reputation = Malicious
THEN Escalate Severity
```

---

## Automated Response

```bash
Temporarily Lock Account
Block Source IP
Force Password Reset
Notify User
Create Security Ticket
```

---

## Escalation Criteria

```bash
Privileged Account Targeted
Successful Login After Failures
Multiple Accounts Targeted
External Source Confirmed
```

---

## Workflow

```bash
Authentication Alert
         ↓
Collect Login Data
         ↓
Check IP Reputation
         ↓
Review User Activity
         ↓
Assess Risk
         ↓
Lock Account
         ↓
Block Source IP
         ↓
Notify User
         ↓
Open Incident
```

---

# 4. Suspicious PowerShell Activity Playbook

## Objective

Detect potentially malicious PowerShell execution commonly associated with malware, lateral movement, persistence, or post-exploitation activities.

---

## Trigger

```bash
EDR Detection
Sysmon Alert
Microsoft Defender Alert
PowerShell Logging Event
SIEM Correlation Rule
```

---

## Automated Investigation

### Step 1: Collect PowerShell Data

```bash
Command Line
Executed Script
Username
Hostname
Execution Time
Process Tree
```

### Step 2: Behaviour Analysis

```bash
Encoded Commands
Network Connections
Download Activity
Credential Access Attempts
Registry Changes
```

### Step 3: Threat Intelligence Checks

```bash
Hash Reputation
URL Reputation
IP Reputation
MITRE ATT&CK Mapping
```

---

## Context Gathering

```bash
User Role
Asset Criticality
Previous Alerts
Associated Processes
Affected Systems
```

---

## Decision Logic

```bash
IF Encoded PowerShell Detected
THEN Increase Severity

IF External Download Detected
THEN Escalate Incident

IF Known Malicious Behaviour Detected
THEN Initiate Containment
```

---

## Automated Response

```bash
Terminate PowerShell Process
Isolate Endpoint
Block Malicious IP
Block Downloaded Hash
Create Incident Ticket
Notify SOC Team
```

---

## Escalation Criteria

```bash
Credential Dumping Detected
Persistence Mechanisms Found
Lateral Movement Identified
Privileged User Involved
```

---

## Workflow

```bash
PowerShell Alert
         ↓
Collect Script Details
         ↓
Analyse Commands
         ↓
Check Threat Intelligence
         ↓
Assess Severity
         ↓
Terminate Process
         ↓
Isolate Endpoint
         ↓
Create Ticket
         ↓
Escalate if Required
```

---

# Complete SOAR Incident Flow

```bash
Alert Generated
       ↓
Data Collection
       ↓
Threat Intelligence Enrichment
       ↓
Context Gathering
       ↓
Risk Assessment
       ↓
Decision Logic
       ↓
Automated Response
       ↓
Ticket Creation
       ↓
Escalation
       ↓
Documentation
       ↓
Closure
```

---

# Key Takeaways

```bash
✓ Phishing playbooks focus on email containment and user protection
✓ DoS playbooks focus on maintaining availability and blocking attack traffic
✓ Brute force playbooks focus on account protection and authentication monitoring
✓ PowerShell playbooks focus on endpoint protection and malicious script detection
✓ All playbooks should include investigation, enrichment, containment, escalation, and documentation steps
✓ Human validation should be included for high-impact response actions
```
