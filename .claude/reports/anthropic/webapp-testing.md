# Skill Analysis: webapp-testing

**Repository:** anthropics/skills  
**Branch:** main  
**Path:** skills/webapp-testing  
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** `webapp-testing`  
**Title text (H1):** `Web Application Testing`  
**Title char length:** 26 characters

**Description (from YAML frontmatter):**  
`Toolkit for interacting with and testing local web applications using Playwright. Supports verifying frontend functionality, debugging UI behavior, capturing browser screenshots, and viewing browser logs.`  
**Description char length:** 204 characters

**Total files (recursive):** 6  
**Subdirectories:** 2 (`examples/`, `scripts/`)

**File list:**

| Path | Size (bytes) | Type |
|---|---|---|
| `SKILL.md` | 3,913 | Markdown |
| `LICENSE.txt` | 11,357 | Text |
| `examples/console_logging.py` | 1,027 | Python |
| `examples/element_discovery.py` | 1,463 | Python |
| `examples/static_html_automation.py` | 953 | Python |
| `scripts/with_server.py` | 3,693 | Python |

---

## 2. SKILL.md Metrics

- **Line count:** 97 (including blank lines and YAML frontmatter)
- **Word count:** ~500
- **Estimated token count (words / 0.75):** ~667
- **Character count:** 3,913 (exact, per GitHub blob API `size` field)

---

## 3. Document Structure Depth

**Headings in order (with line numbers):**

| Line | Level | Text |
|---|---|---|
| 7 | H1 | `Web Application Testing` |
| 16 | H2 | `Decision Tree: Choosing Your Approach` |
| 35 | H2 | `Example: Using with_server.py` |
| 64 | H2 | `Reconnaissance-Then-Action Pattern` |
| 78 | H2 | `Common Pitfall` |
| 83 | H2 | `Best Practices` |
| 92 | H2 | `Reference Files` |

**Max depth:** H2 (level 2)  
**Count per level:**
- H1: 1
- H2: 6
- H3+: 0

**Total headings:** 7

---

## 4. Content Specificity Assessment

**Score: 4 / 5**

The skill is concrete and actionable. It names specific files, specific CLI flags, specific Playwright API calls, and specific error patterns. It stops short of 5 because it does not cover assertions/test validation patterns (only automation/navigation), and the "Common Pitfall" section has only one entry despite the domain having many.

**Justification excerpts:**

1. **Specific tool invocation syntax** (line 41):  
   `python scripts/with_server.py --server "npm run dev" --port 5173 -- python your_automation.py`  
   Not a generic placeholder — gives a realistic dev-server port, exact flag names, and exact argument ordering.

2. **Named Playwright API methods with rationale** (line ~58):  
   `page.wait_for_load_state('networkidle') # CRITICAL: Wait for JS to execute`  
   The inline comment disambiguates the _why_, not just the _what_.

3. **Black-box usage instruction with explicit anti-pattern** (line ~14):  
   `DO NOT read the source until you try running the script first and find that a customized solution is abslutely necessary.`  
   Directly addresses a failure mode unique to LLM context-window behavior — not generic advice.

---

## 5. Internal File References

All file references found in SKILL.md:

| Reference | Context |
|---|---|
| `scripts/with_server.py` | Named in "Helper Scripts Available" bullet and repeatedly in examples |
| `examples/element_discovery.py` | Listed under "Reference Files" |
| `examples/static_html_automation.py` | Listed under "Reference Files" |
| `examples/console_logging.py` | Listed under "Reference Files" |
| `LICENSE.txt` | YAML frontmatter: `license: Complete terms in LICENSE.txt` |

Total internal file references: 5 (4 distinct paths + LICENSE.txt in frontmatter)

---

## 6. Skill Cross-References

None. SKILL.md contains no references to other skills in the `anthropics/skills` repository. There are no `skills/` path references, no skill names cited, and no explicit dependency declarations.

