# Automated Workflows & SLA Execution Blueprint

**Platform:** HubSpot CRM (Professional / Enterprise)  
**Author:** Alvin Ngwerume (Lead Business Systems Analyst)  
**Scope:** Automated Lead Routing, SLA Enforcement, and Cross-Platform Notification Engines  

## 1. Automation Architecture Overview

This document outlines the execution logic, trigger criteria, and action sequences for automated lead routing and Service Level Agreement (SLA) enforcement at TASK Research Academy. The automation engine bridges inbound web/chatbot capture endpoints with commercial outreach teams to eliminate manual lead friction and enforce a strict 15-minute response SLA.

## 2. Workflow 1: MQL Lead Routing & High-Priority SLA Assignment

### Workflow Specifications
* **Workflow Name:** `[Ops] Lead Routing & SLA Assignment - MQL Pending`
* **Object Type:** Contact-based
* **Execution Frequency:** Real-time (Instant Webhook & Form Event Processing)

### Step-by-Step Execution Logic

| Step | Action Type | System Target | Configuration & Rule Parameters |
| :--- | :--- | :--- | :--- |
| **01** | **Enrollment Trigger** | Contact Property | Filter: `qualification_status` is equal to `MQL_Pending` |
| **02** | **Owner Rotation** | Contact Property | Action: Assign Contact Owner via Round-Robin across active members of `Admissions Advisory Team` |
| **03** | **SLA Task Generation** | HubSpot Tasks | Action: Create high-priority task assigned to `Contact Owner`<br>• **Title:** `HIGH SLA: Conduct Discovery Outreach within 15 mins - [Contact First Name] [Contact Last Name]`<br>• **Due Date:** Immediately (+15 minutes)<br>• **Type:** Call / Prospecting |
| **04** | **Slack Notification** | Integrations / Slack | Action: Send automated payload to `#admissions-leads` channel |

### Slack Alert Payload Template
```text
🚨 *NEW MQL LEAD ASSIGNED* 🚨
*Name:* {{ contact.firstname }} {{ contact.lastname }}
*Inquiry Type:* {{ contact.inquiry_type }}
*Email:* {{ contact.email }}
*Assigned Owner:* {{ contact.hubspot_owner_id }}
*SLA Deadline:* 15 minutes from enrollment
*HubSpot Record:* [https://app.hubspot.com/contacts/ACCOUNT_ID/contact/](https://app.hubspot.com/contacts/ACCOUNT_ID/contact/){{ contact.hs_object_id }}
*Workflow 2: Automated Lead Deduplication & Contact EnrichmentWorkflow SpecificationsWorkflow Name: [Data Hygiene] Contact Deduplication & Source AttributionObject Type: Contact-basedExecution StepsTrigger: Contact created where email is known.Deduplication Check: Native HubSpot matching queries existing contact records by primary key (email).If Match Exists: Merge inbound form properties into target record, update last_modified_date, and append new inquiry details to conversion_events without overwriting historical source data.If New Contact: Set lifecycle_stage = Subscriber and set lead_source_detail based on touchpoint (e.g., Chatbot_Widget vs Web_Form_Main).
*Workflow 3: Re-Engagement & Stale Lead EscalationWorkflow SpecificationsWorkflow Name: [SLA Breach] Uncontacted Lead EscalationObject Type: Task & Contact AssociatedExecution StepsTrigger: qualification_status is equal to MQL_Pending AND last_engagement_date is more than 24 hours ago AND lifecycle_stage is NOT equal to Customer.Action 1: Send alert notification to Sales Manager / Team Lead.Action 2: Re-assign contact owner to secondary available advisor via backup pool.Action 3: Update qualification_status property to SLA_Breached_Reassigned.
*Quality Assurance & SLA Testing ProtocolTest CaseSimulated InputExpected OutputVerification PointTC-01Web form submission with inquiry_type = EnterpriseContact created, status = MQL_PendingHubSpot Contact ViewTC-02Trigger firing on MQL_PendingContact owner set via round-robinContact Audit HistoryTC-03Task creation within 15s of enrollmentHigh-priority task created due in 15 minsRep Task DashboardTC-04Slack integration webhookChannel message posted with dynamic tokens#admissions-leads Slack
