# Red Hat Agile Skill

A Claude Code skill that generates structured agile project plans with **Epics, Stories, and Tasks** — each with a rigorous **Definition of Done** and articulated **Intrinsic Value**. The skill uses structured thinking frameworks as multi-agent teams to ensure plans are grounded in real user needs rather than inherited assumptions.

## The Problem This Solves

Most agile plans fail in predictable ways:

1. **Assumption inheritance** — Stories decompose what was asked for, not what's actually needed. Teams build the described solution rather than solving the underlying problem.
2. **Vague "done"** — Without specific, measurable Definitions of Done, teams argue about completeness and stakeholders lose trust.
3. **No independent value** — Work items only make sense as part of a chain, making prioritization, descoping, and trade-off decisions impossible.

This skill addresses all three by running the project vision through structured thinking frameworks **before** any decomposition begins.

## How It Works: Three Phases, Three Thinking Frameworks

The skill orchestrates a three-phase process, each powered by a different thinking framework adapted from the [Thinking Frameworks Skill](https://github.com/toddward/claude-skills-playground/tree/main/thinking-frameworks):

### Phase 1: Discovery (First Principles Thinking)

**Goal:** Strip the project vision to fundamental user needs and business truths, then build the epic structure from bedrock.

Three agents run sequentially:

| Agent | Role | Information Barrier |
|-------|------|-------------------|
| **Vision Archaeologist** | Digs through stated requirements using "Why does this matter?" chains to separate fundamental truths from inherited assumptions | Sees everything |
| **Scope Architect** | Builds the epic structure from ONLY the fundamental truths | Cannot see the original project vision (prevents anchoring bias) |
| **Coverage Evaluator** | Compares the reconstruction against the original to find gaps AND inherited bloat | Sees both original and reconstruction |

The information barrier between the Archaeologist and Architect is critical — it forces the epic structure to emerge from actual user needs rather than from how the project was described.

### Phase 2: Elaboration (Dialectical Thinking)

**Goal:** For each Epic, generate Stories and Tasks through structured debate.

Four agents run per Epic:

| Agent | Role |
|-------|------|
| **Story Advocate** | Proposes the story breakdown with DoD and intrinsic value statements |
| **Story Challenger** | Tests every story against INVEST criteria, challenges DoD completeness, and scrutinizes value claims |
| **Story Integrator** | Resolves the tension between Advocate and Challenger, producing the final refined story set |
| **Task Decomposer** | Breaks each finalized story into 1-3 day implementation tasks with DoD |

The dialectical process (thesis → antithesis → synthesis) catches both under-decomposition (epics disguised as stories) and over-decomposition (tasks disguised as stories).

### Phase 3: Validation (Six Thinking Hats)

**Goal:** Stress-test the complete plan from multiple perspectives before delivery.

Five hats run sequentially, each building on the previous:

| Hat | Perspective | What It Checks |
|-----|------------|---------------|
| **White** (Facts) | Completeness | Requirements coverage, DoD quality, estimation confidence, information gaps |
| **Black** (Caution) | Risk | Scope risks, dependency risks, technical risks, execution risks, value risks |
| **Yellow** (Value) | Opportunity | Value realism, value distribution, value-effort ratio, MVP identification |
| **Red** (Intuition) | Stakeholders | Team energy, stakeholder alignment, organizational friction, the elephant in the room |
| **Blue** (Process) | Synthesis | Plan adjustments, iteration order, confidence assessment, final recommendation |

## About the Thinking Frameworks

This skill embeds three thinking framework methodologies, each designed to surface different kinds of insight:

### First Principles Thinking
Originally developed by stripping problems to irreducible truths (think: physics constraints, regulatory requirements, mathematical certainties) and rebuilding from scratch. In this skill, it's adapted to strip *project visions* to fundamental *user needs* and rebuild the epic structure from those needs alone. The information barrier — where the Architect never sees the original description — is borrowed directly from the First Principles framework and prevents the most common planning failure: unconsciously reproducing the structure someone described rather than the structure users need.

### Dialectical Thinking
A structured debate format: Advocate builds the strongest case, Challenger systematically dismantles it, Integrator transcends both into something stronger than either. In this skill, it's applied per-Epic to stress-test story decomposition. The Advocate proposes stories, the Challenger tests them against INVEST criteria and DoD quality standards, and the Integrator produces the final set with all issues resolved.

### Six Thinking Hats (de Bono)
Parallel thinking where each "hat" represents a different cognitive mode. Rather than everyone arguing at once, each perspective gets its own dedicated analysis pass. In this skill, it's used for plan validation — ensuring the complete plan is examined from factual, risk, value, stakeholder, and synthesis perspectives before delivery.

## Intrinsic Value Framework

Every Epic, Story, and Task articulates its intrinsic value across four dimensions:

| Dimension | Question | Example |
|-----------|----------|---------|
| **User Impact** | How does this directly improve a user's life? | "Users can reset passwords without calling support" |
| **Business Impact** | What business outcome does this enable? | "Reduces support tickets by ~30%" |
| **Technical Impact** | What capability or quality does this create? | "Establishes the authentication foundation" |
| **Learning Impact** | What uncertainty does this reduce? | "Validates SSO integration works with customer's IdP" |

Not every item will score on all four dimensions. Tasks often reference their parent story's value. But if an item scores on zero dimensions, it probably shouldn't exist.

## Definition of Done Quality

Every DoD item must pass four tests:

- **Observable** — Can someone unfamiliar with the work verify it?
- **Unambiguous** — Is there exactly one way to interpret this?
- **Measurable** — Can we check it without subjective judgment?
- **Complete** — Does it include edge cases, not just the happy path?

## Output

The skill produces a structured agile project plan containing:

- Executive Summary
- Fundamental Truths (the bedrock needs the plan is built on)
- Epic Overview with dependency graph
- Detailed breakdown: every Epic → Story → Task with DoD and intrinsic value
- Validation Summary: risk register, value map, MVP subset, recommended iteration order
- Stakeholder readiness assessment
- Open questions for the user

## Skill Structure

```
red-hat-agile-skill/
├── SKILL.md                              # Main skill: process, framework selection, orchestration
├── README.md                             # This file
└── references/
    ├── discovery-agents.md               # Phase 1: First Principles agent prompts
    ├── decomposition-agents.md           # Phase 2: Dialectical agent prompts
    ├── validation-agents.md              # Phase 3: Six Hats agent prompts
    └── output-templates.md               # Templates + Value Framework details
```

## Usage

Once installed, the skill triggers when you ask Claude Code to:

- "Plan this project"
- "Break this into epics and stories"
- "Create a backlog for [project]"
- "Generate a project plan with definition of done"
- "What stories do we need for [feature]?"
- Any request for structured agile work decomposition

## Demo Walkthrough

A complete worked example lives in the [`pm_agile_skill_demo`](../../../) repository — a realistic Red Hat consulting engagement (OpenShift platform modernization at "Hartwell Logistics") with all the messy inputs a PM actually receives.

### What's in the demo

The `artifacts/` directory contains:

- **21 email PDFs** — SoW negotiation, kickoff scheduling, certification-voucher confirmations, and a mid-flight hardware pivot
- **2 meeting transcripts** — the May 4 kickoff and the May 21 hardware-pivot replan
- **1 roadmap PDF** — the current plan (already on revision two), with five phases and four cross-cutting workstreams

This is the kind of dispersed evidence a PM accumulates over the first six weeks of any non-trivial engagement. It's deliberately messy: decisions live in email thread #14, scope rationale lives in transcript page 8, and the roadmap is already out of sync with both.

### Running the walkthrough

1. **Open the demo repo in Cursor** (or Claude Code). The skill auto-discovers from `.claude/skills/red-hat-agile-skill/`.

2. **Ask Claude to plan the engagement:**

   ```
   Read the artifacts/ directory and build me a structured agile plan
   for the Hartwell engagement using the Red Hat Agile Skill.
   ```

3. **Watch the three phases run:**
   - **Phase 1 (First Principles)** surfaces the fundamental truths — e.g., that the real user need is "Hartwell's developers can self-serve the platform without filing tickets," not "stand up OpenShift on bare metal."
   - **Phase 2 (Dialectical)** decomposes each Epic into Stories. The Challenger catches places where the original roadmap conflated infrastructure work with developer enablement.
   - **Phase 3 (Six Hats)** validates the complete plan. The Black hat flags the hardware-pivot scope risk; the Red hat names the elephant in the room (whether Sofia is actually ready to own day-2 ops).

4. **Review the output.** Every Epic, Story, and Task carries a Definition of Done and an Intrinsic Value statement across the four dimensions.

### Why Cursor matters here

Cursor (or any agentic IDE) is the orchestration layer that makes this workflow tractable for a PM. The artifacts live in the side panel, the conversation with Claude lives in the chat, and the resulting plan lands as a file in the repo — all in one window. The PM never leaves the surface they're already working in to switch to a separate planning tool.

### Companion deck

`docs/index.html` in the demo repo is a self-contained HTML presentation that walks through what the demo is and why PM aggregation work is the most leverage-rich place to apply structured AI. Open it in any browser.

### Adapting it to your engagement

Drop your own emails, transcripts, and planning docs into `artifacts/` and re-run the same prompt. The skill is project-agnostic — the Hartwell scenario is just the worked example.

## Running Test Cases

The skill includes a test suite in `evals/evals.json` with three scenarios covering different project sizes:

| Test | Scenario | Project Size | Exercises |
|------|----------|-------------|-----------|
| **insurance-portal** | Customer self-service portal for an insurance company | Medium (3 months) | Full 3-phase process |
| **ecommerce-notifications** | Real-time notifications for an e-commerce platform | Small (2 sprints) | Abbreviated process |
| **hr-migration** | Legacy HR system migration across 12 countries | Large (6 months) | Full process with deep discovery + all 5 hats |

### Running with the Skill Creator

If you have the [skill-creator](https://github.com/anthropics/claude-code-plugins) plugin installed, you can run the full evaluation loop:

1. **Run all test cases** — The skill-creator spawns agents for each eval prompt (with-skill and baseline), saves outputs to the workspace directory, and launches a review viewer.

2. **Review results** — Compare with-skill outputs against baselines to verify the thinking frameworks produce meaningfully better plans (more specific DoD, stronger intrinsic value statements, better risk identification).

3. **Iterate** — Adjust the skill based on feedback and re-run.

### Running Manually

You can also test the skill directly in Claude Code:

```bash
# Ask Claude Code to plan a project using the skill
claude "Plan a customer self-service portal for our insurance company. 
Customers should be able to file claims, check claim status, download 
policy documents, and update personal information. 50,000 policyholders, 
3-month timeline, Java/Spring Boot backend, React frontend."
```

The skill should trigger automatically when Claude Code detects a project planning request. Verify the output includes:

- **Phase 1 artifacts**: Fundamental truths list, assumption archaeology, validated epic structure
- **Phase 2 artifacts**: Stories with INVEST-checked DoD and intrinsic value per epic, tasks with DoD
- **Phase 3 artifacts**: Risk register, value map, recommended iteration order, stakeholder readiness
- **Every item** has a specific, measurable Definition of Done (not vague like "works correctly")
- **Every item** has an intrinsic value statement (or explicit reference to parent item's value for tasks)

### Workspace Structure

Test results are organized by iteration for comparison across skill revisions:

```
red-hat-agile-skill-workspace/
└── iteration-1/
    ├── eval-insurance-portal/
    │   ├── with_skill/outputs/plan.md
    │   └── without_skill/outputs/plan.md
    ├── eval-ecommerce-notifications/
    │   ├── with_skill/outputs/plan.md
    │   └── without_skill/outputs/plan.md
    └── eval-hr-migration/
        ├── with_skill/outputs/plan.md
        └── without_skill/outputs/plan.md
```

### What to Look For

When comparing with-skill vs without-skill outputs:

| Dimension | With Skill (expected) | Without Skill (typical) |
|-----------|-----------------------|------------------------|
| **Epic structure** | Grounded in fundamental truths, independent epics | Mirrors the original description's structure |
| **Definition of Done** | Specific, measurable, verifiable criteria with edge cases | Vague ("works correctly", "tests pass") |
| **Intrinsic value** | Four-dimension framework (user, business, technical, learning) | Generic or missing value statements |
| **Risk identification** | Structured risk register with probability, impact, mitigations | Risks mentioned in passing or absent |
| **Story quality** | INVEST-validated, dialectically stress-tested | Reasonable but unchallenged decomposition |
| **Assumption handling** | Explicitly surfaced and questioned | Inherited without examination |

## Scope Calibration

The skill scales to the project size:

| Project Size | Discovery | Elaboration | Validation |
|-------------|-----------|-------------|------------|
| Small (1-2 sprints) | Light (skip Scope Architect) | Single pass per epic | White + Black hats only |
| Medium (1-3 months) | Full 3-agent chain | Full dialectical per epic | All 5 hats |
| Large (3+ months) | Full + multi-cycle | Full + cross-epic dependency analysis | All 5 hats + phasing |
