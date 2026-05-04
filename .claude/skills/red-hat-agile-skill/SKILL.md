---
name: red-hat-agile-skill
description: >
  Generate structured agile project plans with Epics, Stories, and Tasks — each with
  Acceptance Criteria, Definition of Done, and intrinsic value statements. Uses thinking
  frameworks (First Principles, Dialectical, Six Hats) as multi-agent teams to ensure plans
  are grounded in real user needs rather than inherited assumptions. Use this skill whenever
  the user asks to create a project plan, break down a project into epics and stories, generate
  a backlog, plan a sprint, decompose requirements into agile artifacts, write acceptance
  criteria, define done, or wants to understand the value of their work items. Also trigger
  when users say things like "plan this project", "create stories for", "break this into
  tasks", "what epics do we need", "build me a backlog", "write acceptance criteria",
  "define done for", or "help me plan this feature". Even if the user doesn't explicitly
  say "agile" — if they're asking for structured work decomposition with clear deliverables,
  this skill applies.
---

# Red Hat Agile Skill

Generate rigorous agile project plans where every item — Epic, Story, Task — has clear
Acceptance Criteria, a Definition of Done, and an articulated intrinsic value. The process
uses structured thinking frameworks to ensure the plan is grounded in real needs, not
inherited assumptions or wishful thinking.

## Why This Exists

Most agile plans fail in one of four ways:
1. **Assumption inheritance** — Stories decompose what was asked for, not what's actually needed
2. **Blurry acceptance** — "This story works" is never defined in testable terms, so QA and dev disagree mid-sprint
3. **Missing "done"** — Teams argue about completeness because DoD was vague or absent
4. **No independent value** — Items only make sense as part of a chain, making prioritization impossible

This skill addresses all four by running the project vision through structured thinking
before any decomposition begins, and by treating Acceptance Criteria (per-story) and
Definition of Done (universal) as distinct artifacts.

## Process Overview

Three phases, each using a different thinking framework adapted for agile planning:

```
Project Vision
      |
      v
Phase 1: DISCOVERY (First Principles)
  Strip to fundamental truths → Build epic structure from bedrock
      |
      v
Phase 2: ELABORATION (Dialectical per Epic)
  Advocate story breakdown → Challenge completeness → Integrate with AC + DoD + value
      |
      v
Phase 3: VALIDATION (Six Hats — abbreviated)
  Facts → Risks → Value → Gut check → Final plan
      |
      v
Agile Project Plan
  Epics > Stories > Tasks
  Each with DoD + Intrinsic Value
```

---

## Before You Begin

### Gather Context

Before running the frameworks, collect this from the user (ask if not provided):

1. **Project Vision** — What are we building and why? (1-3 sentences is fine)
2. **Target Users** — Who benefits from this?
3. **Known Constraints** — Budget, timeline, technology, regulatory, team size
4. **Success Criteria** — How will we know this project succeeded?
5. **Existing Context** — Any prior work, documents, or decisions already made

If the user gives you a brief prompt like "plan a customer portal", that's enough to start —
use the Discovery phase to flesh out the rest. Don't block on having perfect inputs.

---

## Phase 1: Discovery (First Principles)

**Goal:** Strip the project vision to fundamental user needs and business truths, then
build an epic structure from only those truths.

**Why this matters:** If you skip this and jump straight to "what epics do we need?",
you'll inherit every assumption baked into the original description. First Principles
forces you to ask "what do users actually need?" before "what should we build?"

Read `references/discovery-agents.md` for agent prompts and orchestration.

### Agent Chain

```
Project Vision + Constraints
        |
        v
  Vision Archaeologist → Fundamental truths + assumption map
        |
        | truths ONLY (no original vision description)
        v
  Scope Architect → Epic structure from bedrock truths
        |
        | both original + reconstruction
        v
  Coverage Evaluator → Validated epic list with gap analysis
```

### Information Barrier (Critical)

The Scope Architect must NOT see the original project vision or description. It receives
ONLY the fundamental truths from the Archaeologist. This prevents anchoring — the epic
structure should emerge from user needs, not from how the project was described.

### Phase 1 Output

A validated list of Epics, each with:
- A clear scope boundary
- The fundamental truths it addresses
- A preliminary intrinsic value statement

---

## Phase 2: Elaboration (Dialectical per Epic)

**Goal:** For each Epic, generate Stories and Tasks through structured debate. Each story
gets **Acceptance Criteria** (story-specific, testable behaviors), compliance with the
**project-level Definition of Done** (universal quality bar), and an intrinsic value
statement.

**Why this matters:** A single pass at story decomposition tends to produce either too-thin
slices (tasks disguised as stories) or too-thick slices (epics disguised as stories). It
also tends to blur acceptance — teams conflate "this specific story's behavior is correct"
(AC) with "this story meets our team's quality bar" (DoD), leading to sprint-time fights
about what "done" means. The dialectical process catches all three failure modes.

Read `references/decomposition-agents.md` for agent prompts and orchestration.

### Agent Chain (runs once per Epic)

