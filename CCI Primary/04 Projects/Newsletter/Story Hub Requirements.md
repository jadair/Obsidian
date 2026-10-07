## Overview

Story Hub is a centralized web application designed to collect, route, review, and manage potential news and communications content across the university.

The platform will allow faculty, staff, students, alumni, and external community members to submit newsworthy items that may be used for:

- Website news
    
- News bytes
    
- Social media
    
- College newsletters
    
- School newsletters
    
- Research newsletters
    
- Department communications
    
- Event promotion
    
- Internal communications
    

The goal of Story Hub is to reduce fragmented email-based processes, improve collaboration between communications and operational teams, and create a scalable university-wide system for capturing and promoting achievements, events, research, and engagement activities.

---

# Primary Goals

- Centralize story and news intake
    
- Improve visibility into pending and published content
    
- Automate routing to the correct teams
    
- Support college/university-wide scalability
    
- Enable reuse of submissions across multiple communication channels
    
- Create a searchable archive of institutional achievements and activities
    

---

# Who Can Submit

Story Hub will support submissions from:

- Faculty
    
- Staff
    
- Students
    
- Alumni
    
- External community members and partners
    

## Internal Users

Users with university accounts will be encouraged to log in using university SSO.

When authenticated, Story Hub can automatically capture:

- Name
    
- Email
    
- School (Once supplied)*
    
- College (Once supplied)*
    
- Department (Once Supplied)*
    
- Other institutional attributes where available

*Some data may be loaded from external sources where available.  We may need users to specify this information once, then the data will be stored and referenced for future use.

## External Users

External users will be able to submit stories through a public-facing form without authentication.

Anonymous users will:

- Be able to submit stories
    
- Receive optional email confirmation
    
- Not have access to dashboards or internal workflows
    

---

# Types of Content

Story Hub should support many forms of institutional news and communications content, including:

- News articles
    
- Research updates
    
- Grants and awards
    
- Student achievements
    
- Faculty achievements
    
- Alumni achievements
    
- Events
    
- Community engagement
    
- Industry partnerships
    
- Publications
    
- Media mentions
    
- Social media content ideas
    
- General story ideas
  
- Honors and Recognitions
  
- Presentation or Talk
  
- Other noteworthy achievements
    

The system should remain flexible so additional categories can be added over time.

---

# Organizational Structure and Scalability

The application should be designed to scale across the university.

Submissions may be associated with:
    
- College
    
- School
    
- Department
    
- Program
    
- Center or Institute
    

The system should support:

- Multi-college use
    
- School-specific workflows
    
- Department-specific routing
    
- Shared communications teams
    
- Separate newsletter and publication workflows by organizational unit
    

---

# Routing and Review Workflow

Submissions should automatically or manually route to the appropriate reviewers based on content type and organizational affiliation.

Potential reviewers may include:

- Communications staff
    
- Research operations
    
- Department heads
    
- School communications teams
    
- Program administrators
    
- Event coordinators
    

Examples:

- Research-related items may route to Research Operations
    
- Department-specific news may route to department leadership
    
- Event submissions may route to event coordinators and communications
    
- Social media ideas may route directly to communications staff
    

Reviewers should be able to:

- Approve submissions
    
- Reject submissions
    
- Request more information
    
- Assign additional reviewers
    
- Mark content for publication channels
    

---

# Publication and Content Reuse

A single submission may be reused in multiple places.

Examples:

- Website article
    
- Social media post
    
- Newsletter item
    
- Research digest
    
- Internal announcement
    

Story Hub should track:

- Where content was used
    
- Publication dates
    
- Related URLs
    
- Newsletter inclusion
    
- Social media usage
    

---

# Dashboards

Dashboards should only be available to authenticated users.

## Submitter Dashboard

Internal authenticated users should be able to:

- View their submissions
    
- Track status
    
- Respond to requests for additional information
    

## Reviewer Dashboard

Authorized reviewers should be able to:

- Review assigned submissions
    
- Filter by organization, type, or status
    
- Manage workflows
    
- Track publication outcomes
    

## Administrative Dashboard

