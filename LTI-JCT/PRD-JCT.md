# PRD: LTI ATS — Applicant-Tracking System

**Priority**: P0 (MVP)
**Status**: Draft
**Last updated**: 2026-04-05

---

## 1. Overview

LTI is a startup building the next-generation Applicant-Tracking System (ATS). The platform targets HR departments that struggle with manual, fragmented hiring workflows. LTI ATS centralizes the entire recruitment lifecycle — from job posting to offer — while embedding AI assistance and real-time collaboration at every step, enabling recruiters and managers to make faster, better-informed hiring decisions.

No prior system exists. This PRD defines the MVP product scope required to launch a differentiated ATS and validate product-market fit with early enterprise customers.

---

## 2. Stakeholders

| Role            | Name / Team             | Interest                                        |
|-----------------|-------------------------|-------------------------------------------------|
| Product Owner   | LTI Product Team        | Final approval on scope and priorities          |
| HR Recruiters   | End users (primary)     | Daily pipeline management and candidate comms   |
| Hiring Managers | End users (secondary)   | Candidate review, feedback, and hire/reject      |
| Candidates      | External users          | Apply, track application status, upload docs    |
| HR Admins       | End users (config)      | Workflow configuration, user management, reports|
| Legal / DPO     | LTI Legal               | GDPR compliance and data residency              |

---

## 3. Problem Statement

- **Pain point**: HR teams rely on spreadsheets, email threads, and disconnected tools to track candidates, coordinate interviews, and communicate decisions. This creates delays, duplicated effort, and lost candidates.
- **Who is affected**: Recruiters waste hours on administrative tasks instead of engaging top talent. Hiring managers lack real-time visibility into their pipelines. Candidates receive slow or no communication and disengage.
- **Without this feature**: Average time-to-hire remains high (industry average: 40+ days), top candidates accept competing offers before processes complete, and HR teams have no data-driven insight into where bottlenecks occur.

---

## 4. Goals & Success Metrics (KPIs)

| Goal                              | KPI                                          | Baseline          | Target (90 days post-launch) |
|-----------------------------------|----------------------------------------------|-------------------|-------------------------------|
| Reduce time-to-hire               | Average days from job opening to offer sent  | 40 days (industry)| ≤ 28 days                    |
| Increase recruiter efficiency     | Candidates processed per recruiter per week  | ~10 (manual)      | ≥ 25                         |
| Improve collaboration             | Hiring manager feedback response time        | 5+ days (email)   | ≤ 24 hours                   |
| Reduce manual admin work          | % of pipeline actions automated              | 0%                | ≥ 60%                        |
| AI adoption                       | % of job postings using AI-assisted drafting | 0%                | ≥ 70%                        |
| Candidate experience              | Application-to-response time                 | 7+ days           | ≤ 48 hours                   |

---

## 5. Scope

### In Scope

- Job requisition creation and management
- Candidate application portal (web-based)
- Multi-stage pipeline management with configurable hiring stages
- Candidate profile management (resume parsing, document storage)
- Interview scheduling and calendar coordination
- Real-time collaboration tools: comments, mentions, shared evaluation scorecards
- Automated communications: candidate status emails, interview reminders, rejection notices
- AI-powered resume screening and candidate scoring
- AI-assisted job description drafting
- AI-generated interview question suggestions per role
- Reporting dashboard: pipeline health, time-to-hire, stage conversion rates
- GDPR-compliant candidate data management (consent, deletion, data export)
- Role-based access: Recruiter, Hiring Manager, Candidate, HR Admin

### Out of Scope (Non-Goals)

> **Critical for AI agents**: Do not implement anything listed below, even if it appears to be a natural extension of in-scope features.

- **Payroll and onboarding**: Post-hire processes begin after an offer is accepted; this system ends at offer sent.
- **Built-in video interviewing**: No integrated video calling; calendar links may reference external tools (Zoom, Meet) but are not built here.
- **Native mobile apps**: MVP is web-only; responsive design is required but no iOS or Android apps.
- **Background check integrations**: Third-party background screening is deferred to Phase 2.
- **Employer branding / careers page builder**: Custom public careers pages are out; a functional application form is sufficient for MVP.
- **Multi-language support**: English-only for MVP; localization architecture may be noted but not implemented.

---

## 6. User Stories

