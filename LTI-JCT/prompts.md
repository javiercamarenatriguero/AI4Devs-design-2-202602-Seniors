# LTI-JCT — Prompt Log

Record of all metaprompts used to generate artifacts in this project. Each entry includes the prompt used and a personal opinion note.

---

## Epics and User Stories Execution

**Prompt (metaprompt):**
> As a Product Owner of LTI ATS — an Applicant-Tracking System built from scratch for HR Recruiters, Hiring Managers, Candidates, and HR Admins — read `LTI-JCT/PRD-JCT.md` in full (focus on sections 5, 6, 7, and 12) and produce a complete backlog of epics and user stories covering the full MVP scope. Save the output to `LTI-JCT/UserStories-JCT.md`.

- Identify 1–3 epics, each with a clear business objective tied to a PRD KPI and mapped to its FR-NNN codes
- Write 2–5 user stories per epic if needed, using: `As a [role], I want to [action] so that [benefit]`
- Enforce INVEST criteria for every story — product-level only, no implementation details
- Add 2–4 acceptance scenarios per story:
  ```
  **Scenario N:** [descriptive name]
  - **Given** [precondition]
  - **When** [action]
  - **Then** [expected result 1], [expected result 2]
  ```
- Tag each story with MoSCoW priority and linked FR-NNN
- Do not add out-of-scope features (payroll, video interviews, native mobile apps)
- GDPR stories and AI feature stories are mandatory (Must have)
- US IDs must be globally unique and sequential across all epics
- Start the file with an epic index table, then one section per epic with its stories
- End with a report: epic count, story count, PRD gaps, and assumptions made

**Output:** `LTI-JCT/UserStories-JCT.md`

**Result:** 3 epics, 11 stories
- EP-01: Core Recruitment Pipeline (5 stories — FR-001, FR-002, FR-003, FR-006, FR-009)
- EP-02: AI-Assisted Hiring (3 stories — FR-004, FR-005, FR-011)
- EP-03: Collaboration, Compliance & Admin (3 stories — FR-007, FR-008, FR-010)

**Opinion:**
> Creo que la ejecución ha sido correcta siguiendo el formato descrito en las skills. He tenido que ajustar el número de Stories ya que generó un número excesivo (alrededor de 30) para este MVP. Simplemente ajustando dicho nñumero a 3-5 Stories por Epic, ha generado correctamente el Output.

---

## User Story Map Generation

**Prompt (metaprompt):**
> As a Product Owner of LTI ATS, read `LTI-JCT/UserStories-JCT.md` and `LTI-JCT/PRD-JCT.md`, then generate a User Story Map following Jeff Patton's technique. Append the output to `LTI-JCT/UserStories-JCT.md` under a new `## Story Map` section.

- Build a backbone of 4–8 activities covering the full user journey in chronological order (verb phrases, user vocabulary)
- Place existing US-NNN stories under their matching activity, ordered top-to-bottom by priority
- Draw horizontal release cut lines grouping stories into MVP and subsequent releases — the MVP cut must enable an end-to-end journey
- Do not invent stories outside `UserStories-JCT.md`; flag any journey gaps instead
- Use this layout:
  ```
  BACKBONE    [Activity 1]   [Activity 2]   ...
              ────────────────────────────────
  MVP         US-NNN         US-NNN
              ────────────────────────────────
  v1.1        US-NNN         US-NNN
  ```

**Output:** `LTI-JCT/USerStories-JCT.md` on ## Story Map

**Opinion:**
> He tenido que ajustar el Skill `story-map-generator.md` para que siga la técnica de Jeff Patton. El resultado ha sido bueno.

---

## Product Backlog Generation

**Prompt (metaprompt):**
> As a Product Owner of LTI ATS, read `LTI-JCT/UserStories-JCT.md` and `LTI-JCT/PRD-JCT.md`, then generate a product backlog by decomposing each user story into actionable tickets. Append the output to `LTI-JCT/UserStories-JCT.md` under a new `## Product Backlog` section.

- Generate tickets in `TK-NNN` format for each US-NNN story, covering only the layers the story requires:
  - **Feature** — user-facing functionality
  - **Technical Task** — infrastructure or configuration that enables a feature
  - **Spike** — time-boxed research when there is a known unknown (max 2 days; always paired with a follow-up implementation ticket)
- Testing is not a separate ticket type — acceptance criteria are included as part of each Feature and Technical Task ticket
- Each ticket must be completable by one person in 1–2 days; split anything larger
- Estimate each ticket using Fibonacci points (1, 2, 3, 5, 8) — any ticket at 8+ must be split
- Every ticket must reference its source US-NNN for traceability
- End with a summary table: `TK-NNN | Type | Story | Title | Points | Priority`

**Output:** `LTI-JCT/UserStories-JCT.md` on `Product Backlog`

**Opinion:**
> Ha generado las tareas linkadas a los UserStories correctamente. Ha generado también tareas para testing, con lo que no estoy de acuerdo. He correguido dicho punto para que el testing esté contenido dentro de cada tarea realizada.

---

## Roadmap

