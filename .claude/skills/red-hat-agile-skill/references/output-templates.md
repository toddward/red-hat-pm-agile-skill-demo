# Output Templates

Complete templates for the final agile project plan deliverable. Use these when
assembling the output from all three phases.

---

## Intrinsic Value Framework (Detailed)

Intrinsic value is the worth an item delivers independently — even if no other item
in the plan existed. It answers "why does this matter on its own?" rather than
"how does this contribute to the larger goal?"

### Why Intrinsic Value Matters for Agile

Without intrinsic value, agile degrades into a feature factory: teams build what's
on the list without understanding why, can't make trade-off decisions during sprints,
and stakeholders can't meaningfully prioritize. When every item has articulated
intrinsic value, the team can:

- **Re-prioritize on the fly** — if priorities shift, you know which items still matter
- **Make scope cuts without panic** — you can identify the MVP subset instantly
- **Explain "why" to stakeholders** — each item justifies its own existence
- **Motivate the team** — people do better work when they understand the impact

### Value Dimensions

| Dimension | What It Captures | Signal Words | Example |
|-----------|-----------------|-------------|---------|
| **User Impact** | Direct, tangible benefit to end users | "Users can...", "Reduces user...", "Enables users to..." | "Users can reset passwords without calling support, recovering access in <2 minutes instead of 24 hours" |
| **Business Impact** | Revenue, cost reduction, compliance, market position | "Reduces cost...", "Enables revenue...", "Achieves compliance..." | "Eliminates ~150 support tickets/month at $12/ticket = ~$1,800/month savings" |
| **Technical Impact** | Capability, quality, maintainability, performance | "Establishes...", "Enables...", "Improves..." | "Establishes the authentication foundation that all role-based features depend on" |
| **Learning Impact** | Uncertainty reduced, knowledge gained, risk validated | "Validates...", "Proves...", "Determines..." | "Validates that our SSO approach works with the customer's IdP before committing to the full integration" |

### Value by Item Level

**Epic-Level Value** (Strategic)
- Answers: "Why does this capability matter to the business?"
- Should connect to business objectives or user segments
- Example: "Secure User Identity — Enables the organization to serve authenticated users,
  unlocking all personalized features and meeting regulatory requirements for data access control."

**Story-Level Value** (Tactical)
- Answers: "What specific benefit does shipping this story deliver?"
- Should be concrete enough that you could demo it to a stakeholder
- Must hold up independently: "If we shipped ONLY this story, would someone benefit?"
- Example: "Password Reset Flow — Users locked out of their account can self-recover
  within 2 minutes, eliminating the #1 support ticket category."

**Task-Level Value** (Operational)
- Answers: "Why is this work necessary?"
- Can reference parent story's value when no independent value exists
- Should still articulate the connection: "Enables X by doing Y"
- Example: "Create user_credentials table migration — Enables the authentication
  system by establishing the schema for secure credential storage."

### Writing Good Value Statements

**The Sniff Test:** Read the value statement out loud. If it sounds like it could apply
to any project ("improves user experience", "adds functionality", "enhances the system"),
it's too vague. Rewrite with specifics.

| Vague (fails sniff test) | Specific (passes) |
|--------------------------|-------------------|
| "Improves user experience" | "Reduces checkout time from 5 steps to 2, decreasing cart abandonment" |
| "Adds important functionality" | "Customers can track orders in real-time, reducing 'where's my order?' calls by ~40%" |
| "Technical improvement" | "Migrates from polling to WebSockets, reducing server load by 60% and enabling real-time features" |
| "Reduces risk" | "Automated daily backups with verified restore process — recovery time drops from 8 hours to 30 minutes" |

---

## Acceptance Criteria vs. Definition of Done

These are two distinct artifacts, and keeping them separate is one of the things this
skill exists to enforce.

| | Acceptance Criteria (AC) | Definition of Done (DoD) |
|---|---|---|
| **Scope** | Specific to *this* story | Universal — applies to *every* story |
| **Answers** | "Is this story's behavior correct?" | "Has this story met our team's quality bar?" |
| **Form** | Given/When/Then scenarios (preferred) | Checklist of team standards |
| **Changes per story?** | Yes | No — set once, revisited rarely |

