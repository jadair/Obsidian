Below is the stakeholder change list translated into implementation action items against the current proposal create flow.

**Form Changes**
1. Replace the current `CCI Lead` source with a maintained roster of all CCI/SCIS faculty and possibly post-docs; confirm whether post-docs are included and define the annual roster update process.
2. Add a required `Department/Org` field near `CCI Lead`; decide whether this is user-entered, selected from org data, or auto-derived from the selected lead.
3. Replace the current proposal type options with:
   - `Pre-proposal`
   - `New`
   - `Resubmission`
   - `Subcontract`
   - `Other`
4. Add conditional behavior for `Other` proposal type with a required free-text description field.
5. Fix proposal type defaulting so `New` is available and the form does not incorrectly default to `LOI`.
6. For `Resubmission`, add a conditional field for `COEUS #` or replacement `proposal ID`; confirm which identifier should be used going forward.
7. For `Subcontract`, relabel the sponsor block to `Lead Institution` and expand it to capture institution, PI, and contact information explicitly.
8. Keep `Prime Sponsor`, but clarify that it is the funding agency/source category and decide whether this should remain free text or become a controlled sponsor/agency lookup.
9. Replace the current solicitation block with:
   - `Solicitation URL`
   - `Solicitation Title`
   - remove file upload entirely
10. Evaluate whether `Solicitation URL` should auto-generate a short solicitation label for reporting, and define the generation rules if yes.
11. Remove the `Is this an open deadline?` field entirely.
12. Replace or supplement `Solicitation Deadline` with a required `Solicitation Deadline` plus an optional `Target Submission Date if different`; confirm whether both dates should remain or whether target date fully replaces deadline in the request form.
13. Make `Project Title` required.
14. Make both `Start Date` and `End Date` required; current form treats them as optional.
15. Rename `Funding Amount Requested` to `Estimated Drexel Budget` and enforce whole numbers if that is the desired format.
16. Decide whether `Project Description` should be labeled `Abstract` or `Description` and whether there is a character limit.
17. Determine whether keywords should be generated automatically for reporting and, if so, define the generation method and storage field.

**Checklist / Notification Changes**
18. Convert the current yes/no radio sections into explicit checkbox-style questions if that is the desired UX.
19. Update the equipment question text to `Does this proposal include major equipment (individual item > $5k)?`
20. Keep the conditional equipment description field when equipment is included.
21. Keep the subcontract question, but update the conditional subcontractor fields to capture `Institution Name`, `Investigator Name`, and `Contact Information`.
22. Keep the internal review question, but confirm whether selecting it should trigger additional email recipients or workflow routing.
23. Implement the stakeholder requirement that “if yes include in email notification” for the applicable checklist items; define exactly which yes-values alter notifications.

**Project Team Changes**
24. Rename `CCI Team Members` to `CCI (SCIS) Team`.
25. Keep the required CCI team rows with `Name`, `Role`, and `Dept/Org`.
26. Restrict CCI team roles to the stakeholder-specified set: `PI`, `Co-PI`, `Senior Personnel`; confirm whether any current roles should remain available.
27. For `Other Drexel`, define the data source for person lookup; current form uses free text for name and org select for org.
28. For `Other Drexel`, define the source for `Dept/Org`; decide whether it should be a searchable directory-backed select or manual entry.
29. Redefine `External Collaborators` rows to include:
   - `Institution`
   - `Name`
   - `Role`
   - `Lead Institution` checkbox
30. Remove the current external collaborator contact-email-centric structure unless email is still needed in addition to the new fields.

**Proposal Record / Data Model Changes**
31. Add proposal record fields for:
   - `COEUS # / proposal ID`
   - `Date submitted to Prime Sponsor`
   - `Date submitted to Lead Institution` for subcontracts
   - `Sponsor Type`
   - `Total Project Budget`
   - `Total CCI/SCIS Budget`
32. Expand status handling to support the stakeholder workflow states:
   - `Created`
   - `Assigned`
   - `Submitted`
   - `Not submitted`
   - `Declined`
   - `Awarded`
33. Add support for assignment metadata, including assigned staff names.
34. For `Awarded`, add a conditional `Grant Fund Number` field.
35. Decide whether `owning_org` should remain in the data model and UI; stakeholder explicitly questioned its continued value.
36. Keep `PhD student count` only if stakeholders confirm it is still needed.
37. Add a per-investigator budget field for Drexel team members.
38. Decide whether external collaborators should contribute to total project budget calculations and reporting.
39. Remove deprecated fields from the recreated form and, if appropriate, from downstream record displays:
   - `Credit split`
   - `Tuition Exemption`
   - `IDC rate`
   - `Total awarded to CCI`

**Backend / API / Reporting Work**
40. Redesign the create API contract around a clean structured payload for proposal, solicitation, team members, collaborators, budgets, and workflow flags; the current create flow is inconsistent.
41. Update persistence logic so new request-form fields map cleanly into proposal, solicitation, team member, collaborator, and status records.
42. Update notification logic to include the new yes-triggered checklist behaviors and any internal review routing.
43. Update reporting/export logic to include new fields and remove retired fields.
44. Review downstream update/detail screens so the new fields and removed fields stay consistent across create, edit, detail, exports, and email templates.

**Clarifications Needed Before Build**
45. Confirm whether post-docs belong in the CCI lead/team dropdowns.
46. Confirm whether `Solicitation Deadline` remains required when `Target Submission Date` is added.
47. Confirm whether `COEUS #` is being replaced by a new internal proposal ID.
48. Confirm whether `Prime Sponsor` should be agency-only, sponsor-type-driven, or free text.
49. Confirm how auto-generated solicitation short names and keywords should work, and whether they are editable.
50. Confirm the authoritative data sources for `Other Drexel` people and department/org lookups.

If you want, I can turn this next into a build-ready implementation backlog split into `frontend`, `API`, `model/schema`, and `migration/reporting` tasks.