---
repository: EveryInc/compound-engineering-plugin
branch: main
skill-path: plugins/compound-engineering/skills/ce-demo-reel
analyzed: 2026-04-11
---

# Skill Analysis: ce-demo-reel


## 1. Overview

**Skill name:** ce-demo-reel

**Title text:** "Demo Reel"
**Title char length:** 9 characters

**Description text:** "Capture a visual demo reel (GIF, terminal recording, screenshots) for PR descriptions. Use when shipping UI changes, CLI features, or any work with observable behavior that benefits from visual proof. Also use when asked to add a demo, record a GIF, screenshot a feature, show what changed visually, create a demo reel, capture evidence, add proof to a PR, or create a before/after comparison."
**Description char length:** 396 characters

**Total files (recursive):**
- SKILL.md (10,397 bytes)
- references/tier-browser-reel.md (4,324 bytes)
- references/tier-screenshot-reel.md (2,353 bytes)
- references/tier-static-screenshots.md (1,716 bytes)
- references/tier-terminal-recording.md (3,066 bytes)
- references/upload-and-approval.md (2,760 bytes)
- scripts/capture-demo.py (26,229 bytes)

**Total file count:** 7

**Subdirectories:** 2
- references/
- scripts/

**File list:**

| Path | Type | Size (bytes) |
|------|------|-------------|
| SKILL.md | blob | 10,397 |
| references/tier-browser-reel.md | blob | 4,324 |
| references/tier-screenshot-reel.md | blob | 2,353 |
| references/tier-static-screenshots.md | blob | 1,716 |
| references/tier-terminal-recording.md | blob | 3,066 |
| references/upload-and-approval.md | blob | 2,760 |
| scripts/capture-demo.py | blob | 26,229 |

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 99 |
| Word count | 1,287 |
| Estimated token count (words / 0.75) | ~1,716 tokens |
| Character count (baseline from known byte size) | 10,397 |

---

## 3. Document Structure Depth

**All headings in order:**

| Line (approx) | Level | Text |
|---------------|-------|------|
| 5 | H1 | Demo Reel |
| 18 | H2 | Arguments |
| 24 | H2 | Step 0: Discover Capture Target |
| 45 | H2 | Step 1: Exercise the Feature |
| 53 | H2 | Step 2: Detect Project Type |
| 60 | H2 | Step 3: Assess Change Type |
| 77 | H2 | Step 4: Tool Preflight |
| 84 | H2 | Step 5: Create Run Directory |
| 90 | H2 | Step 6: Recommend Tier and Ask User |
| 104 | H2 | Step 7: Execute Selected Tier |
| 121 | H2 | Step 8: Upload and Approval |
| 123 | H2 | Output |

**Max depth:** H2 (2 levels)

**Count per level:**
- H1: 1
- H2: 11

**Total headings:** 12

---

## 4. Content Specificity Assessment

**Rating: 5 / 5**

The skill is maximally specific. Instructions are deterministic and operational at every step.

**Justification excerpts:**

1. Constraint with no ambiguity: "Never generate fake or placeholder image/GIF URLs. If upload fails, report the failure." -- zero wiggle room, covers both the failure mode and the forbidden workaround.

2. Cross-platform tool resolution with exact API names: "Use the platform's blocking question tool (`AskUserQuestion` in Claude Code, `request_user_input` in Codex, `ask_user` in Gemini)" -- names three specific environments with their exact function names.

3. Fallback ordering is explicit and exhaustive: "The fallback order is: browser reel -> static screenshots, terminal recording -> screenshot reel -> static screenshots, screenshot reel -> static screenshots." -- no judgment required from the agent, every path is specified.

---

## 5. Internal File References

All file references found in SKILL.md:

| Reference | Type | Step |
|-----------|------|------|
| `scripts/capture-demo.py detect` | script invocation | Step 2 |
| `scripts/capture-demo.py preflight` | script invocation | Step 4 |
| `scripts/capture-demo.py recommend` | script invocation | Step 6 |
| `references/tier-browser-reel.md` | Read instruction | Step 7 |
| `references/tier-terminal-recording.md` | Read instruction | Step 7 |
| `references/tier-screenshot-reel.md` | Read instruction | Step 7 |
| `references/tier-static-screenshots.md` | Read instruction | Step 7 |
| `references/upload-and-approval.md` | Read instruction | Step 8 |

