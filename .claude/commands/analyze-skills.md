---
allowed-tools: Agent, Bash, Read, Write, Glob, Grep, WebFetch
description: Analyze skill structure and patterns from a GitHub skills folder or single skill URL
argument-hint: <github-url-to-skills-folder-or-single-skill>
disable-model-invocation: false
---

You are orchestrating a structural analysis of Claude Code plugin skills from a GitHub URL.

## Input

The user provided: `$ARGUMENTS`

This must be a GitHub URL pointing to either:
- A `skills/` folder containing multiple skills (e.g., `https://github.com/org/repo/tree/main/skills`)
- A single skill directory (e.g., `https://github.com/org/repo/tree/main/skills/skill-name`)

## Phase 1: Discovery

1. Extract the repo owner, repo name, branch, and path from the URL.
2. Use the GitHub API via `gh api` to list the contents of the target directory.
   - If the URL points to a `skills/` folder, each subdirectory is a skill. Collect all skill directory names.
   - If the URL points to a single skill directory (contains a `SKILL.md` file or skill-like structure), treat it as a single-skill analysis.
3. For each discovered skill, collect the full file tree using `gh api` recursively. Record every file path and its size.

Derive the repo name from the URL for use in the output path.

## Phase 2: Parallel Analysis

Launch one `sonnet` model Agent per skill, all in parallel. Each agent receives the following prompt (fill in the specifics per skill):

---

You are analyzing the structure of a Claude Code plugin skill. Your job is purely analytical -- read everything, measure everything, report precisely.

**Skill name:** {skill_name}
**Repository:** {owner}/{repo}
**Branch:** {branch}
**Skill path:** {path_to_skill}

Use `gh api repos/{owner}/{repo}/contents/{path_to_skill}` (with `?ref={branch}` if not the default branch) to explore the skill directory recursively. For each file, fetch its raw content using `gh api repos/{owner}/{repo}/contents/{file_path}?ref={branch}` and read the `content` field (base64-decode it), or use WebFetch on the raw GitHub URL: `https://raw.githubusercontent.com/{owner}/{repo}/{branch}/{file_path}`.

Start with SKILL.md as the primary document.

### Analysis checklist

Produce a markdown report with the following sections. Use exact measurements, not approximations, except where noted.

#### 1. Overview
- Skill name (from directory name and from SKILL.md title if different)
- Skill title text (the `# Title` line in SKILL.md) and its character length
- Skill description (the `description:` from YAML frontmatter if present, or first paragraph) and its character length
- Total number of files in the skill directory (recursive)
- Total number of subdirectories
- List of all files with relative paths

#### 2. SKILL.md Metrics
- Line count
- Word count
- Estimated token count (word count / 0.75, rounded to nearest integer)
- Character count

#### 3. Document Structure Depth
- List every heading in SKILL.md with its level (H1-H6), in document order
- Maximum heading depth reached
- Heading count per level (H1: N, H2: N, etc.)
- Produce a headline breakdown: list each heading with its level indicator and the line number it appears on

#### 4. Content Specificity Assessment
Rate the overall specificity on a 1-5 scale:
1. Pure high-level principles, no actionable instructions
2. General guidance with occasional specific directives
3. Mix of high-level framing and concrete instructions
4. Mostly specific, actionable instructions with some framing
5. Extremely granular, step-by-step instructions with exact patterns/templates

Justify the rating with 2-3 representative excerpts (quote briefly, cite line numbers).

#### 5. Internal File References
List every reference in SKILL.md to other files. For each:
- The reference text/link as written
- Whether it points to a file inside the skill directory or outside it
- Whether the target file exists (check via API)
- The context in which it is referenced (which section of SKILL.md)

If no file references exist, state that explicitly.

#### 6. Skill Cross-References
List every reference to other skills (e.g., mentions of other skill names, links to other skill directories). For each:
- The reference text
- The target skill name
- How it is referenced (link, inline mention, conditional trigger)

If no skill references exist, state that explicitly.

#### 7. Agent References
List every reference to agents (subagents). For each:
- The agent name
- How it is referenced (launched, mentioned, conditional)
- The context/section where it appears

If no agent references exist, state that explicitly.

#### 8. Other Markdown File Analysis
For each non-SKILL.md markdown file in the skill directory:
- File name and path
- Line count, word count, estimated token count
- Brief description of its content (1-2 sentences)
- How it is referenced from SKILL.md (if at all)

If there are no other markdown files, state that explicitly.

#### 9. Structural Observations
Any additional patterns worth noting:
- Use of YAML frontmatter (fields present)
- Use of code blocks (count and languages)
- Use of lists vs prose
- Use of conditional logic ("if X then Y" patterns)
- Use of templates or placeholder variables
- Use of examples
- Presence of constraints/rules sections

### Output format

Return the full report as a single markdown document. Begin with a YAML frontmatter block containing metadata, followed by the H1 title (the skill name), followed by the analysis sections. Do not omit any section even if empty -- explicitly state "None" or "N/A".

The frontmatter must use these exact keys:

```yaml
---
repository: {owner}/{repo}
branch: {branch}
skill-path: {path_to_skill}
analyzed: {YYYY-MM-DD}
---
```

Do not duplicate this metadata as prose below the frontmatter.

---

## Phase 3: Write Individual Reports

As each agent returns its report, write the output to:

```
.claude/reports/{repo_name}/{skill_name}.md
```

Create the directories if they do not exist.

## Phase 4: Summary

After all individual analyses are complete, synthesize an aggregate summary. Read all the individual reports you just wrote, then produce a summary document covering:

### Aggregate Patterns

- **Scale:** Total number of skills analyzed, total files across all skills, total estimated tokens across all SKILL.md files
- **Size distribution:** Min/max/median line counts and token counts for SKILL.md files
- **Structure depth:** Most common max heading depth, range observed
- **Specificity distribution:** How many skills fall at each level of the 1-5 specificity scale
- **Cross-referencing patterns:** How commonly do skills reference other skills? How commonly do they reference agents? What is the typical referencing mechanism?
- **File composition:** Average number of files per skill, most common file types, how many skills have supplementary markdown files beyond SKILL.md
- **Title and description lengths:** Min/max/median character counts
- **Structural conventions:** Common heading patterns, common sections that appear across multiple skills, common frontmatter fields
- **Content patterns:** Prevalence of code blocks, examples, conditional logic, templates, constraints sections

Write the summary to:

```
.claude/reports/{repo_name}/_summary.md
```

The summary must also begin with a YAML frontmatter block:

```yaml
---
repository: {owner}/{repo}
branch: {branch}
skills-analyzed: {count}
analyzed: {YYYY-MM-DD}
---
```

## Completion

Report to the user:
- Number of skills analyzed
- Output directory path
- Any skills that failed to analyze (with reason)
