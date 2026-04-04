---
description: Evaluate a business idea, product plan, or feature through a panel of investor personas
argument-hint: <idea description or file path>
disable-model-invocation: false
---

Evaluate the user's idea through a panel of seven investor personas, each running as a parallel subagent.

## Input

The user provided: `$ARGUMENTS`

This is either:
- **File path**: a path to a document containing the idea. Detect this by checking whether the argument is a single token that looks like a filesystem path (starts with `/`, `./`, `../`, or `~`, or ends with a file extension like `.md`, `.txt`, `.doc`). If detected, read the file. If the file does not exist, tell the user and stop.
- **Inline text**: anything else is treated as a direct description of the idea, product, plan, or feature.

If the input is empty or missing, ask the user to describe their idea.

## Pre-flight: Gather Missing Information

Before launching the investor panel, you need three pieces of context. Check whether the user's input already covers them. For any that are missing, ask the user in a single batch:

1. **Stage**: What stage is this? (raw concept / MVP in progress / live product adding a feature / pivot / something else)
2. **Constraints**: Any known constraints? (budget, timeline, team size, technical limitations, regulatory)
3. **Target market**: Who is this for? (if not already clear from the idea description)

Do not launch agents until you have answers for all three, or the user explicitly says to proceed without them.

## Execution

Once you have the full brief, assemble the complete pitch text: the idea description plus the stage, constraints, and target market context.

Launch all seven investor agents **in parallel** using the Agent tool. Pass each agent the complete pitch text as part of the prompt. The agents are:

1. `investor-graham` -- Paul Graham
2. `investor-thiel` -- Peter Thiel
3. `investor-altman` -- Sam Altman
4. `investor-andreessen` -- Marc Andreessen
5. `investor-naval` -- Naval Ravikant
6. `investor-balaji` -- Balaji Srinivasan
7. `investor-collison` -- Patrick Collison

For each agent, use this prompt structure:

```
Evaluate the following idea from your investor perspective. Here is the complete brief:

<brief>
{the assembled pitch text}
</brief>

Respond using the exact output format specified in your instructions.
```

## Synthesis

After all seven agents return, produce a unified report:

### Individual Verdicts Table

| Investor | Verdict | Conviction | Bull Case (1-line) | Bear Case (1-line) |
|----------|---------|------------|--------------------|--------------------|
| Graham   | ...     | ...        | ...                | ...                |
| Thiel    | ...     | ...        | ...                | ...                |
| Altman   | ...     | ...        | ...                | ...                |
| Andreessen | ...   | ...        | ...                | ...                |
| Naval    | ...     | ...        | ...                | ...                |
| Balaji   | ...     | ...        | ...                | ...                |
| Collison | ...     | ...        | ...                | ...                |

### Consensus

- **Where they agree**: themes that multiple investors raised on the same side
- **Where they diverge**: points of genuine disagreement and why their frameworks produce different answers
- **Recurring risks**: concerns raised by 3+ investors

### Key Questions

Deduplicated list of the most important questions raised across all investors. Group by theme, not by investor.

### Synthesis

Your own integrated assessment. Not a vote count. Weigh the arguments by their quality and relevance. State what the strongest path forward looks like and what the founder should resolve first.