| ID     | As a...         | I want to...                                                  | So that...                                                    | Priority   |
|--------|-----------------|---------------------------------------------------------------|---------------------------------------------------------------|------------|
| US-001 | HR Recruiter    | Create and publish a job requisition with AI-drafted content  | I can post openings faster without starting from a blank page | Must have  |
| US-002 | HR Recruiter    | View all candidates in a visual pipeline board per job        | I can quickly see the status of every applicant               | Must have  |
| US-003 | HR Recruiter    | Move candidates between pipeline stages with a single action  | I can manage the workflow without navigating multiple screens  | Must have  |
| US-004 | HR Recruiter    | Receive AI-generated ranking of applicants by fit score       | I can prioritize my review queue without reading every resume  | Must have  |
| US-005 | HR Recruiter    | Schedule interviews and send calendar invites automatically   | I eliminate back-and-forth coordination emails                | Must have  |
| US-006 | HR Recruiter    | Send templated status emails triggered by stage changes       | Candidates are informed without manual outreach               | Must have  |
| US-007 | Hiring Manager  | Receive a notification when a candidate is ready for review   | I can give timely feedback without chasing recruiters         | Must have  |
| US-008 | Hiring Manager  | Submit a structured scorecard evaluation for each candidate   | My feedback is captured consistently and shared with the team | Must have  |
| US-009 | Hiring Manager  | Comment on a candidate profile and mention a colleague        | Collaboration happens in context, not in email threads        | Must have  |
| US-010 | Candidate       | Submit an application and upload my resume via a web form     | I can apply without creating an account on a third-party site | Must have  |
| US-011 | Candidate       | Receive automated updates on my application status by email  | I'm not left wondering where I stand in the process           | Must have  |
| US-012 | Candidate       | Request deletion of my personal data                          | My GDPR right to erasure is honored                           | Must have  |
| US-013 | HR Admin        | Configure the hiring stages for each job type                 | Different roles can follow different workflows                | Must have  |
| US-014 | HR Admin        | Manage user roles and permissions                             | Access is controlled and auditable                            | Must have  |
| US-015 | HR Admin        | Export candidate data in a machine-readable format            | We can comply with GDPR data portability requests             | Must have  |
| US-016 | HR Recruiter    | View a dashboard showing pipeline metrics and time-to-hire    | I can identify bottlenecks and report to leadership           | Should have|
| US-017 | HR Recruiter    | Get AI-suggested interview questions for a specific role      | Interviews are consistent and role-relevant                   | Should have|
| US-018 | Hiring Manager  | View aggregated scorecard results across all interviewers     | Hiring decisions are based on structured, consolidated data   | Should have|

---

## 7. Functional Requirements

### FR-001: Job Requisition Management

- **Description**: Recruiters and HR Admins can create, edit, publish, and close job requisitions. Each requisition defines the role title, department, location, employment type, and hiring pipeline template.
- **Acceptance Criteria**:
  ```
  Scenario 1: Create a new job requisition
  Given a recruiter is logged in
  When they complete the requisition form and click "Publish"
  Then
  - The job appears in the active jobs list
  - A unique application URL is generated
  - The configured hiring pipeline stages are attached

  Scenario 2: Close a filled position
  Given a job requisition is active
  When the recruiter marks it as "Filled"
  Then
  - The application portal link becomes inactive
  - Candidates in non-final stages receive a closure notification
  - The requisition is moved to the closed jobs archive
  ```
- **Business Rules**: A requisition requires at minimum a title, department, and at least one pipeline stage before it can be published.

---

### FR-002: Candidate Application Portal

- **Description**: External candidates can submit applications for published roles via a web form. The form collects personal details, resume upload, and any role-specific questions. No account creation is required to apply.
- **Acceptance Criteria**:
  ```
  Scenario 1: Successful application submission
  Given a candidate accesses a published job URL
  When they complete and submit the application form
  Then
  - The candidate receives a confirmation email within 2 minutes
  - A candidate profile is created in the system
  - The candidate appears in the first pipeline stage

  Scenario 2: Duplicate application prevention
  Given a candidate has already applied to a role
  When they attempt to submit a second application with the same email
  Then
  - The system rejects the duplicate and shows an informative message
  - The original application is preserved unchanged

  Scenario 3: GDPR consent capture
  Given any candidate submitting an application
  When the form is submitted
  Then
  - Explicit consent to process personal data is recorded with a timestamp
  - The consent record is stored and auditable
  ```
- **Business Rules**: Resume upload is required. Accepted formats: PDF, DOCX. Maximum file size: 5 MB.

---

### FR-003: Pipeline Board and Stage Management