**Prompt (metaprompt):**
> As a Product Owner of LTI ATS, read `LTI-JCT/UserStories-JCT.md`, then build a release roadmap distributing all user stories into sprints ordered by priority and dependencies. Append the output to `LTI-JCT/UserStories-JCT.md` under a new `## Roadmap` section.

- Sprint setup: 2-week sprints, start date 2026-04-20, team velocity 20 points/sprint
- Assign stories to sprints following this order: Must have → Should have → Could have
- Respect the story map release cuts (MVP → v1.1 → v2.0) as sprint grouping boundaries
- Respect dependencies (e.g. TK-018 Spike must precede TK-019)
- For each sprint produce:
  - Sprint number, date range (start → end), release tag (MVP / v1.1 / v2.0)
  - List of US-NNN stories with points
  - Total points and remaining capacity
- End with a release summary table: `Release | Sprint | Date range | Stories | Total points`
- Flag any story that doesn't fit within its release boundary due to capacity

**Output:** `LTI-JCT/UserStories-JCT.md`

**Opinion:**
> He tenido que ajustar los Story points asignados a las tareas ya que me parecían muy bajos para la complejidad de ciertas tareas. También señalar que los riesgos no incluía la parte de AI Scoring, la cual me parece una de las tareas con mayor incertidumbre. Se ha ajustado perfectamente a lo descrito en la Skill relacionada con el Roadmap.

---

## Mermaid Roadmap

**Prompt:**
> As a Product Owner I want to create a Mermaid Roadmap based on the UserStories-JCT.md file and included in the same file.

**Output:** `LTI-JCT/UserStories-JCT.md` under `## Mermaid Roadmap`

**Opinion:**
> Creado perfectamente acorde con lo descrito.

---

## INVEST Evaluation per User Story

**Prompt (metaprompt):**
> As a Product Owner of LTI ATS, read `LTI-JCT/UserStories-JCT.md` and add an INVEST evaluation table after the acceptance criteria of each user story. Edit the file in place — do not create a new file.

- For each US-NNN story, append the following table immediately after its last acceptance scenario:
  ```
  **INVEST Evaluation**

  | Criterion | Rating | Notes |
  |-----------|--------|-------|
  | Independent | ✅ / ⚠️ | One-line rationale |
  | Negotiable | ✅ / ⚠️ | One-line rationale |
  | Valuable | ✅ / ⚠️ | One-line rationale |
  | Estimable | ✅ / ⚠️ | One-line rationale |
  | Small | ✅ / ⚠️ | One-line rationale |
  | Testable | ✅ / ⚠️ | One-line rationale |
  ```
- Use ✅ when the criterion is fully satisfied, ⚠️ when there is a known caveat or risk
- Notes must reference concrete evidence from the story (points, sprint fit, BDD scenario count, runtime dependencies)
- Do not modify any other section of the file

**Output:** `LTI-JCT/UserStories-JCT.md` — INVEST table appended inline after each story's acceptance criteria

**Opinion:**
> Revisando la documentación, faltaba la parte de INVEST por cada Story. El formato de tabla con ✅/⚠️ más una nota concreta por criterio es mucho más útil que una evaluación narrativa. El rating ⚠️ obliga a documentar el riesgo en lugar de ignorarlo, lo que hace el INVEST accionable durante la refinement session.

---

## Technical Spec per Ticket

**Prompt (metaprompt):**
> As a Tech Lead of LTI ATS, read `LTI-JCT/UserStories-JCT.md` and enrich every TK-NNN ticket in the `## Product Backlog` section with a `**Technical Spec:**` block. Edit the file in place — do not create a new file or modify any other section.

- For each ticket add a `**Technical Spec:**` subsection immediately after the `**Points/Priority/Source**` line with the following content depending on ticket type:
  - **Feature tickets**: API endpoints consumed (method, path, request/response shape), key UI behaviour, integration points
  - **Technical Task tickets**: DB schema changes (table DDL with column names, types, constraints, and indexes), REST endpoint contracts (method, path, request body, response codes), queue events produced or consumed, error handling and retry policy
  - **Spike tickets**: evaluation criteria matrix, output artefact (e.g. ADR), timebox enforcement note
- DB schemas must include: column names and types, primary key, foreign key constraints, relevant CHECK constraints, and at least one index where appropriate
- API contracts must include: HTTP method + path, request body shape, success response code, and key error codes (409, 403, 400, etc.)
- Queue events must include: event name, producer ticket, consumer ticket(s), and payload shape
- Do not invent functionality outside the ticket's existing description; only add technical precision to what is already specified
- Do not modify the INVEST tables, story text, acceptance criteria, or any section outside `## Product Backlog`

**Output:** `LTI-JCT/UserStories-JCT.md` — `**Technical Spec:**` block appended inline after each TK-NNN ticket's points/priority line

**Opinion:**
> Revisando la documentación, faltaba añadir una descripción técnica a las tareas, no muy detalladas pero al menos tener una referencia en cada una de las decisiones técnicas que se tomaron en los ADRs de la tarea anterior

---
