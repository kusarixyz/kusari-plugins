# Constraint Design Patterns

Derived from analysis of 27 skills across anthropics/skills and EveryInc/compound-engineering-plugin.

## Why Constraints Matter More Than Content

A skill with excellent reference content and weak constraints will produce inconsistent output. A skill with adequate reference content and strong constraints will produce consistent output. Constraints are the highest-leverage content in any skill.

The model under pressure (long context, complex task, ambiguous input) will take shortcuts. Constraints are the mechanism that prevents shortcuts from landing.

## Constraint Placement

### At point of decision (process skills)
Place the constraint at the exact location in the workflow where the model is tempted to violate it. Not at the top of the document. Not in a "Rules" section the model read 3,000 tokens ago.

From ce-debug:
> Phase 2 opens with: "Reminder: investigate before fixing. Do not propose a fix until the full causal chain is explained."
> Phase 3 opens with: "Reminder: one change at a time."

The author explicitly documents why: "They are repeated at decision points because they matter most when the pressure to skip them is highest."

### In code comments (capability skills)
Embed the constraint inside the code block where the violation would occur:

```ruby
# CRITICAL: never require Rails directly
# Rails may not be loaded yet; use on_load hook
ActiveSupport.on_load(:active_record) do
  extend GemName::Model
end
```

The constraint lives at the line of code it governs. The model reads it at the moment it would write the wrong code.

### In section titles (both types)
When a constraint defines an entire section's purpose, put it in the heading:

```markdown
### Lists (NEVER use unicode bullets)
### CRITICAL: Use Formulas, Not Hardcoded Values
```

This makes the constraint visible in the document outline. The model sees it before reading the section content.

## Constraint Language

### Absolute language
Use: "NEVER", "ALWAYS", "Do not", "Must", "Required"
Avoid: "try to avoid", "prefer not to", "consider", "generally"

Soft language gets soft compliance. The model treats "prefer not to" as a suggestion to weigh against convenience. "NEVER" is treated as a hard boundary.

### Pair with rationale
A constraint without a reason gets discarded when the model decides the situation is "different." A constraint with a reason gets respected because the model can evaluate whether the reason still applies.

Weak:
> Do not use `data_only=True`.

Strong:
> Do not use `data_only=True` -- this replaces all formulas with their cached values. If the workbook is saved afterward, the formulas are permanently destroyed.

The rationale ("permanently destroyed") makes the consequence vivid enough to override the model's inclination to take the easier path.

### Escalation tables for stuck states
When the constraint is "do not keep trying the same thing," provide an alternative. Constraints that say "stop" without saying "do this instead" create a dead end.

From ce-debug:

| Pattern observed | Diagnosis | Next move |
|---|---|---|
| Hypotheses point to different subsystems | Problem spans a boundary | Trace the data flow across the boundary |
| Evidence contradicts itself | Wrong mental model | State what you expected vs what happened; find the false assumption |
| Works locally, fails in CI | Environment difference | Diff the environments: versions, env vars, seed data |
| Fix works but prediction was wrong | Coincidental fix | Revert the fix; find the real cause |

Each row is a specific stuck-state with a specific escape route. The model does not need to improvise.

## Constraint Types

### Behavioral constraints
Control what the model does:
- "Do not ask questions by default -- investigate first"
- "Do not propose a fix until the full causal chain is explained"
- "Ask one question at a time"

### Output constraints
Control what the model produces:
- "Score format must be X/Y (percentage%)"
- "File paths must be repo-relative, never absolute"
- "No implementation code in plans"

### Scope constraints
Control what the model attempts:
- "Do NOT use for PDFs, spreadsheets, Google Docs"
- "For exploratory requests, prefer ce:brainstorm first"
- "This skill covers automation/navigation, not test assertions"

### Ordering constraints
Control when the model does things:
- "Complete all structural changes before step 5"
- "Do not load this file before Phase 2 completes"
- "WAIT for all Phase 1 subagents to complete before proceeding"

### Safety constraints
Control destructive operations:
- "Investigation subagents must not edit files, create successors, or delete anything"
- "Auto-delete only when both the implementation AND the problem domain are gone"
- "Do not overwrite uncommitted user changes without confirmation"

## Anti-Patterns in Constraint Design

### Constraint graveyard at the top
Listing all constraints in a "Rules" section at the document top. By the time the model reaches the decision point 200 lines later, the constraint has left the attention window.

Fix: state constraints at the top AND repeat them at the decision points where they apply.

### Constraint without consequence
"Avoid using X" without explaining what happens if X is used. The model has no reason to prioritize avoidance when the cost is unknown.

Fix: always state the failure mode. "Avoid using X -- it causes Y, which is not recoverable."

### Conflicting constraints
Two sections that give contradictory guidance because the skill grew organically.

Fix: when adding new constraints, search the existing document for related constraints and reconcile.

### Aspirational constraints
"Create work that looks like it took countless hours." This is unmeasurable and unfalsifiable. The model cannot verify compliance.

Fix: convert to concrete criteria. "Every element must be contained within the canvas boundaries with proper margins. Nothing overlaps."

## Measuring Constraint Density

From the analysis:
- Anthropic Skills: average ~5 explicit constraints per skill
- Compound Engineering: average ~7 explicit constraints per skill

Process skills need more constraints because they have more decision points. Capability skills need fewer constraints because the code examples are self-constraining (the WRONG/CORRECT pair is itself a constraint).

Target: at least one explicit constraint per major section (H2). If a section has no constraint, ask whether the model could produce a wrong output in that section. If yes, add a constraint. If no, the section may be unnecessary.
