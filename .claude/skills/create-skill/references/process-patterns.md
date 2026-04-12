# Process Skill Structural Patterns

Derived from analysis of 10 skills in EveryInc/compound-engineering-plugin (ce-brainstorm, ce-plan, ce-debug, ce-compound, ce-compound-refresh, ce-ideate, ce-demo-reel, agent-native-audit, agent-native-architecture, andrew-kane-gem-writer).

## Standard Phase Structure

Process skills organize as numbered phases. Not every phase below is required -- include only what the workflow needs.

### Phase 0: Resume, Assess, and Route (universal)
Every process skill should open with Phase 0. Three responsibilities:

1. **Resume detection.** Check for prior work. If the user has an existing artifact from a previous session (a brainstorm doc, a plan file, a debug session), offer to resume rather than starting fresh. Check by scanning the expected output directory for recent files matching the skill's output pattern.

2. **Domain/scope classification.** Determine the scope of the work from the user's input. Common tiering: Lightweight / Standard / Deep (or equivalent). Classify from signals in the input, present the classification, let the user override. Different tiers gate different behaviors throughout subsequent phases.

3. **Routing.** If the user's request does not match this skill, redirect to the correct one. If the request is ambiguous, surface the ambiguity and ask one clarifying question.

### Phase 1: Gather Context
Research phase. Dispatch sub-agents for parallel information gathering. Common agents:
- Codebase scanner (always)
- Institutional knowledge reader (docs/solutions/, AGENTS.md, CLAUDE.md)
- External research (conditional on domain novelty)
- Slack/communication context (opt-in only)

Phase 1 should consolidate all research into a summary before proceeding. The model should not carry raw research output forward -- synthesize first.

### Phase 2-N: Core Workflow
The domain-specific phases. Structure varies by skill. Common patterns:

- **Investigation phases** (ce-debug Phase 1-2): hypothesize, test, trace, narrow
- **Creative phases** (ce-brainstorm Phase 2): diverge, then converge
- **Construction phases** (ce-plan Phase 3-4): structure, populate, write
- **Classification phases** (ce-compound-refresh Phase 2): categorize inputs into action types

### Final Phase: Close and Handoff
Every process skill should end with:
1. Structured output (template-based summary of what was done)
2. Handoff options (what the user can do next -- including invoking other skills)
3. File write (if the skill produces an artifact)

## Heading Depth Conventions

| Level | Used for |
|-------|----------|
| H1 | Skill title (one per document) |
| H2 | Major sections: Core Principles, Execution Flow, Phase N, Output |
| H3 | Sub-phases within a phase, named decision points |
| H4 | Steps within sub-phases, individual agent specs, conditional branches |
| H5 | Rare. Use only for deeply nested decision trees (confidence checks, scoring rubrics) |

The dominant depth is H4 (5/10 Compound skills). H5 appeared once (ce-plan confidence-check subsections).

## Phase Numbering Conventions

- Integer phases (0, 1, 2, 3, 4, 5) for the original design
- Sub-phases (0.1, 0.2, 1.1, 1.2) for steps within a phase
- Letter suffixes (0.1b, 1.1b) for classification/routing steps inserted between existing steps
- Non-integer phases (1.5, 1.75) indicate post-design insertions. These work but signal the skill has grown organically. Consider renumbering if the skill is being rewritten.

## Agent Dispatch Patterns

### Parallel research agents
Multiple agents scan different data sources simultaneously. Each returns findings to the orchestrator. No agent writes files.

```
Phase 1: Launch in parallel:
  - Context Analyzer (reads codebase)
  - Learnings Researcher (reads docs/solutions/)
  - Issue Intelligence Analyst (reads issue tracker, conditional)
Wait for all to complete before Phase 2.
```

### Sequential write agents
Agents that modify files run one at a time. Rationale: each write agent may need significant context, and parallel writes risk conflicts.

