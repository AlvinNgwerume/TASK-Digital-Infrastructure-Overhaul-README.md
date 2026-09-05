# Business Requirements Document (BRD)
**Project Name:** TASK Research Academy Digital Infrastructure & Intake Overhaul  
**Author:** Alvin Ngwerume (Lead Business Systems Analyst)  
**Status:** Approved / Implemented  

---

## 1. Project Overview & Business Objectives
TASK Research Academy required a modern, scalable digital infrastructure to eliminate manual lead handling, improve prospect engagement, and establish a single source of truth for commercial operations.

* **Primary Objective:** Replace manual spreadsheet tracking with a greenfield HubSpot CRM architecture and automated intake engines.
* **Target Metric:** Improve lead processing efficiency by 25% and reduce lead response time from >24 hours to under 15 minutes.
* **Scope:** Website UI/UX modernization, dynamic lead form engineering, AI chatbot widget deployment, and HubSpot CRM schema setup.

---

## 2. Key Stakeholders & Personas
* **Executive Leadership:** Requires real-time visibility into top-of-funnel conversion rates and pipeline velocity.
* **Admissions & Advisory Reps:** Need clean, deduplicated, and pre-qualified leads assigned automatically with clear follow-up SLAs.
* **Prospective Students & Partners:** Expect immediate, personalized responses and seamless booking options 24/7.

---

## 3. Functional Requirements (FR)

| Requirement ID | Module | Description | Priority |
| :--- | :--- | :--- | :--- |
| **FR-101** | Web Intake | The web lead form must dynamically adapt fields based on user role (e.g., Student vs. Institutional Partner). | High |
| **FR-102** | AI Chatbot | The chatbot must triage incoming traffic, capture contact details, and qualify leads via interactive branching. | High |
| **FR-103** | CRM Ingestion | All validated form and chatbot submissions must instantly sync to HubSpot via API webhooks. | Critical |
| **FR-104** | Deduplication | The CRM must query existing records by `email` domain before creating new contact entities to prevent duplicates. | High |

---

## 4. Non-Functional Requirements (NFR)
* **NFR-201 (Performance):** Web forms and chatbot scripts must add less than 200ms to total page load time.
* **NFR-202 (Data Integrity):** Standardized input masks must enforce email syntax and phone number formatting across all entry points.
* **NFR-203 (Availability):** Chatbot qualification logic and CRM API webhooks must maintain 99.9% uptime.