**A story is *accepted* when its AC pass. A story is *done* when it's accepted AND the
project DoD is satisfied.**

## Acceptance Criteria Templates

### Per-Story Acceptance Criteria

AC describe the specific, testable behavior this story must deliver. Prefer
Given/When/Then — it maps cleanly to test scenarios and forces the author to think in
terms of observable behavior rather than implementation.

Every story should have, at minimum:
- A happy-path scenario
- At least one error / negative-path scenario
- At least one boundary / edge-case scenario

```markdown
**Acceptance Criteria — Story [E.N]: [Title]**

*Scenario 1 — Happy path: [short name]*
  Given [context / precondition]
  When [user action or system event]
  Then [observable outcome]
  And [additional observable outcome]

*Scenario 2 — Error path: [short name]*
  Given [context — e.g., invalid input, missing permission, downstream failure]
  When [action]
  Then [observable outcome — error surface, fallback, retry, etc.]

*Scenario 3 — Edge case: [short name]*
  Given [boundary condition — empty / max / timeout / concurrent / rate-limited]
  When [action]
  Then [observable outcome]
```

**Testable-statement form** (acceptable for technical/infrastructure stories when
Given/When/Then feels forced):

```markdown
**Acceptance Criteria — Story [E.N]: [Title]**

1. The migration script is idempotent: running it twice produces zero schema changes
   on the second run and no data loss.
2. When the migration fails mid-run, the script rolls back cleanly and leaves the
   database in its pre-run state, verified by schema hash comparison.
3. The script completes within 15 minutes against a database with 10M rows of the
   affected table, measured on the staging environment hardware.
```

### AC Quality Checklist

Before accepting a set of AC, confirm:
- [ ] Happy path covered
- [ ] At least one error path covered
- [ ] At least one boundary / edge case covered
- [ ] Every scenario is observable (not "user feels satisfied" — what would you see?)
- [ ] Every scenario is unambiguous (one pass/fail interpretation)
- [ ] Every scenario is scoped to this story (no piggy-backed behavior from elsewhere)
- [ ] No implementation details leak in ("uses Redis" is a design note, not AC)

### AC Bad/Good Examples

| Bad | Good |
|---|---|
| "Login works" | "Given valid email+password, when the user submits, then they receive a JWT with a 24-hour expiry and are redirected to /dashboard." |
| "Handles errors" | "Given an email that is not registered, when the user submits, then the system returns a generic 'Invalid email or password' message (no user enumeration) and stays on /login." |
| "Performance is acceptable" | "Given 100 concurrent login requests, when they execute, then the P95 response time is below 200ms measured by the load-test suite." |
| "User auth is secure" *(also a DoD/AC confusion)* | AC: "Given 5 failed attempts in 15 minutes, when the user tries a 6th time, then the account is locked for 15 minutes and returns 403." DoD: covered universally by the project's "security scan passes" item. |

---

## Definition of Done Templates

### Project-Level DoD

Defined **once** near the top of the plan. Applies to every story. Keep it short,
stable, and universally applicable — if an item doesn't apply to every story, it
belongs in AC or a story-specific DoD addition, not here.

```markdown
**Project Definition of Done**

Every story, to be considered "done," must satisfy:

Engineering:
- [ ] Code reviewed and approved by ≥1 teammate
- [ ] Unit tests present; coverage meets team threshold ([X]%)
- [ ] Integration test covers the primary flow
- [ ] CI pipeline passes (lint, build, test, security scan) with no new warnings

Quality:
- [ ] No new accessibility regressions (WCAG 2.1 AA for UI changes)
- [ ] No new security findings above [severity threshold]
- [ ] Performance budget not regressed beyond agreed tolerance

Documentation:
- [ ] User-facing changes documented (release notes + help docs as applicable)
- [ ] Internal docs updated (runbook, architecture notes, ADRs as applicable)

Delivery:
- [ ] Deployed to staging; smoke test passes
- [ ] Feature flag configured when rollout is risky
- [ ] Monitoring/alerting in place for new or changed code paths
```

### Epic-Level DoD (Rollup)

