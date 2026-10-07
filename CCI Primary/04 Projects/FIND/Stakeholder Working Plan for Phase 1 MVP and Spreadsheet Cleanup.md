
## Summary

Reframe the stakeholder conversation around one prerequisite: Phase 1 should not begin with model creation or import work until the spreadsheet has been cleaned into a reliable source file. The stakeholder’s main responsibility is to help convert the current spreadsheet from a useful reference document into an import-ready catalog.

Phase 1 should still target a searchable endowment inventory with review workflow, but the order changes:

1. define the Phase 1 data contract
2. clean and normalize the spreadsheet
3. split `Department/School` into separate fields before import
4. confirm final controlled vocabularies
5. build models and import process from the cleaned file

## Stakeholder Conversation Structure

### 1. Start with the revised framing

Explain that the MVP is still a searchable endowment catalog, but the first deliverable is a clean source dataset. The current spreadsheet is close enough to drive the system design, but not clean enough to import directly without creating bad data and weak models.

Use this language in the conversation:

- Phase 1 depends on a cleanup pass before build.
- We want to define the real data structure from the spreadsheet, not force the application to inherit spreadsheet inconsistencies.
- If we clean now, the models, filters, and import process will be simpler and more accurate.

### 2. Align on the Phase 1 outcome

Confirm that Phase 1 should deliver:

- a searchable endowment inventory
- separate `School` and `Department` fields from day one
- normalized classifications and purpose categories
- manual review workflow
- clean importable records with source traceability

State that Phase 1 will not include:

- OCR
- AI extraction
- finance integration
- transaction history
- automated recommendations
- document parsing

### 3. Use the spreadsheet findings to focus the discussion

Present the main data issues plainly:

- `Department/School` is currently mixed and must be separated before import
- several lookup-like fields contain spelling, casing, and synonym variants
- some columns appear unused or unreliable
- `Specific Purpose` is high-cardinality free text and should remain text
- review workflow fields do not exist in the spreadsheet and will need to be created in the application

## Phase 1 Product Scope

### Included

- endowment list and detail pages
- search by title, endowment number, school, department, classification, and purpose-related fields
- normalized lookup-backed fields for classification and purpose categories
- free-text purpose and notes fields
- review status, reviewer, date, and comments
- import pipeline from one approved cleaned spreadsheet

### Explicit model direction for Phase 1

Build the data structure assuming these concepts exist in the cleaned file:

- `Endowment`
- `School`
- `Department`
- `Classification`
- `GeneralPurposeCategory`
- `Review`

Keep `Specific Purpose`, `Suggested Use`, and `Prior Usage` as text fields rather than forcing them into premature lookup tables.

## Stakeholder Action Items Before Build

These are the actions the stakeholder should complete or validate during the cleanup phase.

### 1. Approve the canonical columns for the cleaned spreadsheet

The stakeholder should help finalize one import-ready worksheet with these columns:

- `endowment_number`
- `title`
- `source_entered_date`
- `principal_account`
- `school`
- `department`
- `administrator_raw`
- `administrator_clean`
- `dean_classification_raw`
- `dean_classification_clean`
- `general_purpose_raw`
- `general_purpose_clean`
- `specific_purpose`
- `current_suggested_use_raw`
- `current_suggested_use_clean`
- `prior_usage`
- `import_notes`
- `data_issue_flag`
- `source_row_number`

Action item:

- confirm which of these columns are truly required for every record
- identify any additional fields that must exist for business use on day one

### 2. Split `Department/School` for every row

This should happen before import, not later in the app.

Action items:

- review every `Department/School` value and assign a separate `school`
- assign a separate `department`
- flag rows where the current value is really a program, initiative, project, or support note rather than a department
- decide how to handle records that belong only to a school and not a department
- decide whether cross-school or cross-department records need a primary owner rule for Phase 1

Required outcome:

- no imported record should rely on a combined `Department/School` field