### Read-only investigation agents
Explicitly constrained: "Investigation subagents must not edit files, create successors, or delete anything." State the constraint in the agent dispatch section, not just in the agent's own instructions.

### Conditional review agents
Triggered by detected signals (problem_type, technology stack, risk level). Define the trigger condition inline:

```
If problem_type is performance_issue -> dispatch performance-oracle
If problem_type is security_issue -> dispatch security-sentinel
If detected stack includes Ruby/Rails -> dispatch rails-reviewer
```

### Model tier specification
Specify which model tier runs each agent:
- Cheap model (haiku): quick context scans, file discovery
- Mid-tier model (sonnet): synthesis, analysis, review
- Frontier model: only when the agent's task requires complex reasoning

## Lazy-Loading Enforcement

For process skills, reference files should be loaded at the phase that needs them, not at skill start. Two enforcement levels:

**Implicit (adequate for most cases):**
> Read `references/handoff.md` for the closing workflow.

The reference is mentioned at the point of use. The model reads it when it reaches that instruction.

**Explicit (for large reference files or destructive skills):**
> Read `references/deepening-workflow.md` for the confidence-gap scoring rubric. Do not load this file before Phase 5.3 gate passes.

The explicit form adds a prohibition. Use it when:
- The reference file exceeds 2,000 tokens
- Loading it prematurely would waste context on a branch that may not execute
- The reference file contains instructions that could interfere with earlier phases

## Interaction Design

### Blocking questions
Use the platform's blocking question tool to pause execution and get user input. Name all platform variants:
- Claude Code: `AskUserQuestion`
- Codex: `request_user_input`
- Gemini: `ask_user`

If no question tool is available, present the question as text and wait for the user's reply.

### One question at a time
Never ask multiple questions in a single turn. Each question should be specific enough to answer in one sentence.

### Scope-differentiated interaction
Different scope tiers should produce different interaction density:
- Lightweight: minimal questions, fast path
- Standard: moderate questions at key decision points
- Deep: thorough questions, more sub-agent research, longer review cycles

## Drift Prevention

Process skills must account for model drift -- the tendency to shortcut procedures under perceived time pressure. Countermeasures observed in high-quality skills:

1. **Principle repetition.** Restate core constraints at the decision points where they matter most. ce-debug repeats "investigate before fixing" at Phase 2 and Phase 3 entry. This is not redundant -- it is deliberate anti-drift design.

2. **Escalation tables.** When the model gets stuck (failed hypotheses, failed fix attempts), provide a structured decision table mapping symptoms to next moves. Do not leave the model to improvise when stuck.

3. **"Do not skip" constraints.** Explicitly prohibit skipping phases or combining steps: "Do NOT pre-select a mode. Do NOT skip this prompt."

4. **Causal chain gates.** Require the model to explain its reasoning before acting: "Do not propose a fix until the full causal chain is explained." This forces the model to verify its own reasoning.

## Description Field Patterns

Process skill descriptions follow a different formula than capability skills:

> [Primary action verb] [what]. Use when [3-5 trigger conditions with example phrases]. Also use when [secondary conditions]. For [redirects], prefer [other skill] first.

The description should include:
- Verbatim user phrases that trigger the skill ("debug this", "plan the implementation", "let's brainstorm")
- Conditions that redirect to other skills ("For exploratory requests, prefer ce:brainstorm first")
- Scope boundaries (what this skill does NOT handle)

## Quality Signals for Process Skills

A process skill scores 5/5 specificity when:
- Every phase has explicit entry and exit conditions
- Decision points use tables or enumerated conditions, not prose heuristics
- Agent dispatch specifies: role, model tier, dispatch condition, and return format
- Constraints are stated at the point of decision, not only at the top
- Output templates define exact fields with placeholder notation
- The skill can be followed mechanically without requiring model judgment beyond documented decision points

A process skill scores 4/5 when it has most of the above but leaves some decision points open to model judgment, or uses vague framing ("explore approaches") without enumerating what exploration means concretely.