- **Description**: Recruiters see all candidates for a job arranged in a Kanban-style board by pipeline stage. Candidates can be moved between stages via drag-and-drop or a stage selector. Stage transitions may trigger automated actions.
- **Acceptance Criteria**:
  ```
  Scenario 1: Move a candidate to the next stage
  Given a recruiter views a candidate on the pipeline board
  When they drag the candidate card to a new stage column
  Then
  - The candidate's stage is updated immediately
  - Any automation rules configured for that stage trigger (e.g., send email, notify manager)
  - An audit log entry is created with actor and timestamp

  Scenario 2: Bulk stage action
  Given a recruiter selects multiple candidates
  When they choose "Move to stage" from the bulk actions menu
  Then
  - All selected candidates move to the specified stage
  - Stage-triggered automations fire for each candidate individually
  ```
- **Business Rules**: Stage order is defined per job template. A candidate cannot skip mandatory stages unless the recruiter has HR Admin permissions.

---

### FR-004: AI Resume Screening and Candidate Scoring

- **Description**: When a candidate applies, the AI analyzes the resume against the job description and generates a fit score (0–100) with a brief rationale. Recruiters can see this score on the pipeline board and candidate profile.
- **Acceptance Criteria**:
  ```
  Scenario 1: AI score generated on application
  Given a candidate submits an application with a resume
  When the system processes the submission
  Then
  - A fit score between 0 and 100 is displayed on the candidate card within 60 seconds
  - A short rationale (≤ 3 bullet points) explains the score
  - The score is clearly labeled as AI-generated

  Scenario 2: Recruiter overrides or dismisses AI score
  Given a recruiter disagrees with the AI score
  When they mark the score as "Overridden" and proceed with the candidate
  Then
  - The override is recorded in the audit log
  - The candidate's manual status takes precedence in sorted views
  ```
- **Business Rules**: AI scores are advisory only; they cannot block or auto-reject candidates. All automated scoring decisions must be disclosed to candidates upon request (GDPR transparency).

---

### FR-005: AI-Assisted Job Description Drafting

- **Description**: When creating a requisition, recruiters can invoke an AI assistant to generate a draft job description based on the role title, department, and key responsibilities they specify. The draft is editable before publishing.
- **Acceptance Criteria**:
  ```
  Scenario 1: Generate a draft job description
  Given a recruiter has entered a role title and department
  When they click "Generate with AI"
  Then
  - A structured draft (summary, responsibilities, requirements, nice-to-haves) appears in the editor within 10 seconds
  - The recruiter can edit any section before publishing

  Scenario 2: Regenerate after editing
  Given a recruiter has a draft and modifies the key responsibilities
  When they click "Regenerate"
  Then
  - A new draft is generated incorporating the updated responsibilities
  - The previous draft is preserved and accessible via "Undo"
  ```
- **Business Rules**: The AI draft does not publish automatically. A recruiter must explicitly review and save before the job goes live.

---

### FR-006: Interview Scheduling and Automation

- **Description**: Recruiters can schedule interviews from within the platform. The system sends calendar invites to all participants and reminder notifications before the interview time. Interview results are linked back to the candidate's profile.
- **Acceptance Criteria**:
  ```
  Scenario 1: Schedule an interview
  Given a candidate is in an interview-eligible stage
  When the recruiter creates an interview slot and selects participants
  Then
  - All participants receive a calendar invite via email
  - The interview appears on the candidate's timeline
  - A reminder is automatically sent 24 hours before the scheduled time

  Scenario 2: Reschedule an interview
  Given a scheduled interview exists
  When the recruiter changes the time
  Then
  - Updated invites are sent to all participants
  - The original invite is cancelled
  - The candidate's timeline reflects the new time
  ```
- **Business Rules**: Interviews require at least one internal participant (recruiter or hiring manager). The system does not host video calls; external meeting links may be included as free-text.

---

### FR-007: Real-Time Collaboration — Comments and Mentions

- **Description**: Any internal user (recruiter, hiring manager, HR admin) can leave comments on a candidate's profile. Users can @mention colleagues to request their attention. Mentioned users receive an in-app and email notification.
- **Acceptance Criteria**:
  ```
  Scenario 1: Leave a comment and mention a colleague
  Given a hiring manager is viewing a candidate profile
  When they type a comment with @username and submit
  Then
  - The comment appears on the profile immediately
  - The mentioned user receives an in-app notification and an email
  - All team members with access to the job can see the comment

  Scenario 2: Comment thread on a specific section
  Given multiple users comment on the same candidate
  Then
  - Comments are displayed in chronological order with author and timestamp
  - A total comment count is visible on the pipeline board card
  ```
