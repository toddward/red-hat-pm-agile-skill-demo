# PM Agile Skill Demo

A working demo of how a project manager uses **Cursor** as an orchestration layer with the **Red Hat Agile Skill** to pull scattered project artifacts into a rigorous, value-driven agile plan.

> This is a demo — not a production tool. It exists to show the workflow on a realistic body of artifacts.

## The Scenario

A single mid-sized Red Hat consulting engagement — the *Hartwell Logistics × OpenShift Platform Modernization* — captured in `artifacts/`:

- **21** email PDFs across SoW negotiation, kickoff, and a mid-flight hardware pivot
- **2** long-form meeting transcripts (kickoff + replan)
- **1** living roadmap PDF (already on revision two)

The premise: the real plan is *trapped* across these artifacts. Decisions live in thread #14, scope pivots surface on transcript page 8, and "done" gets fuzzy. The demo shows how a PM uses the skill to aggregate that signal and produce structured Epics, Stories, and Tasks — each with Acceptance Criteria, Definition of Done, and an intrinsic value statement.

## What's in the Repo

- `artifacts/` — the raw inputs (emails, transcripts, roadmap)
- `.claude/skills/red-hat-agile-skill/` — the skill the demo exercises
- `docs/` — the slide deck (`index.html` / `index.md`) walking through the narrative

## Running the Demo

Open the project in Cursor (or Claude Code), point the agent at `artifacts/`, and invoke the **red-hat-agile-skill** to generate a backlog. The deck in `docs/index.html` narrates the why, what, and how.

---
*Todd Wardzinski · Architect · Red Hat · May 2026*
