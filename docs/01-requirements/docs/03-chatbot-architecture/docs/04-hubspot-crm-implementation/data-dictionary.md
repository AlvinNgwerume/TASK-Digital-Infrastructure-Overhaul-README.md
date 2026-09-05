---

### File 3: `docs/04-hubspot-crm-implementation/data-dictionary.md`

```markdown
# Master Data Dictionary & CRM Schema
**Platform:** Greenfield HubSpot CRM Implementation  
**Author:** Alvin Ngwerume (Lead Business Systems Analyst)  

---

## 1. Contact Object Field Schema

| Property Name | Internal API Name | Field Type | Acceptable Values / Enumerations |
| :--- | :--- | :--- | :--- |
| First Name | `firstname` | Single-line text | Free text |
| Last Name | `lastname` | Single-line text | Free text |
| Email | `email` | Single-line text | Unique Identifier (Standard Email Syntax) |
| Inquiry Type | `inquiry_type` | Dropdown select | `Student`, `Institutional_Partner`, `Faculty`, `General` |
| Lifecycle Stage | `lifecyclestage` | Dropdown select | `Subscriber`, `Lead`, `Marketing Qualified Lead`, `Sales Qualified Lead`, `Customer` |
| Lead Source Detail | `lead_source_detail` | Single-line text | `Web_Form_Main`, `Chatbot_Widget`, `Direct_Advisory` |
| Qualification Status| `qualification_status` | Dropdown select | `Unqualified`, `MQL_Pending`, `SQL_Verified`, `Disqualified` |

---

## 2. Lifecycle Stage Transition Blueprint

```mermaid
stateDiagram-v2
    [*] --> Subscriber: Visitor Submits Web Form / Interacts with Chat
    Subscriber --> Lead: Contact Email Validated
    Lead --> MarketingQualifiedLead: Chatbot / Form Logic Meets Persona Criteria
    MarketingQualifiedLead --> SalesQualifiedLead: Advisory Team Accepts Lead & Conducts Discovery
    SalesQualifiedLead --> Opportunity: Program Proposal / Enterprise Scope Delivered
    Opportunity --> Customer: Contract Executed / Enrollment Finalized