**Total internal file references:** 8 (3 script invocations + 5 reference file reads)

---

## 6. Skill Cross-References

**Referenced skills:**
- `git-commit-push-pr` -- mentioned in the Output section as the expected caller: "Return these values to the caller (e.g., git-commit-push-pr)"

No `$SKILL` or skill-path references found. The cross-reference is informal (example text), not a hard dependency declaration.

---

## 7. Agent References

No agent references found in SKILL.md. The skill does not invoke subagents. The only agent-adjacent mention is the `agent_browser` tool (a CLI tool checked during preflight), which is a binary, not a Claude agent.

---

## 8. Other Markdown File Analysis

### references/tier-browser-reel.md (4,324 bytes)

**Headings:**
| Level | Text |
|-------|------|
| H1 | Tier: Browser Reel |
| H2 | Step 1: Connect to the Application |
| H2 | Step 2: Capture Screenshots |
| H2 | Step 3: Stitch into GIF |
| H2 | Step 4: Cleanup |

**Total headings:** 5 (1x H1, 4x H2)
**Estimated lines:** ~100
**Estimated words:** ~600
**Estimated tokens:** ~800
**Character count (baseline):** 4,324
**Code blocks:** 9 (bash commands for agent-browser, curl, ffmpeg pipeline)
**Notable:** Contains CDP (Chrome DevTools Protocol) connection logic for Electron apps, port polling loop, fallback handling for web vs desktop app distinction.

---

### references/tier-screenshot-reel.md (2,353 bytes)

**Headings:**
| Level | Text |
|-------|------|
| H1 | Tier: Screenshot Reel |
| H2 | Step 1: Write Demo Content |
| H2 | Step 2: Split into Frame Files |
| H2 | Step 3: Render and Stitch |
| H2 | Step 4: Cleanup |

**Total headings:** 5 (1x H1, 4x H2)
**Estimated lines:** ~60
**Estimated words:** ~370
**Estimated tokens:** ~494
**Character count (baseline):** 2,353
**Code blocks:** 3 (demo-steps.txt example, frame file list, capture-demo.py invocation)
**Notable:** Contains a literal multi-frame demo-steps.txt example with `---` delimiters, concrete tip about stripping unicode for silicon compatibility.

---

### references/tier-static-screenshots.md (1,716 bytes)

**Headings:**
| Level | Text |
|-------|------|
| H1 | Tier: Static Screenshots |
| H2 | Capture by Project Type |
| H3 | Web app or desktop app (agent-browser available) |
| H3 | CLI tool (silicon available) |
| H3 | CLI tool (no silicon) |
| H3 | Library |
| H2 | Upload |

**Total headings:** 7 (1x H1, 2x H2, 4x H3)
**Max depth:** H3 (3 levels -- deepest in the skill)
**Estimated lines:** ~55
**Estimated words:** ~270
**Estimated tokens:** ~360
**Character count (baseline):** 1,716
**Code blocks:** 5 (agent-browser commands, silicon command, markdown embed example)
**Notable:** Only file in the skill reaching H3. Branches on tool availability with four named sub-cases.

---

### references/tier-terminal-recording.md (3,066 bytes)

**Headings:**
| Level | Text |
|-------|------|
| H1 | Tier: Terminal Recording |
| H2 | Step 1: Plan the Recording |
| H2 | Step 2: Generate .tape File |
| H2 | Step 3: Run VHS |
| H2 | Step 4: Quality Check |

**Total headings:** 5 (1x H1, 4x H2)
**Estimated lines:** ~85
**Estimated words:** ~480
**Estimated tokens:** ~640
**Character count (baseline):** 3,066
**Code blocks:** 2 (VHS .tape example, capture-demo.py invocation)
**Notable:** Contains a complete annotated VHS .tape template with inline comments explaining each directive. Lists explicit "Avoid" constraints (non-deterministic output, interactive input, long scrolling output).

---

### references/upload-and-approval.md (2,760 bytes)

**Headings:**
| Level | Text |
|-------|------|
| H1 | Upload and Approval |
| H2 | Step 1: Preview Upload (Temporary) |
| H2 | Step 2: Approval Gate |
| H3 | On "Recapture" |
| H3 | On "Proceed without evidence" |
| H2 | Step 3: Promote to Permanent Hosting |
| H2 | Step 4: Return Output |
| H2 | Step 5: Cleanup |

