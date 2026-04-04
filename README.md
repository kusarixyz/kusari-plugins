# kusari-plugins

Claude Code plugin collection.

## Installation

Register the marketplace:
```
/plugin marketplace add /Users/ryowa/Repos/kusari-plugins
```

Install a plugin:
```
/plugin install kusari-dev@kusari-plugins
/reload-plugins
```

## Plugins

- **kusari-dev**: PRD-to-code pipeline.
  - `/plan <prd-file>` to create an implementation plan
  - `/execute <step-file>` to execute a single step
  - `/review [step-file]` to review uncommitted changes
  - `/build <plan-folder-or-step>` to execute and review in an isolated worktree
  - `/finish [step-title]` to commit, merge, push, and clean up the worktree
  - `/evaluate <idea>` to run an investor panel evaluation
