---
repository: anthropics/skills
branch: main
skill-path: skills/doc-coauthoring
analyzed: 2026-04-11
---

# Skill Analysis: doc-coauthoring


## 1. Overview

| Field | Value |
|---|---|
| Skill name | `doc-coauthoring` |
| Title text | `Doc Co-Authoring Workflow` |
| Title char length | 26 |
| Description (from frontmatter) | `Guide users through a structured workflow for co-authoring documentation. Use when user wants to write documentation, proposals, technical specs, decision docs, or similar structured content. This workflow helps users efficiently transfer context, refine content through iteration, and verify the doc works for readers. Trigger when user mentions writing docs, creating proposals, drafting specs, or similar documentation tasks.` |
| Description char length | 427 |
| Total files (recursive) | 1 |
| Subdirectories | 0 |

**File list:**

```
skills/doc-coauthoring/
  SKILL.md    (15,815 bytes)
```

No subdirectories. No additional files (no examples, no templates, no reference files).

---

## 2. SKILL.md Metrics

| Metric | Value |
|---|---|
| Reported file size | 15,815 bytes |
| Line count | ~290 |
| Word count | ~2,360 |
| Estimated token count (words / 0.75) | ~3,147 |
| Character count | ~15,815 |

Notes on estimation: Line and word counts are derived from the raw content. The file contains no binary data; character count approximates byte count for ASCII/UTF-8 with minimal non-ASCII characters.

---

## 3. Document Structure Depth

### Heading inventory (in order)

| # | Level | Heading text | Notes |
|---|---|---|---|
| 1 | H1 | Doc Co-Authoring Workflow | Main title, line ~7 |
| 2 | H2 | When to Offer This Workflow | line ~9 |
| 3 | H2 | Stage 1: Context Gathering | line ~18 |
| 4 | H3 | Initial Questions | line ~22 |
| 5 | H3 | Info Dumping | line ~40 |
| 6 | H2 | Stage 2: Refinement & Structure | line ~73 |
| 7 | H3 | Step 1: Clarifying Questions | line ~100 |
| 8 | H3 | Step 2: Brainstorming | line ~107 |
| 9 | H3 | Step 3: Curation | line ~114 |
| 10 | H3 | Step 4: Gap Check | line ~126 |
| 11 | H3 | Step 5: Drafting | line ~129 |
| 12 | H3 | Step 6: Iterative Refinement | line ~150 |
| 13 | H3 | Quality Checking | line ~163 |
| 14 | H3 | Near Completion | line ~172 |
| 15 | H2 | Stage 3: Reader Testing | line ~183 |
| 16 | H3 | Testing Approach | line ~189 |
| 17 | H3 | Step 1: Predict Reader Questions | line ~193 (sub-agent branch) |
| 18 | H3 | Step 2: Test with Sub-Agent | line ~200 |
| 19 | H3 | Step 3: Run Additional Checks | line ~210 |
| 20 | H3 | Step 4: Report and Fix | line ~218 |
| 21 | H3 | Step 1: Predict Reader Questions | line ~226 (no sub-agent branch, duplicate heading) |
| 22 | H3 | Step 2: Setup Testing | line ~229 |
| 23 | H3 | Step 3: Additional Checks | line ~243 |
| 24 | H3 | Step 4: Iterate Based on Results | line ~249 |
| 25 | H3 | Exit Condition (Both Approaches) | line ~255 |
| 26 | H2 | Final Review | line ~259 |
| 27 | H2 | Tips for Effective Guidance | line ~273 |

### Summary

| Level | Count |
|---|---|
| H1 | 1 |
| H2 | 6 |
| H3 | 20 |
| H4+ | 0 |
| **Total** | **27** |

**Max depth:** 3 (H3)

**Duplicate headings:** "Step 1: Predict Reader Questions" and "Step 3: Additional Checks" / "Step 4: Iterate Based on Results" appear twice each -- once under the sub-agent branch and once under the no-sub-agent branch of Stage 3. These are structural parallels within a conditional split, not errors, but they would render identically in any document system that auto-generates anchor IDs.

---

## 4. Content Specificity Assessment

**Rating: 4 / 5**

The skill is highly actionable and operationally specific. It prescribes exact step counts, branching logic, tool call names, and exit conditions. Most instructions are directive enough that an LLM could execute them without additional disambiguation.

**Justification excerpts:**

1. **Quantified outputs:** "Generate 5-10 numbered questions based on gaps in the context." and "brainstorm [5-20] things that might be included, depending on the section's complexity." -- these give Claude bounded ranges, not open-ended directives.

2. **Explicit tool call prescriptions:** "Use `create_file` to create an artifact" / "Use `str_replace` to replace the placeholder text" -- the skill names specific tools and specifies when to use each, not just what outcome is desired.

3. **Concrete shorthand examples provided to model for user guidance:** "e.g., '1: yes, 2: see #channel, 3: no because backwards compat'" -- the skill supplies example utterances the model can reproduce verbatim to users, reducing improvisation.

**Deduction from 5:** One point off because Stage 3 (Reader Testing) diverges into two large parallel branches (sub-agent vs. no sub-agent) that repeat the same step names with minimal structural differentiation. The conditional logic is correct but increases cognitive load and slightly dilutes precision with redundancy.

---

## 5. Internal File References

| Reference | Type | Context | Exists check |
|---|---|---|---|
| `decision-doc.md` | Filename example | Stage 2, "If no access to artifacts" block: suggested name for output file | Not a referenced file -- it is an example value for a file Claude would create at runtime. Not tracked in repo. |
| `technical-spec.md` | Filename example | Same block as above | Same as above. |

