# Claude Instructions

## Skills

Invoke these with the `Skill` tool or by typing `/skill-name`.

| Skill | When to use |
|-------|-------------|
| `prd-generator` | Create or update a Product Requirements Document |
| `user-story-writer` | Write or refine individual user stories |
| `story-map-generator` | Generate a Jeff Patton user story map |
| `estimate-effort` | Estimate stories using Planning Poker (Fibonacci) + MoSCoW |
| `ticket-writer` | Break user stories into sprint tickets |
| `write-meta-prompt` | Create a metaprompt for a subagent task |

---

## Subagents

Launch a subagent via the `Agent` tool when a task requires reading files and producing a structured output autonomously. Pass the metaprompt content as the prompt.

| Subagent | Role | Trigger |
|----------|------|---------|
| Product Owner | Reads PRD and existing artifacts to generate epics, user stories, and story maps | When asked to create or refine backlog items from a PRD |
