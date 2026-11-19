---
name: search-first
description: "Find reusable tools, MCPs, skills and packages before implementing new functionality or selecting an integration. Use for substantial additions and requests such as 기존 도구부터 찾아줘. Skip routine edits and tasks already covered by a selected tool."
license: MIT
metadata:
  origin: ECC
  upstream_commit: 3f14a103a8694e51c1df9a806217a6d0b5f7a6f7
  adaptation: Codex selective profile
---

# Search before implementing

Choose whether to reuse, extend, compose, or build. Match the depth of research
to the decision: a small helper may need only a local search; a new integration
usually needs current upstream evidence.

## Start with what is available

- Read the current project's instructions and search its files with `rg --files`
  and targeted `rg` queries. Inspect existing dependencies and helpers first.
- Use the current skill catalog and discover relevant connected tools. Prefer a
  suitable existing plugin or installed application for its supported operations.
  A missing connector is a coverage gap, not evidence that no solution exists.
- For skill discovery, use `find-skills` if available. On the user's Windows
  toolbox setup, use the existing `Skills.cmd find <query>` launcher in
  `$env:USERPROFILE/Desktop/GITHUB` when present; do not fetch another CLI with
  `npx` merely to search. From another project, invoke that launcher's full path.
- When a package or service is needed, inspect its official repository and
  documentation. Verify current compatibility, maintenance, license, and required
  credentials before recommending adoption. Use only relevant search channels;
  do not run an inventory of every registry, account, or configuration file.

## Make the decision

Compare only the strongest relevant candidates. Judge the required function,
actual platform support, dependency footprint, maintenance, license, and the
effort to integrate with this project. Popularity is supporting evidence, not a
substitute for inspecting the source and documentation.

| Finding | Preferred action |
| --- | --- |
| Existing project tool already meets the need | Reuse it |
| Maintained external tool fits the constraints | Adopt it |
| Useful foundation needs a small adapter | Extend it |
| Several small tools fit together cleanly | Compose them |
| No suitable option found within a relevant search | Build, explaining the gap |

Report the recommendation, the decisive tradeoff, and links or local file
evidence. Distinguish "documented support" from "tested on this machine" and
state material search gaps. Avoid reporting hypothetical scores or test results.
Stop researching once the evidence supports the next practical step.

## Continue the authorized work

A discovery-only request ends with findings. When the user has also asked for
installation or implementation, proceed with that work within the agreed scope;
do not ask again for authorization already given. Preserve unrelated tools and
configuration. Forks, publishing, account changes, and updates stay within the
user's actual request.

Use the tools and shell exposed by the current Codex session. On Windows use
PowerShell-compatible commands; Claude-specific `Agent(...)`, `/commands`, and
`~/.claude` paths are not prerequisites. Use subagents only when authorized and
when an independent task justifies them, not as a required research step.

Source and license: [ECC upstream skill](https://github.com/affaan-m/ECC/blob/3f14a103a8694e51c1df9a806217a6d0b5f7a6f7/skills/search-first/SKILL.md),
adapted for this Codex profile. The original MIT notice is in [LICENSE](LICENSE).
