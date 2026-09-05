# Conversational AI Chatbot Architecture
**System:** TASK AI Advisor Widget  
**Author:** Alvin Ngwerume (Lead Business Systems Analyst)  

---

## 1. Intent Mapping & Qualification Tree

```text
[Start: User Opens Chatbot]
  │
  ├── Intent A: "Academic Programs & Admissions"
  │     ├── Collect: Full Name, Email, Target Field
  │     ├── Branch: Select Qualification Level (Undergrad / Postgrad / Professional)
  │     └── Action: Set `inquiry_type` = "Student" -> Route to Admissions Pipeline
  │
  ├── Intent B: "Institutional / Enterprise Partnerships"
  │     ├── Collect: Name, Work Email, Organization Name, Role
  │     ├── Branch: Select Engagement Scope (Research Collaboration / Enterprise Training)
  │     └── Action: Set `lifecycle_stage` = "MQL" -> Trigger High-Priority Rep SLA
  │
  └── Intent C: "General Support & FAQs"
        ├── Search: Knowledge Base Resolution
        └── Fallback: Submit Offline Ticket -> Create General HubSpot Contact Record