**Total headings:** 8 (1x H1, 5x H2, 2x H3)
**Max depth:** H3 (3 levels)
**Estimated lines:** ~75
**Estimated words:** ~430
**Estimated tokens:** ~573
**Character count (baseline):** 2,760
**Code blocks:** 3 (preview upload, upload/promote commands)
**Notable:** Two-phase upload pattern (litterbox for preview, catbox for permanent). Approval gate branches to three outcomes. Explicit cross-platform blocking question tool names (same pattern as SKILL.md). Final cleanup step removes RUN_DIR.

---

## 9. Structural Observations

### YAML Frontmatter
Present in SKILL.md. Three fields:
- `name: ce-demo-reel`
- `description:` (full trigger-phrase-rich description, 396 chars)
- `argument-hint: "[what to capture, e.g. 'the new settings page' or 'CLI output of the migrate command']"`

No frontmatter in any references/ files -- they are pure content loaded at runtime.

### Code Blocks
SKILL.md contains 6 code blocks, all `bash` or unlabeled:
- `python3 scripts/capture-demo.py detect` (Step 2)
- `python3 scripts/capture-demo.py preflight` (Step 4)
- `mktemp -d -t demo-reel-XXXXXX` (Step 5)
- `python3 scripts/capture-demo.py recommend` (Step 6)
- Output format block (Output section)
- Markdown table in Step 3 (classification guide)

References files add ~22 additional code blocks across all 5 files, totaling ~28 code blocks across the skill.

### Lists vs Prose
SKILL.md is predominantly prose with embedded bullet lists for:
- Arguments parsing (Step 0 bullets for context sources)
- Feature exercise checklist (Step 1)
- Tier options in Step 6 (numbered list with 5 options)
- File-to-tier mapping list (Step 7)
- Output field descriptions

Approximately 60% prose, 25% lists, 15% code blocks by line count.

### Conditional Logic
Extensive. Identified conditional branches in SKILL.md:
- Step 0: Single behavior vs. multiple behaviors vs. no observable behavior (3-way branch)
- Step 7: 5-way branch on selected tier (browser, terminal, screenshot, static, none)
- Step 7: Runtime failure fallback chain (explicit ordered fallback per tier)
- Output section: skipped vs. captured distinction

References files add further branching:
- tier-browser-reel.md: web app vs. Electron/CDP vs. CDP failure (3-way)
- tier-static-screenshots.md: 4-way branch by project type and tool availability
- upload-and-approval.md: 3-way approval gate (use / recapture / proceed without)

### Templates
- VHS .tape template in tier-terminal-recording.md is a complete, annotated, copy-usable template
- demo-steps.txt frame template in tier-screenshot-reel.md
- Output block in SKILL.md Output section serves as a structured return format template

### Examples
- Step 0: capture hypothesis phrasing example: "The best evidence appears to be [behavior]"
- Arguments: `argument-hint` contains two concrete examples
- Step 6: blocking question tool invocation examples by platform
- Output section: Description example: "CLI detect command classifying 3 project types and recommending capture tiers"
- tier-screenshot-reel.md: complete worked demo-steps.txt example with three frames

### Constraints (explicit prohibitions)
- "Evidence means USING THE PRODUCT, not running tests." (absolute, capitalized)
- "Never generate fake or placeholder image/GIF URLs."
- "Test output is never labeled 'Demo' or 'Screenshots.'" (stated twice)
- "Do not silently skip to 'no evidence needed' or substitute test output."
- "Do not start it automatically" (re: dev server, in tier-browser-reel.md)
- VHS "Avoid" list: non-deterministic output, interactive input, scrolling output

### Progressive Disclosure Pattern
The skill uses a two-layer disclosure model. SKILL.md defines the orchestration logic and references four tier files and one upload file. Tier files are only loaded at the point of execution (Step 7), not upfront. This keeps the active context window lean until a specific tier is selected. The scripts/ directory provides a third layer -- a 26,229-byte Python helper that handles tool detection, stitching, uploading, and recommendation, offloading computational logic from the prompt layer entirely.
