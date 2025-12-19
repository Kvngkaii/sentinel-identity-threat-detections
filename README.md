# Microsoft Sentinel SIEM – Identity Threat Detection Lab

## Overview
This project demonstrates the deployment and configuration of Microsoft Sentinel to detect and investigate identity-based attacks using Microsoft Entra ID (Azure AD) sign-in and audit logs.

Custom KQL analytics rules were created to identify suspicious authentication behavior, generate alerts, and automatically create security incidents for investigation. The lab simulates a real-world Security Operations Center (SOC) workflow focused on identity-based threat detection and incident response.

---

## Project Objectives
- Ingest Microsoft Entra ID (Azure AD) logs into Microsoft Sentinel
- Detect identity-based attacks using Kusto Query Language (KQL)
- Create scheduled analytics rules
- Generate alerts and security incidents
- Demonstrate a SOC-style investigation workflow

---

## Tools and Technologies Used
- Microsoft Sentinel (SIEM)
- Microsoft Entra ID (Azure AD)
- Log Analytics Workspace
- Kusto Query Language (KQL)
- Microsoft Defender Portal
- MITRE ATT&CK Framework

---

## Architecture Overview
Microsoft Entra ID authentication events are forwarded to a Log Analytics Workspace using the native Microsoft Sentinel data connector. Microsoft Sentinel continuously analyzes these logs using scheduled analytics rules written in KQL. When suspicious authentication behavior is detected, alerts are generated and grouped into security incidents for investigation by a SOC analyst.

Add screenshot: Sentinel architecture or data flow diagram

---

## Step 1: Log Ingestion Configuration (Microsoft Entra ID)
Microsoft Entra ID was integrated with Microsoft Sentinel using the built-in data connector. This allowed authentication and audit events to be streamed into a Log Analytics Workspace for centralized analysis.

Actions performed:
- Navigated to Microsoft Sentinel > Data connectors
- Selected the Microsoft Entra ID (Azure AD) data connector
- Enabled ingestion for sign-in logs and audit logs
- Verified permissions were granted for log collection
- Confirmed logs were successfully sent to the Log Analytics Workspace

Validation was performed by running KQL queries against the `SigninLogs` and `AuditLogs` tables to ensure data was actively ingesting.

Add screenshot: Entra ID data connector enabled  
Add screenshot: Log Analytics Workspace showing SigninLogs data

---

## Step 2: KQL-Based Threat Detection Queries
Custom KQL queries were developed to detect suspicious identity activity. The primary focus of this lab was identifying brute-force authentication attempts against Entra ID user accounts.

Detection logic included:
- Multiple failed sign-in attempts within a short time window
- Repeated authentication failures originating from the same IP address
- Targeting of a single user account across many attempts

These queries were tested directly in Log Analytics to confirm accurate results before being used in analytics rules.

Add screenshot: KQL query editor showing brute-force detection query  
Add screenshot: Query results showing failed sign-in activity

---

## Step 3: Analytics Rule Creation
Scheduled analytics rules were created in Microsoft Sentinel using the custom KQL queries. These rules continuously monitor incoming authentication logs and automatically generate alerts when detection thresholds are met.

Analytics rule configuration included:
- Scheduled query execution interval
- Lookup period for historical sign-in activity
- Thresholds based on failed authentication count
- Automatic creation of security incidents
- Entity mapping for user accounts and IP addresses
- MITRE ATT&CK tactic and technique classification

MITRE ATT&CK Mapping:
- Tactic: Credential Access
- Technique: Brute Force (T1110)

Add screenshot: Analytics rule configuration settings  
Add screenshot: MITRE ATT&CK mapping section

---

## Step 4: Alert and Incident Generation
When the analytics rule detected suspicious authentication behavior, Microsoft Sentinel generated alerts and grouped them into security incidents. Each incident included relevant context to support investigation and triage.

Incident details included:
- Affected user accounts
- Source IP addresses
- Timestamps of authentication attempts
- Related alerts and entities
- Severity classification

Add screenshot: Alert details page  
Add screenshot: Incident overview dashboard

---

## Step 5: SOC-Style Investigation Workflow
Each generated incident was investigated using Microsoft Sentinel’s investigation tools and Entra ID sign-in logs. The investigation process followed standard SOC procedures to validate the alert and assess potential impact.

Investigation steps:
- Reviewed incident timeline to understand activity sequence
- Analyzed failed and successful sign-in attempts
- Identified source IP addresses and geographic locations
- Determined whether activity matched brute-force behavior
- Assessed whether the alert represented a true positive

Add screenshot: Incident investigation graph  
Add screenshot: Sign-in log details for affected user

---

## Detection Results
This lab successfully generated alerts and incidents for simulated brute-force authentication attempts against Entra ID accounts.

Detected:
- Brute-force sign-in activity using failed authentication attempts

Configured but not triggered:
- Additional identity-based detection rules (no test logs generated)

This distinction is documented to reflect accurate testing conditions and realistic SOC validation practices.

---

## Lessons Learned
- Microsoft Sentinel provides strong native integration with Entra ID for identity monitoring
- KQL enables precise and customizable detection logic
- Proper tuning of detection thresholds is essential to minimize false positives
- Incident grouping improves investigation efficiency in a SOC environment
- Clear documentation of simulated versus observed detections improves reporting accuracy

---

## Future Enhancements
- Simulate additional identity attack scenarios such as impossible travel and MFA fatigue
- Implement automated response playbooks using Logic Apps
- Expand detections using UEBA analytics
- Create dashboards focused on identity risk and authentication trends

---

## References
- Microsoft Sentinel Documentation
- Microsoft Entra ID Sign-In Logs Documentation
- MITRE ATT&CK Framework

