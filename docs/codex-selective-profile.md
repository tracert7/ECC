# Selective Codex profile

This fork adapts two ECC skills for the user's Codex workflow on Windows:

| Skill | Purpose |
| --- | --- |
| `search-first` | Reuse project tools, installed skills and connected tools before choosing a new implementation |
| `verification-loop` | Verify substantial changes with the project's applicable checks and report actual evidence |

The original source is ECC commit
`3f14a103a8694e51c1df9a806217a6d0b5f7a6f7`. The fork's `main` branch retains that
upstream snapshot; the `codex/selective-skills` branch carries these adaptations.
Each selected directory includes the original MIT notice so it can be installed
independently.

The installed profile consists only of these two skill directories. It does not
install the ECC plugin, hooks, agents, MCP configurations, rules, observer,
memory-vault, background service, or automatic update job. Repository-level
`AGENTS.md` and `.codex` configuration are not copied into the user's Codex home.

## Adaptation decisions

- Preserve names and the useful search and verification procedures, while
  removing Claude-only invocation syntax, hard-coded Claude paths, mandatory
  subagents, timed repeat checks, and unnecessary generic advice.
- Search the current project and existing tool catalog first. Reuse the shared
  `Skills.cmd` launcher when available instead of downloading another CLI.
- Use native PowerShell commands and preserve failing process exit codes before
  trimming output. Derive test commands and coverage gates from the project.
- Review staged, unstaged and relevant untracked changes. Report skipped checks
  and target acceptance separately from local test results.
- Keep automatic skill discovery enabled. The user may explicitly invoke
  `$search-first` and `$verification-loop`; ordinary relevant requests can also
  select them.

## Installation

Use Codex's bundled `skill-installer/scripts/install-skill-from-github.py` helper
with `--repo tracert7/ECC`, the reviewed commit SHA as `--ref`, and these paths:

```text
skills/search-first skills/verification-loop
```

The helper installs only the selected directories into the Codex skills home and
refuses to overwrite an existing destination. Use an exact reviewed commit,
not a moving branch, for a reproducible install. Updating upstream code does not
automatically replace these installed adaptations.

Examples:

```text
$search-first Find an existing local tool or maintained package for this feature, then implement the selected approach.
$verification-loop Check the completed change against this project's requirements and tell me what was actually verified.
```