- **Business Rules**: Comments are visible to all internal users with access to the job. Candidates cannot see internal comments.

---

### FR-008: Evaluation Scorecards

- **Description**: HR Admins can define structured scorecard templates per job type. Interviewers complete a scorecard for each candidate they assess. Results are aggregated and visible to the hiring team.
- **Acceptance Criteria**:
  ```
  Scenario 1: Submit a scorecard
  Given an interviewer has completed an interview
  When they fill in the scorecard and submit
  Then
  - The scorecard is saved and linked to the candidate profile
  - The recruiter receives a notification that feedback is available
  - The hiring team sees the aggregated score on the candidate profile

  Scenario 2: View aggregated results
  Given multiple interviewers have submitted scorecards
  When a recruiter or hiring manager views the candidate profile
  Then
  - Individual scores and comments are visible (with interviewer attribution)
  - An average score across all completed scorecards is displayed
  ```
- **Business Rules**: A scorecard is locked after submission; edits require HR Admin override. Scorecards are not visible to candidates.

---

### FR-009: Automated Candidate Communications

- **Description**: The system sends automated emails to candidates when their application status changes. HR Admins can configure email templates per pipeline stage. Emails are sent from the company's configured sender domain.
- **Acceptance Criteria**:
  ```
  Scenario 1: Automatic acknowledgment on application
  Given a candidate submits an application
  Then
  - An acknowledgment email is sent within 2 minutes of submission

  Scenario 2: Stage-change notification
  Given a recruiter moves a candidate to a new stage that has an email template configured
  Then
  - The email is sent to the candidate within 5 minutes of the stage change
  - The email uses the template defined for that stage with candidate name merged

  Scenario 3: Rejection notification
  Given a recruiter moves a candidate to the "Rejected" stage
  Then
  - A rejection email is sent automatically using the rejection template
  - The candidate can no longer access the application portal link for that role
  ```
- **Business Rules**: At minimum, acknowledgment and rejection templates are required system defaults. Recruiters may not disable rejection notifications (GDPR transparency obligation).

---

### FR-010: GDPR Data Management

- **Description**: The system provides tools for HR Admins and candidates to satisfy GDPR obligations: data access, portability, deletion (right to erasure), and retention policy enforcement.
- **Acceptance Criteria**:
  ```
  Scenario 1: Candidate requests data export
  Given an HR Admin receives a GDPR data access request
  When they trigger a data export for the candidate's email
  Then
  - A JSON or CSV file containing all stored personal data is generated within 72 hours
  - The file is delivered securely and the action is logged

  Scenario 2: Candidate requests erasure
  Given a candidate submits a deletion request via email or form
  When an HR Admin executes the erasure
  Then
  - All personally identifiable information is deleted or anonymized
  - Aggregate metrics derived from the candidate's data are preserved in anonymized form
  - The deletion event is logged with timestamp and actor

  Scenario 3: Retention policy enforcement
  Given a candidate's application is older than the configured retention period (default: 2 years)
  Then
  - The system notifies HR Admins before automated anonymization
  - Personal data is anonymized on the retention expiry date unless manually extended
  ```
- **Business Rules**: Personal data must not be transferred outside the EU without explicit contractual safeguards. Consent records must be retained even after erasure of other data, per GDPR Article 7.

---

### FR-011: Reporting Dashboard

- **Description**: Recruiters and HR Admins can view a real-time dashboard of recruitment metrics, including pipeline health, time-to-hire per role, and stage conversion rates.
- **Acceptance Criteria**:
  ```
  Scenario 1: View pipeline health
  Given a recruiter opens the dashboard
  Then
  - They see the number of open roles, total active candidates, and candidates per stage
  - Data reflects the current state (updated within 1 minute)

  Scenario 2: Time-to-hire report
  Given a recruiter selects a date range
  Then
  - Average time-to-hire is shown per job and in aggregate
  - Stage conversion rates (% of candidates advancing per stage) are displayed as a funnel
  ```
- **Business Rules**: Dashboard data is filtered by the user's role-based access; recruiters see only their assigned jobs unless they have HR Admin permissions.

---

## 8. Non-Functional Requirements