No internal links to other files within the skill directory. No `[text](path)` links. No `![]()` image references. The skill references runtime-generated files (artifacts) by example name only.

---

## 6. Skill Cross-References

None. The SKILL.md contains no explicit references to other skills by name or path. The word "skill" appears only in reference to the document itself ("This skill provides...") or as a generic noun. No `skills/` path references, no `@skill` syntax, no import-style references.

---

## 7. Agent References

**Sub-agent references:** The skill references "sub-agents" as a runtime capability check, not as named agents to invoke.

Relevant excerpts:
- "If access to sub-agents is available (e.g., in Claude Code): Perform the testing directly without user involvement."
- "For each question, invoke a sub-agent with just the document content and the question."
- "Invoke sub-agent to check for ambiguity, false assumptions, contradictions."

These are capability-conditional instructions. No named agents are referenced (no agent file paths, no agent names from a registry). The sub-agent invocations are anonymous and context-dependent -- the skill assumes the runtime environment may or may not have sub-agent access and branches accordingly.

---

## 8. Other Markdown File Analysis

None. The `skills/doc-coauthoring/` directory contains only `SKILL.md`. There are no:
- Additional `.md` files (no examples, no changelog, no reference docs)
- Subdirectories with further content
- Template files
- Configuration files

---

## 9. Structural Observations

### YAML Frontmatter

Present. Located at lines 1-4.

```yaml
---
name: doc-coauthoring
description: Guide users through a structured workflow for co-authoring documentation. Use when user wants to write documentation, proposals, technical specs, decision docs, or similar structured content. This workflow helps users efficiently transfer context, refine content through iteration, and verify the doc works for readers. Trigger when user mentions writing docs, creating proposals, drafting specs, or similar documentation tasks.
---
```

Fields: `name` and `description` only. No `version`, `author`, `tools`, or `triggers` fields. The description is a single long paragraph (427 chars) functioning as both a trigger guide and a capability summary.

### Code Blocks

No fenced code blocks (` ``` `) appear in the body. The frontmatter delimiter `---` is the only use of triple-dash syntax. All technical terms (`create_file`, `str_replace`, `str_replace`) are inline-code formatted with single backticks.

Inline code references:
- `` `create_file` `` -- artifact creation tool
- `` `str_replace` `` -- artifact edit tool (referenced 4 times)
- `` `decision-doc.md` ``, `` `technical-spec.md` `` -- example filenames

### Lists vs Prose

The document uses a heavy mix:
- **Numbered lists** for sequential steps within sections (Stage 2 per-section workflow, Stage 3 testing steps)
- **Bulleted lists** for trigger conditions, tips, and item enumerations
- **Bold labels** (`**Trigger conditions:**`, `**Initial offer:**`, `**Goal:**`, `**Instructions to user:**`, `**Key instruction for user:**`) used extensively to mark paragraph-level directives without elevating them to headings
- **Prose paragraphs** used primarily for rationale and contextual framing within steps

Approximately 60% list-based, 40% prose.

### Conditional Logic

The skill contains explicit branching with two main patterns:

**Pattern 1 -- capability branching (If/If not):**
- "If access to artifacts is available" / "If no access to artifacts"
- "If access to sub-agents is available (e.g., in Claude Code)" / "If no access to sub-agents (e.g., claude.ai web interface)"
- "If integrations are available" / "If no integrations are detected"

**Pattern 2 -- user-state branching:**
- "If user provides a template or mentions a doc type"
- "If user mentions editing an existing shared document"
- "If user gives freeform feedback instead of numbered selections"
- "If user wants to skip a stage"
- "If user seems frustrated"

These branches are written in prose with bold `**If ...**` labels, not as formal conditional syntax. The Stage 3 sub-agent vs. no-sub-agent split is the most extensive, duplicating an entire set of H3-level steps.

### Templates

The skill does not contain document templates. It instructs Claude to create runtime artifacts with section placeholders like `[To be written]` or `[Content here]`, but these are described verbally, not embedded as template text in the skill itself.

### Examples

Inline shorthand examples are provided for user-facing communication:
- Shorthand answer format: `"1: yes, 2: see #channel, 3: no because backwards compat"`
- Curation instruction examples: `"Keep 1,4,7,9"`, `"Remove 3 (duplicates 1)"`, `"Remove 6 (audience already knows this)"`, `"Combine 11 and 12"`
- User feedback examples: `"Remove the X bullet - already covered by Y"`, `"Make the third paragraph more concise"`
- Reader Claude question format: "The answer", "Whether anything was ambiguous or unclear", "What knowledge/context the doc assumes"

These examples are embedded within prose and serve as scripted prompts the model is expected to relay to users.

### Constraints

Explicit prohibitions and limits:
- "never reprint the whole doc" (in Step 6: Iterative Refinement)
- "Never use artifacts for brainstorming lists - that's just conversation" (Tips section)
- "Use `str_replace` for all edits" (Artifact Management tip)
- Sub-agent invocations use only document content + question (no context bleed by design)

Exit conditions are defined for Stage 1 ("Sufficient context has been gathered when questions show understanding") and Stage 3 ("When Reader Claude consistently answers questions correctly and doesn't surface new gaps or ambiguities").

Quality thresholds are defined: "After 3 consecutive iterations with no substantial changes, ask if anything can be removed."

Completion checkpoint: "Near Completion" triggers at "80%+ of sections done" -- a quantified heuristic.
