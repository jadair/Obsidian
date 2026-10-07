---
title: "Course Assistant / Scheduler Release Notes"
version: "1.0"
release_date: "TBD"
status: "In Progress"
audience: ["Technical", "Stakeholder"]
project: "[[Home|CCIA]]"
---

# Release Notes: Course Assistant & Scheduler

**Last Updated:** [Date]  
**Version:** 1.0  
**Project:** [[Home|CCIA - Course Assistant & Scheduler]]

---

## Overview

This release includes improvements to documentation, application cleanup automation, new export formats, CLC displays, course management features, and user profile functionality.

---

## Released Features

### Documentation

- Updated documentation deployed to production
- Additional documentation in progress:
  - New-term setup guide
  - TA creation workflow
  - Applicant pool management

**Impact:** Improved user onboarding and self-service support

---

### Course Assistant: In-Progress Application Cleanup

**What changed:**
- Applications in "In Progress" status for **30+ days** are now automatically deleted
- Initial cleanup completed (removed all legacy in-progress applications)
- Automated weekly cleanup going forward
- Notifications sent before deletion to alert applicants

**Why:** Reduce database clutter and improve user experience by removing stale applications

---

### Scheduler: New Export Formats

**Available Now:**
- Summary Export
- Schedules – Grading Export
- Schedules – Hours Export
- Schedules – Tutoring Export

**Use Case:** Better analytics and reporting flexibility for administrators

---

### CLC Display Pages

**Production URLs:**
- [CLC Schedule Display](https://apps.cci.drexel.edu/scheduler/display/clc/)
- [CLC Roster Display](https://apps.cci.drexel.edu/scheduler/display/clc/roster/)
- [CLC Schedule Page](https://apps.cci.drexel.edu/scheduler/display/clc/schedule/)

**Status:** Testing with iCommons planned this week

---

### Scheduler Course Management

**Improvements:**
- Courses now sorted **alphanumerically** in course list
- New ability to show/hide individual courses
- Course visibility management available on course detail page

**Why:** Improved usability and course organization

---

### Scheduler Import Interface

**Enhanced:**
- Clearer status information
- More detailed feedback & error messages
- Better UX for troubleshooting import issues

#### Course Import (TMS)

- **Classes without instructor:** Now import with default placeholder; auto-replaces when instructor info provided in subsequent import
- **Location/time updates:** Latest import data automatically updates existing records

---

### User Profile Updates

Users can now manage:
- Headshot
- Preferred name
- Preferred pronouns

---

## In Progress

### Interest & Availability Surveys
- Adding ability for authorized users to **clear/reopen surveys** without IT support (for corrections)

### Documentation
- Clarifying distinction between TA creation in Scheduler vs. Course Assistant applicant pool setup

**ETA:** TBD

---

## Planned / Roadmap

### Dashboard Cleanup
Remove legacy exports from Scheduler Dashboard:
- Lanyard & BB Export
- Employee Summary Export
- Course Detail Export (Accudemia)

### UI & Workflow Improvements (Ongoing)
- **Student:** Term organization, availability entry, schedule displays, dashboard navigation
- **Faculty:** Streamlined schedule/student access, improved navigation, enhanced display options
- **Admin:** Dashboard updates, import/export workflows, course search redesign, employee management, master schedule view

---

## Known Issues

| Issue | Workaround | Status |
|-------|-----------|--------|
| | | Pending |

---

## Resources

- **Project Home:** [[Home|CCIA]]
- **GitHub Repo:** [Link]
- **Support:** [Contact Info]

---