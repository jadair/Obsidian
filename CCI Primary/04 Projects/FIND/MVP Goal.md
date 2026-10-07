**Provide a centralized, searchable catalog of endowments with enough metadata to support manual analysis and future expansion.**

This application will initial server as a master inventory for endowment records and continue to evolve from there.

Drexel endowment made up of multiple endowments
these records are actual funds
- there could be endowed funds
- 
Endowments gifts of funds
- possible restrictions/no restrictions
---

### **1. What funds do we have?**

Simple searchable list.

```
Smith Endowment

Endowment #100342

School of Medicine

Research

Established 1986

Status: Active
```

---

### **2. Who owns it?**

Identify responsible department.

**Possible difference between how admin/finance handles orgs departments**
- Match departments with 
Example

```
Department

Pediatrics

Administrator

Jane Smith

School

Medicine
```

---

### **3. What is its stated purpose?**

Use existing spreadsheet fields.

General Purpose

Specific Purpose

Suggested Use

Prior Usage

This alone provides tremendous value.

---

### **4. What organizational area benefits?**

Instead of searching spreadsheets.

Examples

Search:

```
Pediatrics
```

Returns

- Smith Fund
- Jones Fund
- Wilson Scholarship

---

### **5. Has someone reviewed this fund?**

Simple workflow.

Status

- Not Reviewed
- Needs Review
- Reviewed
- Needs Gift Agreement
- Archived

This creates progress tracking immediately.

---

# **Leave These Out**

These belong in Phase 2 or 3.

❌ OCR

❌ AI

❌ PDF Parsing

❌ Finance Integration

❌ Banner/PeopleSoft

❌ Charge Recovery Engine

❌ Transaction Imports

❌ Spending History

---

# **Suggested Django Models**

Instead of 15 tables, I’d start with 5.

## **Fund**

Core information.

```
Endowment
----------
id
endowment_number
title
established_date
status
notes
```

---

## **Organization**

```
Organization
-------------
School
Department
Division
Administrator
```

One organization can own many endowments.

---

## **Classification**

This comes directly from your spreadsheet.

Examples

- Chair
- Scholarship
- Research
- Equipment
- Program Support

---

## **Fund Purpose**

```
General Purpose

Specific Purpose

Suggested Future Use

Prior Usage
```

Could remain one-to-one with Endowment initially.

---

## **Review**

Tracks project progress.

```
Reviewer

Review Date

Status

Comments

Confidence
```

---

# **Data Dictionary for MVP**

|**Field**|**Description**|**Required**|
|---|---|---|
|Endowment Number|Unique identifier|Yes|
|Title|Fund name|Yes|
|Established Date|Date created|No|
|School|Beneficiary school|Yes|
|Department|Department|Yes|
|Administrator|Responsible owner|No|
|Classification|Chair, Scholarship, etc.|Yes|
|General Purpose|Broad donor intent|Yes|
|Specific Purpose|Detailed description|Yes|
|Suggested Use|Proposed modern use|No|
|Prior Usage|Historical notes|No|
|Status|Active/Inactive|Yes|
|Review Status|Workflow|Yes|
|Reviewer|Person reviewing|No|
|Notes|Analyst comments|No|

---

# **User Stories**

This is where many MVPs become much clearer.

### **As a Finance employee**

I want to search all endowments

so I can quickly locate a fund.

---

### **As Development**

I want to browse endowments by department

so I understand what resources exist.

---

### **As an analyst**

I want to record review notes

so work isn’t duplicated.

---

### **As leadership**

I want dashboards showing

- number reviewed
- number remaining
- by school
- by department

so I can monitor project progress.

---

### **As a reviewer**

I want to flag funds requiring legal review

so they can be revisited later.

---

# **Nice-to-Have Features (Still MVP-Friendly)**


- Full-text search across titles and purpose descriptions
- Filter by school, department, classification, and review status
- Export filtered results to Excel or CSV
- Attach notes to an endowment
- Tag endowments with keywords (e.g., “Research”, “Faculty”, “Pediatrics”)
- Basic dashboard with counts by department, school, and review status
- Import and re-import the spreadsheet with duplicate detection

---

# **Roadmap**

| **Phase**   | **Goal**                                                                                                                 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| **Phase 1** | Searchable endowment repository, classifications, review workflow, dashboard, Excel import                               |
| **Phase 2** | Upload and associate gift agreements, document management, OCR, AI-assisted summaries, structured restriction extraction |
| **Phase 3** | Finance integration, charge categories, spending history, opportunity matching, reporting                                |
| **Phase 4** | Recommendation engine to identify eligible endowments for proposed expenses and quantify recovery opportunities          |

## ** Backend Architecture**

Finance data is not part of phase one but the initial design should incldue it to allow for implementation without disruption of existing data and logic.