```
Epic Definition + Fundamental Truths + Project DoD
        |
        v
  Story Advocate → Proposed stories with AC + DoD-fit + value
        |
        v
  Story Challenger → Critique: INVEST, AC gaps, DoD-fit gaps, value gaps
        |
        v
  Story Integrator → Final stories with refined AC + value (DoD applies universally)
        |
        v
  Task Decomposition → Tasks per story with completion criteria
```

### INVEST Criteria (enforced by the Challenger)

Every Story must be:
- **I**ndependent — deliverable without requiring other stories to be done first
- **N**egotiable — describes the what, not the how
- **V**aluable — delivers intrinsic value (see Value Framework below)
- **E**stimable — team can reasonably estimate effort
- **S**mall — completable within a single sprint
- **T**estable — DoD is verifiable and unambiguous

### Phase 2 Output

For each Epic:
- Stories with **Acceptance Criteria** (Given/When/Then), intrinsic value, and a DoD-fit check
- Tasks per story with completion criteria
- Dependency map (which stories/tasks block others)

A **project-level Definition of Done** (the universal quality bar applied to every story)
is defined once, near the top of the plan — not repeated per story.

---

## Phase 3: Validation (Six Hats — Abbreviated)

**Goal:** Stress-test the complete plan from four perspectives before delivering it.

**Why this matters:** Phases 1 and 2 focus on structure and correctness. Phase 3 asks
"will this actually work in the real world?" — surfacing risks, confirming value, and
checking stakeholder readiness.

Read `references/validation-agents.md` for agent prompts and orchestration.

### Agent Chain

```
Complete Plan (Epics + Stories + Tasks)
        |
        v
  White Hat → Completeness check: gaps, missing requirements, data quality
        |
        v
  Black Hat → Risk assessment: what threatens this plan?
        |
        v
  Yellow Hat → Value validation: does the total value justify the effort?
        |
        v
  Red Hat → Stakeholder gut check: will the org accept this?
        |
        v
  Blue Hat → Synthesis: final adjustments + delivery recommendation
```

### Phase 3 Output

- Risk register with mitigations
- Value summary (total intrinsic value across all items)
- Stakeholder readiness assessment
- Recommended iteration order (which epics/stories to tackle first)

---

## Intrinsic Value Framework

Every Epic, Story, and Task should articulate its intrinsic value — the worth it delivers
independently, even if no other item in the plan existed.

Read `references/output-templates.md` for the full value framework and templates.

### Value Dimensions

| Dimension | Question It Answers | Example |
|-----------|-------------------|---------|
| **User Impact** | How does this directly improve a user's life? | "Users can reset passwords without calling support" |
| **Business Impact** | What business outcome does this enable? | "Reduces support tickets by ~30%" |
| **Technical Impact** | What capability or quality does this create? | "Establishes the authentication foundation other features build on" |
| **Learning Impact** | What uncertainty does this reduce? | "Validates that our SSO integration approach works with the customer's IdP" |

### Value Levels by Item Type

- **Epic Value** — Strategic: answers "why does this capability matter?"
- **Story Value** — Tactical: answers "what specific benefit does shipping this deliver?"
- **Task Value** — Operational: answers "why is this work necessary?" (tasks may reference their parent story's value when they don't carry independent value)

Tasks are the one level where intrinsic value can be inherited — a database migration task
may not have standalone user value, but it should still articulate why it's necessary
("enables the new schema required for feature X").

---

## Acceptance Criteria & Definition of Done Framework

Acceptance Criteria (AC) and Definition of Done (DoD) are **two distinct artifacts**. Teams
that conflate them end up arguing during sprint review about whether a story is "done,"
because there's no shared contract for either what *this* story must do or what *every*
story must satisfy.

### The Distinction

| | Acceptance Criteria (AC) | Definition of Done (DoD) |
|---|---|---|
| **Scope** | Specific to *this* story | Universal — applies to *every* story |
| **Answers** | "Is this story's behavior correct?" | "Has this story met our quality bar?" |
| **Form** | Given/When/Then scenarios (preferred) or numbered testable statements | Checklist of team standards |
| **Owned by** | PO / BA, reviewed with QA | The team (engineering + QA + ops) |
| **Changes per story?** | Yes — every story has its own | No — set once per team/project, revisited rarely |
| **Example** | "Given a locked account, when the user submits valid credentials, then the system returns 403 with message 'Account locked. Try again in 15 minutes.'" | "All unit tests pass in CI; code reviewed by ≥1 teammate; feature flag configured; docs updated." |

A story is **accepted** when its AC pass. A story is **done** when it's accepted AND the
project DoD is satisfied.

### Acceptance Criteria Quality Checklist

Good AC items answer YES to all of these:
- Written from the user/system perspective (observable behavior, not implementation)
- Covers the happy path, error paths, and at least one boundary/edge case
- Unambiguous — one interpretation only
- Testable — a QA engineer can write an automated or manual test directly from it
- Scoped to this story — doesn't drag in behaviors that belong to another story

**Preferred format: Given / When / Then** (Gherkin-style)
```
Scenario: User logs in with valid credentials
  Given a registered user with email "user@example.com" and password "correct-pw"
  When they submit the login form
  Then they receive a JWT with a 24-hour expiry
  And they are redirected to /dashboard
```