Epic DoD is a rollup view — "this capability is complete." It typically references the
stories and adds a cross-cutting demo/acceptance moment.

```markdown
**Definition of Done — Epic: [Name]**

- [ ] All stories in this epic are accepted (AC pass) and done (project DoD satisfied)
- [ ] End-to-end flow demoed to [stakeholder group] and approved
- [ ] [Cross-cutting capability 1] operational in production
- [ ] [Cross-cutting capability 2] operational in production
- [ ] Rollback / sunset plan documented for the capability as a whole
```

### Story-Level DoD Fit

Do **not** copy the project DoD into every story. Instead, each story states one of:

```markdown
**DoD Fit:** Applies as-is — the project DoD is sufficient for this story.
```

```markdown
**DoD Fit:** Applies as-is PLUS the following story-specific additions:
- [ ] [Genuine story-specific addition — e.g., "data migration runbook reviewed
      by SRE", "a11y audit performed on new UI surface", "privacy review
      performed for new data collection"]
```

A story-specific DoD addition is justified only when it's something *this story*
uniquely requires that isn't already in the project DoD. If it applies to many stories,
promote it into the project DoD instead.

### Task-Level Completion Criterion

Tasks have a single, specific completion criterion — not AC, not DoD, just "when is
this work item finished?"

```markdown
**Task [E.N.T]: [Description]**
**Completion Criterion:** [Single specific, verifiable statement]

Examples:
- "Migration script runs successfully against staging database with 0 errors and all existing data preserved"
- "API endpoint returns 200 with correct payload for all 5 test cases in the spec; returns 400/401/404 for invalid inputs"
- "Component renders correctly at 320px, 768px, and 1440px viewports; matches approved design mockup"
- "CI pipeline passes all stages: lint, test, build, security scan"
```

---

## Complete Plan Template

Use this template to assemble the final deliverable from all three phases.

