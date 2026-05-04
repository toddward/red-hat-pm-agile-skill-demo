# Your Plan Is Trapped Inside Twenty-One Emails.

A working demo of how a project manager uses Cursor and the Red Hat Agile Skill to pull scattered artifacts together and draft a rigorous, value-driven plan — without losing the signal in the noise.

**Project Management Demo** · May 2026
_Todd Wardzinski · Architect · Red Hat_

---

## Slide 1 — Your Plan Is *Trapped* Inside Twenty-One Emails

A working demo of how a project manager uses **Cursor** and the **Red Hat Agile Skill** to pull scattered artifacts together and draft a rigorous, value-driven plan — without losing the signal in the noise.

Tags: Cursor-Orchestrated · Multi-Source Aggregation · Definition of Done · Intrinsic Value

> Contextual notes: This deck introduces the PM Agile Skill Demo — a working example of how a project manager uses Cursor as an orchestration layer to pull scattered project artifacts (emails, meeting transcripts, roadmap PDFs) into a structured, value-driven agile plan. Tips: Arrow keys or click to navigate · Press **N** to toggle contextual notes · Use fullscreen (F11) for the cleanest view.

---

## Slide 2 — One Engagement. **Twenty-Four Artifacts.**

Below is the artifact inventory for a single Red Hat consulting engagement — the OpenShift platform modernization at Hartwell Logistics — captured in the `artifacts/` directory of this very repo.

- **21** — Email PDFs across SoW, kickoff, and a mid-flight hardware pivot
- **2** — Long-form meeting transcripts: kickoff and replan
- **1** — Living roadmap PDF, already on revision two
- **~10** — Stakeholders named across both organizations

> Contextual notes: These numbers come from a single real engagement — the **Hartwell Logistics × Red Hat OpenShift Platform Modernization** project that ships with this demo. Look in `artifacts/` and you'll see all of it: 21 numbered email PDFs, two long meeting transcripts (kickoff + the May 21 hardware-pivot replan), and the current roadmap PDF. This is what a PM's reality looks like for *one* mid-sized engagement.

**Source:** `artifacts/` directory in this demo repo · May 2026 snapshot

---

## Slide 3 — The Signal Hides In The **Last Reply**

- **Decisions live in email thread #14**, not in the roadmap. The plan ages out the moment someone hits Reply.
- **Scope pivots surface in transcript page 8.** The "why" rarely propagates to the artifact that the team actually executes from.
- **"Done" gets fuzzy.** Without explicit acceptance criteria, three engineers will agree the story is shipped and disagree about whether it works.
- **Stories don't ladder to value.** Items get prioritized by who asked loudest, not by user impact, business outcome, or learning.
- **The PM becomes the cache.** Context lives in their head. If they're on PTO, the team rebuilds it from scratch.

> Contextual notes: The cost of manual aggregation isn't time — it's **fidelity loss**. Decisions made in a Tuesday email thread get re-litigated in a Friday meeting. A scope change agreed in transcript page 14 never makes it into the roadmap. The PM ends up as a human cache, and when they're out for a week, the cache evicts.

---

## Slide 4 — The Tension

> "Project management is now ninety percent **aggregation** and ten percent allocation — but our tools were built for the opposite ratio."
>
> — The premise behind this demo

> Contextual notes: This is the tension the demo is built to resolve. Aggregation has historically been treated as administrative work — but in modern engagements it's the most leverage-rich activity a PM does. Whoever can compress dispersed artifacts into a single, auditable plan owns the outcome.

---

## Slide 5 — A PM Workspace, **Orchestrated By Cursor**

Three pieces, working together. Cursor is the surface the PM works in; Claude does the reasoning; the Red Hat Agile Skill provides the discipline.

**Layer 1 · Inputs — The artifacts/ directory**
Twenty-one emails, two transcripts, one roadmap. The same scattered evidence a PM would receive in a real engagement.

**Layer 2 · Orchestrator — Cursor**
The PM's editor. Reads the artifacts, hands them to Claude with the right skill loaded, surfaces the plan inline. No separate planning tool to switch into.

**Layer 3 · Discipline — The Red Hat Agile Skill**
Three thinking frameworks running as multi-agent teams — turning raw context into Epics, Stories, and Tasks with explicit Definition of Done and Intrinsic Value.

> Contextual notes: The demo is intentionally minimal: a directory of realistic artifacts, a Claude skill that knows how to plan, and Cursor as the orchestration surface. The Red Hat Agile Skill (in `.claude/skills/red-hat-agile-skill/`) does the heavy thinking. Cursor is the place the PM *lives* — files in the side panel, AI in the chat, plan in the editor.

---

## Slide 6 — Cursor Reads **Everything**, The PM Stays In **One Window**

**Without Cursor — Six tabs and a notes file**
The PM opens Outlook, the SoW in Acrobat, the roadmap in Lucid, the meeting recording in Zoom, Confluence, and a scratch doc. They re-type the synthesis by hand. Half the signal is lost in transit.