- **Performance**: All page loads and pipeline interactions must respond in < 500ms (p95). Resume AI scoring must complete within 60 seconds of application submission. Dashboard data must be no more than 60 seconds stale.
- **Security**: All user sessions require authenticated access. Candidate data must be encrypted at rest and in transit. Role-based access control enforces data isolation between jobs and teams. GDPR data residency: all EU candidate data must be stored and processed within EU infrastructure.
- **Scalability**: MVP must support up to 50 concurrent internal users and 1,000 candidate applications per day per customer instance.
- **Reliability**: Target availability of ≥ 99.5% measured monthly, excluding scheduled maintenance windows.
- **Accessibility**: Public-facing candidate application form must meet WCAG 2.1 AA. Internal UI should meet WCAG 2.1 AA for all primary recruiter workflows.

---

## 9. UI/UX Considerations

### Key Screens

1. **Recruiter Dashboard**: Overview of all open roles with candidate counts by stage. Quick-action buttons to advance or reject candidates in bulk.
2. **Pipeline Board (per job)**: Kanban board with candidate cards showing name, AI fit score, days in stage, and last activity. Drag-and-drop stage changes.
3. **Candidate Profile**: Full application details, resume viewer, AI score with rationale, comment thread, scorecard results, and interview history.
4. **Job Requisition Form**: Step-by-step wizard with AI draft generation for job description.
5. **Interview Scheduler**: Inline scheduling interface on the candidate profile with participant selector and calendar link generation.
6. **Admin Panel**: Workflow configuration, user management, email template editor, and GDPR tools.
7. **Candidate Portal**: Simple apply form, confirmation page, and status check view (email-gated, no login required).

### User Flow (Core)

1. HR Admin configures pipeline stages and email templates.
2. Recruiter creates a job requisition (with AI draft assist) and publishes it.
3. Candidate applies via the public URL.
4. AI scores and ranks the applicant; recruiter is notified.
5. Recruiter reviews top candidates, moves them to interview stage.
6. Recruiter schedules interview; all parties receive invites.
7. Hiring Manager completes the scorecard post-interview.
8. Recruiter sees consolidated feedback, moves candidate to Offer or Reject.
9. Automated email is sent to candidate with the outcome.

---

## 10. Dependencies

- **Email delivery service**: External transactional email provider required for candidate and internal notifications (no specific provider mandated here).
- **Calendar invite generation**: System must generate standard iCal (.ics) attachments for interview invites; no deep calendar API integration required for MVP.
- **AI language model**: External large language model API required for job description drafting, resume scoring, and interview question generation.
- **Document parsing service**: Resume text extraction from PDF and DOCX formats required upstream of AI scoring.

---

## 11. Risks & Mitigations

| Risk                                          | Impact | Probability | Mitigation                                                                                   |
|-----------------------------------------------|--------|-------------|----------------------------------------------------------------------------------------------|
| AI scoring perceived as biased or opaque      | High   | High        | Make scores advisory-only, require rationale display, and allow recruiter override with audit log |
| GDPR non-compliance at launch                 | High   | Medium      | Engage DPO in design review; implement consent and erasure flows before any EU data ingested |
| Low hiring manager adoption of scorecards     | Medium | High        | Keep scorecards short (≤ 5 criteria); send reminder notifications; show value via dashboard  |
| Resume parsing quality varies by format       | Medium | Medium      | Fall back to raw text extraction; flag low-confidence parses for manual recruiter review     |
| Automated emails marked as spam               | Medium | Medium      | Use dedicated sending domain with SPF/DKIM; limit email volume per candidate per day         |
| Scope creep from "quick wins" outside MVP     | High   | High        | All feature requests during build are queued in backlog; nothing added without PRD update    |

---

## 12. Implementation Phases

> Structured for sequential execution by AI coding agents. Each phase has explicit dependencies and a verifiable output. Do not start a phase until the previous one's output is confirmed.

### Phase 1: Core Data Model and Authentication (MVP Foundation)

- **Depends on**: Nothing (greenfield start)
- **Scope**: User authentication and role-based access (Recruiter, Hiring Manager, HR Admin, Candidate). Core data entities: Jobs, Candidates, Applications, Pipeline Stages. HR Admin can configure pipeline stages per job type. Basic job requisition CRUD (no AI yet).
- **Verifiable output**: An HR Admin can log in, create a job with custom pipeline stages, and see an empty pipeline board. A recruiter can log in and view the job list. Role restrictions are enforced (e.g., a Hiring Manager cannot create jobs).
- **DO NOT CHANGE**: Nothing yet.

