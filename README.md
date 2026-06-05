# AWS CLOUDTRAIL INCIDENT INVESTIGATION 

## Document Information

**Project Title:** AWS CloudTrail Incident Investigation & Threat Hunting
**Prepared By:** Mohamed Ibrahim Shire
**Role:** SOC Analyst / Cloud Security Analyst
**Environment:** AWS Free Tier Laboratory
**Log Source:** AWS CloudTrail
**Classification:** Internal Use Only
**Report Version:** 1.0
**Investigation Date:** June 2026

---

# Executive Summary

This investigation analyzed suspicious activity generated within an AWS environment and recorded by AWS CloudTrail. The objective was to identify potentially malicious actions, reconstruct the attack timeline, determine the impact, and provide remediation recommendations.

CloudTrail logs revealed successful console authentication, resource discovery activity, CloudTrail enumeration, IAM reconnaissance, S3 inspection attempts, and multiple unauthorized actions that resulted in Access Denied responses. The activity closely resembles the reconnaissance and privilege validation phases commonly observed during cloud-focused attacks.

The investigation successfully identified the source user, reconstructed the sequence of events, and verified that no critical AWS resources were successfully modified or destroyed.

---

# Investigation Objectives

The primary objectives of this investigation were:

* Detect suspicious AWS account activity.
* Analyze CloudTrail event logs.
* Identify attacker behavior.
* Determine affected AWS services.
* Build a complete attack timeline.
* Assess business impact.
* Recommend containment and remediation actions.

---

# Environment Overview

## AWS Services Used

* AWS CloudTrail
* AWS Identity and Access Management (IAM)
* Amazon S3
* AWS Management Console

## Logging Configuration

CloudTrail was configured to capture:

* Management Events
* Read Events
* Write Events
* Multi-Region Activity

The generated logs served as the primary source of evidence throughout the investigation.

---

# Incident Overview

## Alert Description

CloudTrail recorded multiple activities performed by a user account exhibiting reconnaissance and administrative exploration behavior.

Observed actions included:

* Console authentication
* IAM enumeration
* S3 bucket inspection
* CloudTrail inspection
* Administrative action attempts
* Access Denied events

The activity pattern was indicative of a user attempting to understand the cloud environment and validate available privileges.

---

# MITRE ATT&CK Mapping

| Tactic            | Technique                   | ID    |
| ----------------- | --------------------------- | ----- |
| Initial Access    | Valid Accounts              | T1078 |
| Discovery         | Cloud Service Discovery     | T1526 |
| Discovery         | Permission Groups Discovery | T1069 |
| Discovery         | Account Discovery           | T1087 |
| Defense Evasion   | Indicator Removal Attempts  | T1070 |
| Credential Access | Cloud Account Enumeration   | T1087 |

---

# Evidence Collection

## Evidence Sources

### Source 1

<img width="794" height="222" alt="history event1" src="https://github.com/user-attachments/assets/23da2f8f-dc46-44ab-afe0-8d0f4a17d067" />
<img width="788" height="207" alt="history event" src="https://github.com/user-attachments/assets/3aec64a6-4d27-4791-8769-7d24323bc8a7" />
<img width="754" height="118" alt="trail" src="https://github.com/user-attachments/assets/bef772ee-ac7a-42a7-8c58-b853a9eb2966" />

### Source 2

CloudTrail Event JSON Details

### Source 3

<img width="722" height="174" alt="IAM" src="https://github.com/user-attachments/assets/98b42e3a-b940-4276-89ce-a62d7fdb0039" />

### Source 4

CloudTrail Configuration Screenshots

### Source 5

<img width="755" height="224" alt="s3 access denied" src="https://github.com/user-attachments/assets/2139e192-1724-404a-b6a0-ec3766b15f20" />
<img width="922" height="297" alt="att denied to create s3" src="https://github.com/user-attachments/assets/83caeb8e-e73a-4ea9-8e5a-4d3c20d082f4" />
<img width="752" height="245" alt="decribe trail denied" src="https://github.com/user-attachments/assets/d0d9ac60-4972-4e9f-bb29-7d90314cb841" />

### Source 6

Timeline Documentation

---

# Investigation Findings

## Finding 1: Successful Console Authentication

CloudTrail recorded successful AWS Management Console access.

### Significance

Successful authentication confirms valid credentials were used to access the AWS environment.

### Risk Level

Medium

---

## Finding 2: IAM Reconnaissance Activity

The actor accessed IAM-related resources and attempted to enumerate users and permissions.

### Significance

This behavior commonly occurs during the discovery phase of an attack.

### Risk Level

Medium

---

## Finding 3: S3 Enumeration

The user attempted to identify available S3 resources.

### Significance

Attackers frequently enumerate storage resources searching for sensitive data.

### Risk Level

Medium

---

## Finding 4: CloudTrail Enumeration

The actor inspected CloudTrail configuration settings.

### Significance

Adversaries often investigate logging systems to understand detection capabilities.

### Risk Level

High

---

## Finding 5: Access Denied Events

Several actions generated Access Denied responses.

### Significance

These events demonstrate attempts to perform actions beyond the user's assigned privileges.

### Risk Level

High

---

# Attack Timeline

| Time  | Event                            |
| ----- | -------------------------------- |
| 10:01 | Successful Console Login         |
| 10:02 | IAM Enumeration                  |
| 10:03 | User Discovery                   |
| 10:04 | S3 Resource Enumeration          |
| 10:05 | CloudTrail Inspection            |
| 10:06 | Administrative Action Attempt    |
| 10:07 | Access Denied Response           |
| 10:08 | Additional Validation Activities |
| 10:09 | Session End                      |

---

# Indicators of Compromise (IOCs)

## User Account

Attacker-user

## Log Source

AWS CloudTrail

## Event Types

* ConsoleLogin
* ListUsers
* GetUser
* ListBuckets
* DescribeTrails
* AccessDenied

## Investigation Indicators

* Repeated resource enumeration
* Unauthorized administrative actions
* Logging infrastructure inspection
* Privilege validation attempts

---

# Root Cause Analysis

The investigation determined that a valid AWS user account was used to access the environment.

The account possessed limited permissions and was unable to perform privileged administrative operations.

Although the actor attempted to interact with sensitive AWS services, existing IAM controls prevented successful privilege escalation.

---

# Impact Assessment

## Confidentiality

No evidence of data exposure.

Impact: Low

## Integrity

No evidence of resource modification.

Impact: Low

## Availability

No evidence of service disruption.

Impact: Low

## Overall Severity

Medium

---

# Detection Opportunities

SOC teams should create alerts for:

### CloudTrail Monitoring Rules

* Console Login Activity
* Multiple Access Denied Events
* IAM Enumeration Activity
* CloudTrail Modification Attempts
* New IAM User Creation
* IAM Policy Changes
* S3 Enumeration Activity

---

# Containment Actions

Recommended actions include:

1. Review IAM permissions.
2. Rotate user credentials.
3. Enable MFA.
4. Investigate unusual CloudTrail events.
5. Restrict unnecessary privileges.
6. Monitor CloudTrail continuously.

---

# Lessons Learned

The investigation demonstrated the importance of:

* Centralized logging
* CloudTrail monitoring
* Least privilege access
* IAM governance
* Cloud security visibility

---

# Final Assessment

The activity observed during this investigation reflects a realistic cloud attack scenario involving authentication, reconnaissance, permission validation, and logging awareness.

CloudTrail successfully captured all critical actions required for investigation and incident reconstruction.

No evidence of successful privilege escalation or resource destruction was identified.

The environment's IAM controls effectively limited attacker capabilities and reduced overall impact.

---