```markdown
# Agile Project Plan: [Project Name]

**Generated:** [date]
**Vision:** [1-2 sentence project vision from user]
**Target Users:** [who benefits]
**Constraints:** [key constraints in brief]

---

## Executive Summary

[3-5 sentences: what this plan delivers, how many epics/stories/tasks,
estimated total effort, recommended iteration order, and the biggest risk]

---

## Fundamental Truths

[Numbered list from the Vision Archaeologist — these are the bedrock
user needs and constraints that the entire plan is built on]

1. [Truth 1]
2. [Truth 2]
...

---

## Project Definition of Done

[Defined once. Every story inherits this DoD implicitly — stories should
reference "DoD: applies as-is" unless they need documented additions.]

**Engineering**
- [ ] Code reviewed and approved by ≥1 teammate
- [ ] Unit tests present; coverage meets team threshold
- [ ] Integration test covers the primary flow
- [ ] CI pipeline passes (lint, build, test, security scan)

**Quality**
- [ ] No new accessibility regressions (WCAG 2.1 AA for UI changes)
- [ ] No new security findings above [severity threshold]
- [ ] Performance budget not regressed beyond agreed tolerance

**Documentation**
- [ ] User-facing changes documented (release notes + help docs as applicable)
- [ ] Internal docs updated (runbook, architecture notes, ADRs as applicable)

**Delivery**
- [ ] Deployed to staging; smoke test passes
- [ ] Feature flag configured when rollout is risky
- [ ] Monitoring/alerting in place for new or changed code paths

---

## Epic Overview

| # | Epic | Stories | Tasks | Intrinsic Value (1-line) | Size | Priority |
|---|------|---------|-------|--------------------------|------|----------|

### Dependency Graph
[Visual or textual representation of epic-level dependencies]

---

## Detailed Breakdown

### Epic [N]: [Name]

**Intrinsic Value:**
- User Impact: [specific]
- Business Impact: [specific]
- Technical Impact: [specific]
- Learning Impact: [specific or N/A]
**Value Summary:** [One sentence]

**Epic-Level DoD (rollup):**
- [ ] All stories in this epic accepted (AC pass) and done (project DoD satisfied)
- [ ] [Cross-cutting criterion — e.g., end-to-end flow demoed and approved]
- [ ] [Operational readiness — e.g., runbook delivered, rollback tested]

**Fundamental Truths Addressed:** [#list]

---

#### Story [E.N]: [Title]

**Description:** [user story format or clear description]

**Intrinsic Value:**
- User Impact: [specific or N/A]
- Business Impact: [specific or N/A]
- Technical Impact: [specific or N/A]
- Learning Impact: [specific or N/A]
**Value Summary:** [One sentence]

**Acceptance Criteria:**

*Scenario 1 — Happy path: [short name]*
  Given [context]
  When [action]
  Then [observable outcome]

*Scenario 2 — Error path: [short name]*
  Given [context]
  When [action]
  Then [observable outcome]

*Scenario 3 — Edge case: [short name]*
  Given [context]
  When [action]
  Then [observable outcome]

[Add more scenarios only as needed. Use the testable-statement form instead of
Given/When/Then when the story is infrastructure/technical and G/W/T feels forced.]

**DoD Fit:** Applies as-is.
*(If genuinely needed, replace with: "Applies as-is PLUS:" and list story-specific
additions — e.g., "a11y audit on new UI surface", "privacy review for new data
collection".)*

**Size:** [S/M/L]
**Dependencies:** [story IDs or "Independent"]

**Tasks:**

| # | Task | Why Necessary | Completion Criterion | Est. | Depends On |
|---|------|--------------|---------------------|------|-----------|
| E.N.1 | [task] | [connection to value / AC scenario] | [completion criterion] | [days] | [task IDs] |
| E.N.2 | [task] | [connection to value / AC scenario] | [completion criterion] | [days] | [task IDs] |

---

[...repeat for all stories in all epics...]

---

## Validation Summary

### Risk Register
| # | Risk | Probability | Impact | Affected Items | Mitigation | Status |
|---|------|------------|--------|---------------|-----------|--------|

### Value Map
| Item | Value Score | Effort | Value/Effort | Quadrant |
[Sorted by value/effort ratio — highest first]

### Minimum Viable Plan (MVP)
[Smallest subset of stories that delivers core value]
| Story | Cumulative Value Delivered |

### Recommended Iteration Order

**Sprint 1: [Theme]**
- Stories: [list]
- Value unlocked: [what becomes possible]
- Risks addressed: [what's validated]
- Stakeholder message: [how to frame outcomes]

**Sprint 2: [Theme]**
...

### Stakeholder Readiness
[Summary from Red Hat — organizational fit, energy, concerns]

### Confidence Assessment
| Dimension | Confidence | Key Concern |
|-----------|-----------|------------|

### Open Questions
[Questions that need answers before or during execution]

---

## Appendix: Assumption Archaeology

[The full assumption map from Phase 1 — useful for future reference
when someone asks "why didn't we include X?"]

| Stated Requirement | Fundamental Truth | Unmasked Assumption |
```

---

## Formatting Guidelines

### Consistency Rules

- Use the same numbering scheme throughout: Epic N, Story E.N, Task E.N.T
  (e.g., Epic 1, Story 1.3, Task 1.3.2)
- Every DoD item starts with a checkbox `- [ ]`
- Every AC scenario uses the Given/When/Then form (or the testable-statement form
  for infra/technical stories) — never a bare checkbox
- The project DoD is defined once near the top of the plan; individual stories use
  "DoD Fit: Applies as-is" rather than repeating it
- Every value statement uses the four-dimension structure (mark N/A where applicable)
- Every dependency reference uses the item's number, not its name
- Size estimates use S/M/L for stories, hours/days for tasks

### When the Plan Is Large

For plans with more than 5 epics or 30 stories:
- Add a table of contents at the top
- Include a one-page summary before the detailed breakdown
- Consider splitting into multiple documents: overview + one per epic
- The validation summary should still be unified across all epics

### Presenting to the User

After generating the plan:
1. Present the Executive Summary and Epic Overview first
2. Ask if the high-level structure looks right before showing details
3. Offer to dive into any specific epic's stories and tasks
4. Present the Validation Summary as a decision aid, not a blocker
5. Flag the Open Questions — these need the user's input to proceed