### 3. Normalize controlled vocabulary fields

Action items:

- review all raw `Dean's Classification` values and approve one canonical version for each
- review all raw `General Purpose` values and approve one canonical version for each
- review low-volume `Current Suggested Use` values and decide whether they should be normalized or left as raw text
- identify values that are typos, duplicates, or synonyms

Examples from the current data that need decisions:

- `Cliinical Innovation` vs `Clinical Innovation`
- `Commity Care` vs `Community Care`
- `Community care` vs `Community Care`
- `Unkown` and `unkown`
- `Research & Education` vs `Research and Education`

Required outcome:

- each raw value maps to one approved clean value

### 4. Resolve ambiguous ownership and responsibility fields

Some source fields do not yet look trustworthy enough to use directly.

Action items:

- confirm whether `Administrator` is meaningful ownership data or just a placeholder/source artifact
- decide whether Phase 1 needs a true business owner field separate from administrator
- identify whether school, department, or another role is the primary accountable owner for each endowment
- flag rows where ownership is unknown

Required outcome:

- either approve a usable owner field or defer owner-based workflows from Phase 1

### 5. Review duplicate and questionable records

The stakeholder should validate records that may be duplicates or may not belong in the core inventory as modeled endowments.

Action items:

- review duplicate titles such as `Pharmacy`
- identify whether holding accounts should be imported as endowments, tagged separately, or excluded
- identify whether quasi-endowed or temporary structures belong in the same Phase 1 catalog
- flag records that are inactive, obsolete, transferred, or no longer relevant
- confirm whether any rows should be excluded from import entirely

Required outcome:

- every row is marked `import`, `exclude`, or `needs business decision`

### 6. Confirm date and status semantics

The spreadsheet does not appear to contain all business-ready lifecycle fields.

Action items:

- confirm whether `Entered` should be stored as a visible field or treated only as source metadata
- identify whether another source exists for established date
- identify whether another source exists for active/inactive status
- if no source exists, decide whether status should be omitted from Phase 1 or added manually during cleanup

Required outcome:

- no date or status field is imported with unclear meaning

### 7. Add explicit cleanup flags to the spreadsheet

The stakeholder should use a working column to track unresolved issues during cleanup.

Recommended values for `data_issue_flag`:

- `ready`
- `needs school/department split`
- `needs normalization`
- `needs owner decision`
- `possible duplicate`
- `exclude`
- `needs stakeholder review`

Required outcome:

- every row has a visible readiness state before import begins

## Revised Phase 2 and Phase 3 Overview

### Potential Phase 2

Only after the cleaned catalog and review workflow are working:

- document attachment and gift agreement tracking
- bulk updates and analyst work queues
- audit trail and change history
- improved ownership model with school/department/division hierarchies
- refresh import tools for revised spreadsheets

### Potential Phase 3

Only after the data model and operational workflow are stable:

- OCR and document extraction
- AI-assisted classification or summarization
- Banner/PeopleSoft or finance integrations
- transaction and spending history
- recommendation support and advanced reporting

## Acceptance Criteria for Cleanup Completion

The spreadsheet is ready for model design and import only when:

- every imported row has a valid `endowment_number` or an approved exception rule
- `school` and `department` are split into separate columns for all retained rows
- classification and general purpose fields have approved canonical values
- duplicate and questionable records are resolved or flagged for exclusion
- all rows have an import readiness flag
- all required Phase 1 fields are present and semantically understood
- one final cleaned worksheet is approved as the import source of truth

## Assumptions and Defaults

- The stakeholder, not the application team, is the business owner of source-data cleanup decisions.
- Phase 1 should model `School` and `Department` separately from the start.
- Cleanup should happen in the spreadsheet before import rather than being deferred into application logic.
- The application should preserve raw source values where useful, but it should be built around approved cleaned values.
- `Specific Purpose` remains free text in Phase 1.
- Review statuses will be created in the system, not imported from the spreadsheet.