**With Cursor — One workspace, full visibility**
Cursor reads the entire **artifacts/** directory, holds it in the working context, hands the right slice to Claude when the skill runs, and writes the resulting plan back into the repo. The PM reviews, edits, and commits.

> Contextual notes: Cursor's role here is the part PMs underestimate. The AI does the thinking, but Cursor is what makes the workflow *tractable* — it gives the PM a single window where the source artifacts, the conversation with Claude, and the resulting plan all live side by side. PMs don't work in a single tool today; they flip between Outlook, Confluence, Jira, Slack, the SoW PDF, and a notes app. Cursor collapses that.

---

## Slide 7 — Three Phases. **Three Thinking Frameworks**

Each phase runs structured agents with deliberate information barriers, so the plan emerges from real user needs — not from how the project was originally described.

**Phase 1 · First Principles — Discovery**
Vision Archaeologist → Scope Architect → Coverage Evaluator. The Architect cannot see the original brief, which prevents inherited assumptions.

**Phase 2 · Dialectical — Elaboration**
Advocate proposes, Challenger tests against INVEST, Integrator resolves. Then a Task Decomposer breaks each story into 1–3 day units with DoD.

**Phase 3 · Six Thinking Hats — Validation**
White (facts) · Black (risk) · Yellow (value) · Red (intuition) · Blue (synthesis). The plan ships only after all five passes.

> Contextual notes: The Red Hat Agile Skill isn't a single prompt — it's a structured three-phase pipeline where each phase uses a different thinking framework as a multi-agent team. The information barrier in Phase 1 is the most important architectural decision: it forces the epic structure to emerge from actual user needs rather than from how the project was described. Full skill source: `.claude/skills/red-hat-agile-skill/SKILL.md`

---

## Slide 8 — Every Item Ladders To **Value**. Every Item Has A **Defensible "Done"**

**Dimension 1 · User Impact**
How does this directly improve a user's day? *"Hartwell developers can self-serve namespaces without a ticket."*

**Dimension 2 · Business Impact**
What outcome does this unlock? *"Hardware-pivot CO countersigned, scope risk closed."*

**Dimension 3 · Technical Impact**
What capability does this build? *"ACM hub manages both ROSA bridge and bare-metal target."*

**Dimension 4 · Learning Impact**
What uncertainty does this kill? *"Day-45 tabletop validates Sofia owns Sev-1 path."*

> Contextual notes: Every Epic, Story, and Task carries two non-negotiable artifacts: a rigorous **Definition of Done** (observable, unambiguous, measurable, complete) and an **Intrinsic Value** statement across four dimensions. If a work item scores zero on all four dimensions, it probably shouldn't exist — built-in pruning that keeps backlogs honest.

**Source:** Each Definition of Done is observable, unambiguous, measurable, and complete — covering edge cases, not just the happy path.

---

## Slide 9 — The Aggregation Tax Is Finally **Delegable**

- **Replans collapse from weeks to an afternoon.** When scope shifts mid-flight, the PM re-runs the skill against the updated artifacts and gets a refreshed plan with intact rationale.
- **"Done" stops being a debate.** Every story carries observable, measurable acceptance criteria the team can verify without the PM in the room.
- **Backlogs prune themselves.** Items that score zero on all four value dimensions get flagged for removal.
- **The PM does the work only PMs can do.** Stakeholder judgment, trade-offs, sequencing instinct. The synthesis grunt-work moves elsewhere.

> Contextual notes: The point isn't 'AI writes plans for PMs.' The point is that the aggregation tax — the work of pulling signal from twenty-one emails and two transcripts into a single coherent plan — is finally delegable. On the Hartwell engagement: the May 21 hardware pivot rewrote half the roadmap. With this workflow, that replan happens in an afternoon, not over two weeks of email threads and re-meetings.

---

## Slide 10 — Three Steps To Run The Demo **End To End**

**01 · Open the repo in Cursor**
Point Cursor at `pm_agile_skill_demo/`. The `artifacts/` directory holds the full Hartwell engagement.

**02 · Ask Claude to plan**
"Read the artifacts and build me an agile plan using the Red Hat Agile Skill." The three phases run automatically.

**03 · Review, edit, commit**
The plan lands in the repo with Epics, Stories, Tasks, DoD, and value statements. Edit anything, then commit. Re-run when scope shifts.

> Contextual notes: Everything you need to run the demo is in this repo. To point it at your own engagement: drop your emails, transcripts, and current planning docs into the `artifacts/` directory and ask Claude to run the same flow. The skill is project-agnostic.

**Source:** Skill: `.claude/skills/red-hat-agile-skill/SKILL.md` · Artifacts: `artifacts/`

---

## Slide 11 — Thank You

Todd Wardzinski · Architect · Red Hat

> Contextual notes: Thanks for walking through the demo. Open the repo in Cursor and try the workflow against the Hartwell artifacts — or against your own engagement.
