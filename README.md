# TASK Research Academy: Digital Infrastructure & CRM Overhaul
**End-to-End Business Systems Analysis: Website Modernization, Conversational AI Chatbot & Greenfield HubSpot CRM Architecture**

---

## 📌 Executive Summary

TASK Research Academy underwent a complete digital transformation to modernize its online presence, capture high-intent inquiries, and centralize commercial pipeline operations. Acting as the Lead Business Systems Analyst, I scoped, architected, and executed a multi-phase systems overhaul:

1. **Website UI/UX & Lead Engine Modernization:** Scoped functional requirements and optimized lead capture touchpoints for prospective students and institutional partners.
2. **Conversational AI Chatbot Integration:** Designed decision tree branching and intent triage workflows for a 24/7 automated lead qualification widget.
3. **Greenfield HubSpot CRM Implementation:** Built the master Data Dictionary, custom contact/company properties, lifecycle stage transitions, and automated routing rules from scratch.

---

## 🛠️ System Architecture & Automated Lead Flow

```mermaid
flowchart TD
    subgraph USER ["User / Visitor"]
        A1([Land on Website]) --> A2{Select Engagement Path}
        A2 -->|Fill Form| A3[Submit Web Contact Form]
        A2 -->|Open Chat| A4[Interact with AI Chatbot]
        A5[Receive Booking Link] --> A6[Book Advisory Consultation]
    end

    subgraph GATEWAY ["Chatbot & Web Gateway"]
        A3 --> B1[Capture Form Payload]
        A4 --> B2[Bot Intent Triage & Qualification]
        B1 --> B3{Field Validation Pass?}
        B2 --> B4{Meets Qualification Criteria?}
        
        B3 -->|Yes| B5[Set Status: Qualified MQL]
        B3 -->|No| B6[Display Form Error] --> A3
        B4 -->|Yes| B5
        B4 -->|No / Dropped| B7[Set Status: Unqualified Lead]
        B5 --> A5
    end

    subgraph HUBSPOT ["HubSpot CRM & Sales Team"]
        B5 --> C1[Ingest Lead via Webhook]
        B7 --> C1
        C1 --> C2{Duplicate Email Check}
        C2 -->|Duplicate Exists| C3[Merge & Update Existing Contact]
        C2 -->|New Email| C4[Create New Contact Record]
        C3 --> C5{Lifecycle Stage Check}
        C4 --> C5
        C5 -->|Qualified MQL| C6[Set Lifecycle = MQL & Assign Sales Task]
        C5 -->|Unqualified Lead| C7[Enroll in Lead Nurture Workflow]
        C6 --> C8[Trigger Rep SLA Alert]
    end

    style USER fill:#f9f9f9,stroke:#333,stroke-width:1px
    style GATEWAY fill:#e1f5fe,stroke:#0288d1,stroke-width:1px
    style HUBSPOT fill:#e8f5e9,stroke:#388e3c,stroke-width:1px