```text
Endowment
├── Organization
├── Classification
├── Review
├── GiftAgreement (optional, Phase 2)
└── FinancialAccount (optional, Phase 3)
```




## Data Analysis
# Endowment MVP model inventory

Source: Sorted Updated _ FHT Classifications FY26 _stc.xlsx

Records analyzed from `Unitized Schedule`: 211

  

## Endowment

- Candidate endowment records: 211

- Unique titles: 210

- Duplicate titles: {'Pharmacy': 2}

  

## Organization

- Principal account values (9):

- 530501

- 530501/598601

- 530501/598607

- 530501/598609

- 530501/598610

- 530501/598612

- 530501/598614

- 530501/598616

- 530501/598619

- Administrators (1):

- Jeff Eberly

- Department/School raw unique values (43):

- 11th Street Corridor

- 11th Street Corridor/Program renovation support initiatives

- Bariactric Center Support

- CHOP

- CME Program Development and Restructuring

- Cardiology [department support]

- Clinical Trial Research Group

- Clinical Trial Research Pharmacist

- Community Health Initiatives

- Cover Brodsky support

- Employee Health Services

- Gastroenterology initiatives

- Graduate Hospital

- Healing Garden

- Library upgrades for LCME

- Nanotechnolgy - Collaboration with Drexel and Penn

- Orthopedics/gait lab support

- Outpatient Clinic Care - Ob/Gyn, Psychiatry and Medicine

- PHD Student Stipends

- Pediatric Initiatives

- Pediatric initiatives

- Pediatric initiatives - hearingpaired

- Program renovation support initiatives

- Pulmonology-related initiatives

- Purchase ECHO Machines

- Purchase Electron Microscope for Pathology Department

- Purchase Ultrasound reporting software

- Purchased Stroboscope, EMG and Scopes in ENT

- Recruitment Support for Gyn oncology group

- Recruitment support for Dr. Wigdahl

- Renovations for Infusion Center

- Renovations to Student Lounges

- Renovations to gatehouse for Inst for Women's Health

- School of Public Health Grand Rounds

- Support Chair Package for Surgery related to research commitments

- Support Chair Package for surgery related to research commitment

- Support Department of Neurology

- Support Department of Radiation Oncology

- Support Kidney transplant program

- Support Office of Educational Affairs related to requirements to met LCME

- Support for College of Nursing and Health Professions

- TBD

- Urology Department Support

  

## Classification

- Dean's Classification raw unique values (9):

- Cliinical Innovation

- Clinical Innovation

- Commity Care

- Community Care

- Community Care - Peds

- Community care

- Facutly Excellence

- Research and Innovation

- Student Experience

- General Purpose raw unique values (25):

- Awards & Scholarships

- CME Program Development and Restructuring

- Community Health Initiatives

- Community Programs

- Department Chair at Graduate Hospital

- Education

- Equipment

- Free Care

- General Purpose

- Holding Account

- Indigent Care

- NonMedical Services

- Outpatient Clinic Care - Ob/Gyn, Psychiatry and Medicine

- Pediatric initiatives

- Pediatric initiatives - hearingpaired

- Physical Plant

- Physical Plant & Equipment

- Prov of Non Med Serv

- Research

- Research & Education

- Research and Education

- Scholarship

- Unkown

- Various Directives

- unkown

  

## EndowmentPurpose

- Specific Purpose unique values: 174 (recommend free text)

- Current Suggested Use raw unique values (16):

- ?

- Asif Ilyas

- COM Capital

- Clinical Services

- Clinical Services (?)

- Clinical services

- Clinical services; no longer Graduate Hospital

- Cuthbert

- Faculty Affairs/Faculty development

- Faculty development CME

- Meera Harhay support

- Microbiology/Immunology Research

- PCCP/GIM

- Pediatrics

- Research

- Surgical animal facilities expenses at Cuthbert/Asif Ilyas

- Prior Usage raw unique values (3):

- A Sanz-Clemente Recruitment Package

- HSB

- Jenna Hope Recruitment Package

  

## Review

- No review/workflow columns exist in the spreadsheet.

- Recommended seed statuses from the MVP note:

- Not Reviewed

- Needs Review

- Reviewed

- Needs Gift Agreement

- Archived

  

## Normalization candidates

- Dean's Classification:

- Cliinical Innovation -> Clinical Innovation

- Commity Care -> Community Care

- Community care -> Community Care

- Facutly Excellence -> Faculty Excellence

- General Purpose:

- unkown -> Unknown

- Unkown -> Unknown

- Research & Education -> Research and Education

- Department/School:

- Pediatric Initiatives -> Pediatric initiatives

- Support Chair Package for surgery related to research commitment -> Support Chair Package for Surgery related to research commitments

- Current Suggested Use:

- Clinical services -> Clinical Services

- Clinical Services (?) -> Clinical Services