Administrators should be able to:

- Configure routing rules
    
- Manage submission categories
    
- View reporting and analytics
    
- Manage organizational structures
    
- Manage permissions and workflows
    

---

# Search and Reporting

The system should support search and reporting across:

- Submission type
    
- School
    
- College
    
- Department
    
- Publication channel
    
- Status
    
- Date range
    
- Submitter type
    

Reports may include:

- Submission volume
    
- Publication metrics
    
- Engagement by department
    
- Research activity
    
- Newsletter utilization
    
- Workflow turnaround times
    

---

# Initial Technology Direction

Recommended stack:

- Django backend
    
- Django templates for primary UI
    
- Optional React components for advanced interactive interfaces
    
- MySQL database
    
- University SSO integration
    
- Responsive mobile-friendly design
    

---

# MVP Scope

Initial release should include:

- Public submission form
    
- University SSO login
    
- Internal dashboards
    
- Submission workflow management
    
- Routing and assignment
    
- Attachments
    
- Notifications
    
- Search and filtering
    
- Reporting basics
    
- Publication tracking
    

---

# Long-Term Vision

Future enhancements may include:

- AI-assisted content summaries
    
- Newsletter builders
    
- CMS integrations (We cannot integrate directly into Sitecore but may be able to generate usable html that can be copied and pasted)
    
- Advanced analytics
    
- Public-facing story showcases (Is this something we are interested in?)

---

# Story Hub — Technical Requirements Version

# 1. Architecture

## Application Stack

### Backend

- Django (latest LTS preferred)
    

### Frontend

- Django templates as primary rendering layer
    
- Optional React islands/components for dynamic UI areas
    

### Database

- MySQL initially
    
- Architecture should remain database-portable where possible
    

### Infrastructure

- Ubuntu LTS
    
- Gunicorn + Nginx
    
- Redis + Celery for async tasks
    
- S3-compatible object storage for media uploads
    

---

# 2. Authentication and Authorization

## Internal Authentication

- CAS/SSO authentication required for internal users
    
- Auto-create/update local user profiles on login
    
- Sync available attributes where possible:
    
    - Name
        
    - Email
        
    - School
        
    - College
        
    - Department
        
    - Employee/student status
        

## Anonymous External Submission

Public submission endpoint:

- No login required
    
- CAPTCHA/spam protection required
    
- Rate limiting required
    

Anonymous users:

- May create submissions
    
- May upload attachments
    
- Cannot access dashboards
    
- Cannot edit submissions after submission unless future tokenized editing is added
    

---

# 3. Organizational Hierarchy Model

The system must support scalable university-wide organizational hierarchy.

Recommended structure:

    - College
        
        - School
            
            - Department
                
                - Program
                    
                - Center/Institute
                    

Routing and permissions should support inheritance and overrides.

Example:

- College communications team sees all college submissions
    
- Department reviewer sees only department submissions
    
- Research Operations sees all research-related items
    

---

# 4. Core Models

## Submission

Fields:

- title
    
- short_summary
    
- full_description
    
- submission_type
    
- status
    
- priority
    
- submitter
    
- external_submitter_name
    
- external_submitter_email
    
- school
    
- college
    
- department
    
- program
    
- center
    
- event_date
    
- requested_publish_date
    
- time_sensitive
    
- research_related
    
- public_sharing_approved
    
- created_at
    
- updated_at
    

## SubmissionPerson

Fields:

- submission
    
- name
    
- email
    
- affiliation
    
- role
    
- school
    
- college
    
- department
    
- public_display_approved
    

## SubmissionAttachment

Fields:

- submission
    
- file
    
- caption
    
- credit
    
- uploaded_by
    
- uploaded_at
    

## RoutingRule

Fields:

- submission_type
    
- school
    
- college
    
- department
    
- conditions_json
    
- destination_group
    
- priority
    

## ReviewAssignment

Fields:

- submission
    
- assigned_user
    
- assigned_group
    
- assigned_by
    
- status
    
- due_date
    

## ChannelUsage

Fields:

- submission
    
- channel
    
- publication_status
    
