# PRD Template

Use this exact structure when generating PRDs.

> **Note for AI coding agents**: Sections 4 (Out of Scope) and 11 (Implementation Phases) are critical. Do not skip them or generate code that exceeds the explicit scope. Execute phases sequentially; each phase's output is the input for the next.

---

# PRD: [Feature Name]

**Priority**: P0 / P1 / P2
**Status**: Draft / Review / Approved
**Last updated**: YYYY-MM-DD

## 1. Overview
Brief description of the feature, why it matters, and how it fits into the platform.

## 2. Stakeholders

| Role          | Name / Team    | Interest                   |
|---------------|----------------|----------------------------|
| Product owner | [Name]         | Final approval on scope    |
| End users     | [User segment] | Will use the feature daily |
| [Other]       | [Name / team]  | [What they care about]     |

## 3. Problem Statement
- What pain point does this solve?
- Who is affected?
- What happens today without this feature?

## 4. Goals & Success Metrics (KPIs)

| Goal     | KPI                    | Baseline        | Target         |
|----------|------------------------|-----------------|----------------|
| [Goal 1] | [Measurable indicator] | [Current value] | [Target value] |

> KPIs must be measurable and time-bound (e.g., "reduce time-to-hire by 20% within 90 days of launch"). Avoid vague goals like "improve UX".

## 5. Scope

### In Scope
- Bullet list of what IS included in this feature

### Out of Scope (Non-Goals)
> **Critical for AI agents**: these limits are explicit. Do not implement anything listed here, even if it seems like a natural extension.

- [What is explicitly excluded and why]
- [What is deferred to a future phase and why]

## 6. User Stories

| ID     | As a... | I want to... | So that... | Priority  |
|--------|---------|--------------|------------|-----------|
| US-001 | [role]  | [action]     | [benefit]  | Must have |

## 7. Functional Requirements

### FR-001: [Requirement Title]
- **Description**: What the system must do, in plain language from the user's perspective.
- **Acceptance Criteria**:
  ```
  Scenario 1: [descriptive name]
  Given [precondition]
  When [action]
  Then
  - [expected result 1]
  - [expected result 2]
  - [expected result 3]
  ```
- **Business Rules**: Constraints or logic rules (no DB fields, no API details)

(Repeat for each requirement)

## 8. Non-Functional Requirements

- **Performance**: Response time and throughput targets as numbers (e.g., "< 500ms", ">= 99.5% uptime"). Do not specify which technology achieves them.
- **Security**: Auth requirements, data privacy, and compliance needs (e.g., GDPR, WCAG). Do not specify implementation (no JWT, Redis, RLS, etc.).
- **Scalability**: Expected user load and growth (e.g., "support 500 concurrent users"). No infrastructure specifics.
- **Accessibility**: WCAG compliance level and key requirements.

## 9. UI/UX Considerations

- Key screens or interactions
- Wireframe references (if applicable)
- User flow description

## 10. Dependencies

- Other **features** or **modules** this depends on (not infrastructure)
- External **services** required (e.g., "calendar integration", "e-signature provider")

## 11. Risks & Mitigations

| Risk     | Impact       | Probability  | Mitigation |
|----------|--------------|--------------|------------|
| [Risk 1] | High/Med/Low | High/Med/Low | [Strategy] |

## 12. Implementation Phases

> Structured for sequential execution by AI coding agents. Each phase has explicit dependencies and a verifiable output. Do not start a phase until the previous one's output is confirmed.
>
> **Phase sizing**: each phase should represent ~5–15 minutes of agent work. Larger phases introduce too many variables; smaller phases create unnecessary overhead.
>
> **No dead ends**: every phase must end with the codebase in a runnable state. No commented-out blocks, no placeholder functions left unresolved — the agent cannot distinguish scaffolding from bugs.

### Phase 1: [Name] (MVP)
- **Depends on**: nothing / [previous phase output]
- **Scope**: [What gets built — product-level, no implementation details]
- **Verifiable output**: [How to confirm this phase is done, e.g., "user can complete X end-to-end"]
- **DO NOT CHANGE**: nothing yet / [list any existing elements that must remain untouched]

### Phase 2: [Name] (Enhancement)
- **Depends on**: Phase 1 output — [specific capability that must exist]
- **Scope**: [What gets built]
- **Verifiable output**: [Confirmation criteria]
- **DO NOT CHANGE**: [Phase 1 elements that must remain stable, e.g., database schema, API signatures, auth flow]

### Phase 3: [Name] (Scale / Polish)
- **Depends on**: Phase 2 output — [specific capability that must exist]
- **Scope**: [What gets built]
- **Verifiable output**: [Confirmation criteria]
- **DO NOT CHANGE**: [Phase 1–2 elements that must remain stable]

## 13. Open Questions

- [ ] Question 1
- [ ] Question 2