Plain testable statements are also acceptable when Given/When/Then feels forced (e.g., for
infrastructure stories): "The migration script runs idempotently — re-running it produces
no schema changes and no data loss."

### Project Definition of Done

Defined *once* for the whole plan, near the top. Every story inherits this DoD implicitly.
Typical items:

- Code reviewed and approved by ≥1 teammate
- Unit tests present; CI pipeline passes (lint, test, build, security scan)
- Integration test covers the primary flow
- User-facing changes documented (release notes, help docs, runbook as applicable)
- Deployed to staging; smoke test passes
- Feature flag configured when rollout is risky
- No new accessibility or security regressions introduced

Teams may extend this — but the list should be **short, stable, and universally applicable**.
If a criterion only applies to *some* stories, it belongs in AC, not DoD.

### Bad vs Good AC Examples

| Bad (blurs AC and DoD, or is vague) | Good (clean AC) |
|---|---|
| "User authentication works" | "Given valid email+password, when the user submits, then they receive a JWT and land on /dashboard. Given invalid credentials, then the response is 401 with message 'Invalid email or password.' Given 5 failed attempts in 15 min, then the account is locked for 15 min and a 403 is returned." |
| "Tests pass and code is reviewed" | *(this is DoD, not AC — move it to the project DoD)* |
| "Performance is acceptable" | "The login endpoint returns a response within 200ms (P95) under a load of 100 concurrent requests, validated by the load-test suite." |

---

## Output Format

The final deliverable is a structured agile project plan. Use this hierarchy:

Read `references/output-templates.md` for the complete templates with all fields.

### Summary Structure

```markdown
# Project Plan: [Project Name]

## Vision Summary
[2-3 sentences from Discovery phase]

## Fundamental Truths
[Numbered list from Archaeologist]

## Project Definition of Done
[The universal quality bar applied to every story in this plan. Defined once here.]
- [ ] [team standard 1]
- [ ] [team standard 2]
- ...

## Epic Overview
| # | Epic | Stories | Intrinsic Value (1-line) | Priority |
|---|------|---------|--------------------------|----------|

## Detailed Breakdown

### Epic 1: [Name]
**Intrinsic Value:** [value statement]
**Epic-Level DoD:** [rollup criteria specific to the epic — e.g., "all stories accepted, end-to-end flow demoed"]

#### Story 1.1: [Name]
**Intrinsic Value:** [value statement]

**Acceptance Criteria:**
- Scenario 1: Given... When... Then...
- Scenario 2: Given... When... Then...
- Edge case: Given... When... Then...

**DoD Fit:** [confirm the project DoD applies cleanly; note any story-specific
additions such as "also requires a data migration runbook"]

**Tasks:**
| # | Task | Completion Criterion | Estimate |
|---|------|---------------------|----------|

[...repeat for all stories and epics...]

## Validation Summary
### Risks
### Value Map
### Recommended Iteration Order
### Stakeholder Readiness
```

---

## Practical Guidance

### Scope Calibration

The depth of analysis should match the project size:

| Project Size | Discovery | Elaboration | Validation |
|-------------|-----------|-------------|------------|
| Small (1-2 sprints) | Light: skip Scope Architect, go straight from truths to stories | Single pass per epic | White + Black hats only |
| Medium (1-3 months) | Full 3-agent chain | Full dialectical per epic | All 5 hats |
| Large (3+ months) | Full chain + multi-cycle | Full dialectical + cross-epic dependency analysis | All 5 hats + recommended phasing |

### When to Stop Decomposing

- **Epics** should be deliverable in 1-3 sprints (2-6 weeks of work)
- **Stories** should be completable in a single sprint (1-2 weeks)
- **Tasks** should be completable in 1-3 days
- If a task takes longer than 3 days, it's probably a story

### Common Pitfalls

| Pitfall | How This Skill Prevents It |
|---------|---------------------------|
| Feature factory (building without purpose) | Every item must articulate intrinsic value |
| Scope creep disguised as stories | Challenger agent enforces INVEST + traces back to fundamental truths |
| "Done" means different things to different people | Project DoD is defined once and universal; per-story AC is testable and story-scoped — both checked by the Challenger |
| Analysis paralysis | Scope calibration table right-sizes the process |
| Dependency spaghetti | Stories must be Independent (INVEST); dependencies are explicitly mapped |

---

## Reference Files

Read the appropriate reference file BEFORE spawning agents:

| File | Contents | When to Read |
|------|----------|-------------|
| `references/discovery-agents.md` | Vision Archaeologist, Scope Architect, Coverage Evaluator prompts | Phase 1: before decomposing the project vision |
| `references/decomposition-agents.md` | Story Advocate, Story Challenger, Story Integrator, Task Decomposer prompts | Phase 2: before elaborating each epic |
| `references/validation-agents.md` | White, Black, Yellow, Red, Blue hat prompts adapted for plan validation | Phase 3: before validating the complete plan |
| `references/output-templates.md` | Complete templates for Epics, Stories, Tasks + Value Framework details | When producing the final output |