### Phase 2: Candidate Application Portal and Pipeline Board (MVP Core)

- **Depends on**: Phase 1 output — authenticated users exist, jobs and pipeline stages are persisted.
- **Scope**: Public candidate application form (no login required) with resume upload. Candidate profile creation on submission. Kanban pipeline board per job. Stage transitions via drag-and-drop. Confirmation email sent to candidate on application.
- **Verifiable output**: A candidate can apply via a public URL, upload a resume, and receive a confirmation email. A recruiter can view the candidate on the pipeline board and move them between stages.
- **DO NOT CHANGE**: User auth flow, role definitions, and pipeline stage configuration from Phase 1.

### Phase 3: Automated Communications and Interview Scheduling (MVP Automation)

- **Depends on**: Phase 2 output — candidates exist in the pipeline; stage transitions are working.
- **Scope**: Email templates configurable per pipeline stage. Automated emails triggered on stage changes (including rejection). Interview scheduling from candidate profile with iCal invite generation to participants. Interview reminder emails 24 hours before.
- **Verifiable output**: A recruiter can move a candidate to the "Interview" stage and schedule an interview; all participants receive an iCal invite. Moving a candidate to "Rejected" automatically sends the rejection email using the configured template.
- **DO NOT CHANGE**: Application form, pipeline board, and stage transition logic from Phase 2.

### Phase 4: Collaboration and Evaluation Tools (MVP Collaboration)

- **Depends on**: Phase 3 output — candidate profiles and interview scheduling are operational.
- **Scope**: Comments and @mentions on candidate profiles with in-app and email notifications. Scorecard templates configurable by HR Admin. Interviewers can complete and submit scorecards; aggregated results visible on the profile.
- **Verifiable output**: A hiring manager can leave a comment on a candidate profile, @mention a recruiter, and the recruiter receives a notification. An interviewer can submit a scorecard; the recruiter sees the aggregated score on the candidate profile.
- **DO NOT CHANGE**: Email automation and interview scheduling logic from Phase 3.

### Phase 5: AI Features (Differentiation Layer)

- **Depends on**: Phase 4 output — candidate data, resume text, and job descriptions are available. An AI model API is provisioned and accessible.
- **Scope**: AI fit score generated on application submission (displayed on pipeline card). AI rationale bullets on candidate profile. AI job description draft generator in the requisition form. AI interview question suggestions per role accessible from the interview scheduler.
- **Verifiable output**: A recruiter creates a job with an AI-drafted description. A candidate applies and within 60 seconds a fit score (0–100) with rationale is visible. A recruiter scheduling an interview can generate a suggested question list.
- **DO NOT CHANGE**: All pipeline, collaboration, and scoring logic from Phases 1–4. AI scores must be clearly labeled as advisory and cannot auto-reject candidates.

### Phase 6: Reporting, Dashboard, and GDPR Tools (MVP Complete)

- **Depends on**: Phase 5 output — full candidate lifecycle data is being captured.
- **Scope**: Recruiter/admin dashboard showing open roles, active candidates, and pipeline health. Time-to-hire and stage conversion funnel report. GDPR tooling: data export (JSON/CSV), manual erasure, retention policy alerts, and consent audit log.
- **Verifiable output**: An HR Admin can view the dashboard with live pipeline metrics, generate a time-to-hire report for a date range, trigger a candidate data export, and execute a deletion request — with all actions logged.
- **DO NOT CHANGE**: All AI features and collaboration tools from Phases 1–5.

---

## 13. Open Questions

- [ ] **Q1**: What is the target customer segment for MVP? (SMB vs. mid-market enterprise — affects permission complexity and multi-tenant architecture decisions.)
- [ ] **Q2**: Will LTI operate as a multi-tenant SaaS or deploy per-customer instances? (Critical for data isolation and GDPR compliance design.)
- [ ] **Q3**: Which AI model provider is contractually preferred? (Vendor selection may affect data processing agreements required for GDPR compliance.)
- [ ] **Q4**: Is job board publishing (LinkedIn, Indeed) a P1 feature or can it remain out of scope beyond MVP? (Currently excluded; clarification needed for roadmap planning.)
- [ ] **Q5**: What is the expected maximum number of active jobs and candidates per customer at launch? (Needed to validate scalability targets in NFRs.)
- [ ] **Q6**: Should candidates be able to check application status via a link without login, or is status visibility limited to email notifications? (Affects candidate portal scope.)
