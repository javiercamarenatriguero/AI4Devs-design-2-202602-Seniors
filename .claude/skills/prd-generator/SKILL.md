---
name: prd-generator
description: Generate structured Product Requirements Documents (PRDs) for software features. Use this skill when the user asks to create a PRD, write product requirements, document a feature spec, or needs a product manager-style feature specification. Triggers on requests like "write a PRD", "create product requirements", "document this feature", "feature spec for X".
metadata:
   author: Javier Camarena
   version: 1.0.0
---

# PRD Generator

Generate complete, structured PRDs for software features following a standardized template.

In 2026, a PRD serves a **dual function**:
1. **Human alignment** — ensures designers, developers, and stakeholders share the same vision and priorities.
2. **Executable specification for AI coding agents** — tools like Cursor, Claude Code, or Codex use the PRD as primary input to generate code autonomously. A vague PRD produces vague code; a structured PRD produces working features.

## Usage

Provide the following inputs:
- **Feature name**: The feature to document
- **Priority**: P0 (MVP) / P1 (post-launch) / P2 (competitive)
- **Target users**: Which user roles benefit from this feature
- **Format** (optional): `full` (default) or `one-pager` for agile contexts with high uncertainty

## Process

1. **Read context first**: Read the project's design document to understand the data model, architecture, and existing use cases.
2. **Ask before writing**: Before generating anything, interview the user with targeted questions to fill gaps. Do not assume — a PRD built on guesses is worse than no PRD. Gather at minimum:
   - What problem does this feature solve? For whom?
   - What does success look like in 90 days? (drives KPIs)
   - What is explicitly out of scope for this iteration?
   - Are there known constraints (timeline, budget, tech, compliance)?
   - Which stakeholders need to sign off?
   - Will this PRD be used as input for an AI coding agent? (affects level of phase detail needed)
3. **Iterate if needed**: If answers raise new questions, ask them. Do not proceed until the scope and goals are unambiguous.
4. If the user requests a **one-pager**, generate a lightweight brief (problem, KPIs, key user stories, launch notes) instead of the full template.
5. Generate the PRD following the template in [references/prd-template.md](references/prd-template.md).
6. Save the PRD as `PRDs/PRD-NNN-feature-slug.md` (auto-increment the number based on existing PRDs in the folder).

## Writing Guidelines

1. **Be specific**: Use concrete numbers for metrics and targets, not vague terms like "fast" or "scalable".
2. **Stay product-level**: Describe WHAT the system does and WHY, not HOW it is implemented. Avoid DB field names, API endpoints, infrastructure technologies (Redis, SQS, S3, etc.), or data schemas — those belong in the technical design phase, after the PRD.
3. **AI-first mindset**: Where applicable, describe how AI enhances the feature from the user's perspective.
4. **Write acceptance criteria as testable assertions**: Use the Gherkin format below — in plain language, without implementation details. Each scenario gets a sequential number and a descriptive name. `Then` can have multiple bullet points for compound outcomes. **Max 3–5 scenarios per requirement** — more is a signal to split.
   ```
   Scenario 1: [descriptive name]
   Given [precondition]
   When [action]
   Then
   - [expected result 1]
   - [expected result 2]
   ```
5. **Keep scope tight**: A PRD covers ONE feature, not an entire module.
6. **Number everything**: User stories (US-NNN), functional requirements (FR-NNN), risks — all get IDs for traceability.
7. **Dependencies = features, not infrastructure**: List only feature-level or external service dependencies (e.g., "Interview Scheduling feature"), never infrastructure components (e.g., Redis, AWS SES).
8. **NFRs without technology**: State performance targets as numbers (e.g., "< 500ms"), but do not specify which technology achieves them.
9. **Explicit non-goals are mandatory**: AI coding agents cannot infer implicit limits. Always state what the feature must NOT do or include in this iteration.
10. **Phase the implementation plan for agent consumption**: Structure the Release Plan as sequential phases, each with clear input dependencies (what must exist before this phase starts) and a verifiable output (what "done" looks like). This lets an agent execute one phase at a time without ambiguity.

## Output

Save the generated PRD file and inform the user of the path. If a design document exists, suggest updating its table of contents to reference the new PRD.