---

## 7. Agent References

None. SKILL.md contains no references to Claude agents, subagents, or agent configuration files.

---

## 8. Other Markdown File Analysis

No markdown files exist outside of `SKILL.md` in this skill. `LICENSE.txt` is plain text (Apache 2.0, 11,357 bytes) and contains no skill-relevant content. The three `examples/*.py` and one `scripts/*.py` file are Python, not Markdown.

---

## 9. Structural Observations

### YAML Frontmatter
Present. Three fields:
```yaml
name: webapp-testing
description: Toolkit for interacting with and testing local web applications using Playwright. Supports verifying frontend functionality, debugging UI behavior, capturing browser screenshots, and viewing browser logs.
license: Complete terms in LICENSE.txt
```
No `tools`, `version`, `author`, or `triggers` fields. The `license` field is non-standard for Claude Code skill frontmatter — it redirects to the LICENSE.txt file rather than stating a SPDX identifier.

### Code Blocks
5 fenced code blocks total:

| Block | Language | Purpose |
|---|---|---|
| 1 | (none/plain) | Decision tree ASCII diagram |
| 2 | `bash` | Single-server invocation |
| 3 | `bash` | Multi-server invocation |
| 4 | `python` | Minimal Playwright automation template |
| 5 | `python` | Reconnaissance DOM inspection snippet |

### Lists vs Prose
- Prose paragraphs: 3 (intro paragraph, server-helper note, automation script intro)
- Unordered lists: 3 (Helper Scripts Available, Best Practices, Reference Files)
- Ordered lists: 1 (Reconnaissance-Then-Action Pattern, 3 steps)
- Nested list: 1 (Reference Files section has a nested unordered list under the `examples/` entry)

Overall the document skews toward structured lists and code blocks over prose, which is appropriate for LLM consumption.

### Conditional Logic
One explicit decision tree (code block 1) using ASCII branching notation. Two branches: static HTML vs. dynamic webapp. Sub-branch under dynamic: server already running vs. not running. This is the most structurally distinctive element of the skill.

### Templates
One reusable Playwright script template (code block 4) with inline comments marking integration points (`# Always launch chromium in headless mode`, `# Server already running and ready`, `# CRITICAL: Wait for JS to execute`, `# ... your automation logic`).

### Examples
Three example files in `examples/`:

| File | Lines | Pattern Demonstrated |
|---|---|---|
| `element_discovery.py` | ~37 | Enumerate buttons, links, inputs; take screenshot |
| `static_html_automation.py` | ~30 | `file://` URL navigation; form fill and submit |
| `console_logging.py` | ~30 | `page.on("console", ...)` event capture; write log to file |

All three use `sync_playwright`, `headless=True`, and `p.chromium.launch()` — consistent with the template in SKILL.md. `element_discovery.py` and `console_logging.py` hard-code `http://localhost:5173` as the target URL.

### Scripts
`scripts/with_server.py` (3,693 bytes, ~100 lines):
- `argparse`-based CLI accepting repeated `--server`/`--port` pairs
- Port-polling readiness check via `socket.create_connection` with 0.5s retry loop
- `subprocess.Popen` with `shell=True` to support `cd ... && ...` composite commands
- `try/finally` cleanup with `process.terminate()` + fallback `process.kill()`
- Exits with the return code of the user command

### Constraints / Anti-patterns Documented
- **Do not** read script source directly — use `--help` first (explicit in prose, rationale given: context window pollution)
- **Do not** inspect DOM before `networkidle` on dynamic apps (documented under "Common Pitfall" with ❌/✅ notation)
- Typo present in SKILL.md line ~14: `abslutely` (should be `absolutely`)

### Notable Absence
No assertions, no test framework integration (pytest, unittest), no CI invocation patterns. The skill covers browser automation and UI reconnaissance but not test result validation — the word "test" in the skill name is partially misleading relative to actual content scope.