- final_title
    
- final_copy
    
- publication_url
    
- publication_date
    

## InternalNote

Fields:

- submission
    
- author
    
- note
    
- visibility
    
- created_at
    

---

# 5. Submission Types

Initial configurable types:

- News article
    
- Research
    
- Event
    
- Award
    
- Publication
    
- Student achievement
    
- Faculty achievement
    
- Alumni achievement
    
- Social media idea
    
- Community engagement
    
- General story idea
    
- Other
    

Should be admin-configurable.

---

# 6. Suggested Publication Channels

Initial channels:

- Website news
    
- News bytes
    
- Social media
    
- College newsletter
    
- School newsletter
    
- Research newsletter
    
- Department newsletter
    
- Internal communications
    
- Event promotion
    

Channels should be configurable.

---

# 7. Workflow States

Recommended statuses:

- Draft
    
- Submitted
    
- Under Review
    
- Needs More Information
    
- Routed
    
- Approved
    
- Scheduled
    
- Published
    
- Archived
    
- Rejected
    
- Duplicate
    

Workflow transitions should be permission-aware.

---

# 8. Routing Engine

## Requirements

Routing should support:

- Rule-based routing
    
- Manual reassignment
    
- Multi-destination routing
    
- Conditional routing
    

Routing conditions may include:

- Submission type
    
- Organizational unit
    
- Research flag
    
- Event flag
    
- Priority
    
- Time sensitivity
    
- Suggested channel
    

---

# 9. Dashboard Requirements

## Dashboard Access

Dashboards require authentication.

Anonymous external users:

- No dashboard access
    
- No submission tracking
    

## Reviewer Dashboard

Features:

- Assigned submissions
    
- Pending review
    
- Recently submitted
    
- Filters
    
- Saved views
    
- Bulk actions
    

## Admin Dashboard

Features:

- Routing management
    
- Workflow analytics
    
- Submission reporting
    
- User/group management
    
- Taxonomy management
    

---

# 10. Search Requirements

Search fields:

- Title
    
- Description
    
- People involved
    
- Organizational unit
    
- Tags
    
- Submission type
    
- Publication channel
    

Filters:

- Status
    
- College
    
- School
    
- Department
    
- Reviewer
    
- Time-sensitive
    
- Research-related
    
- Date range
    

---

# 11. Notifications

Notification triggers:

- Submission created
    
- Assignment created
    
- Status updated
    
- More information requested
    
- Submission approved/rejected
    
- Publication completed
    

Delivery methods:

- Email initially
    
- Optional future in-app notifications
    

---

# 12. Security Requirements

- CSRF protection
    
- CAPTCHA on public forms
    
- File upload validation
    
- MIME type validation
    
- Virus scanning optional future enhancement
    
- Rate limiting on anonymous submissions
    
- Permission-based object access
    
- Audit logging for workflow actions
    

---

# 13. API Requirements

Optional API layer using Django REST Framework.

Potential uses:

- CMS integrations
    
- Newsletter integrations
    
- Reporting exports
    
- React-driven UI components
    
- External communications tooling
    

---

# 14. Non-Functional Requirements

## Performance

- Support high-volume submission periods
    
- Optimized dashboard filtering/search
    

## Scalability

- Multi-college and university-wide capable
    
- Configurable routing architecture
    

## Accessibility

- WCAG 2.1 AA compliance target
    

## Responsive Design

- Mobile-friendly submission forms
    
- Tablet-compatible reviewer dashboards
    

## Maintainability

- Configurable taxonomy and routing
    
- Minimal hardcoded organizational logic
    

---

# 15. MVP Technical Scope

## Included

- Public submission form
    
- Internal SSO login
    
- Reviewer dashboard
    
- Routing workflows
    
- File uploads
    
- Search/filtering
    
- Email notifications
    
- Publication tracking
    
- Basic reporting
    

## Deferred

- AI-assisted summaries
    
- CMS integrations
    
- Social media scheduling integrations
    
- Newsletter builder
    
- Advanced analytics
    
- Public story showcase
    
- Workflow automation enhancements