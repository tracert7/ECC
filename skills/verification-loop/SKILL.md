---
name: verification-loop
description: "Verify a substantial implementation, refactor or repair using the project's own checks and an honest evidence report. Use before delivery or a PR, or for 검증해줘 requests about changed software. Skip unrelated research and trivial prose edits."
license: MIT
metadata:
  origin: ECC
  upstream_commit: 3f14a103a8694e51c1df9a806217a6d0b5f7a6f7
  adaptation: Codex selective profile
---

# Verify the requested result

Inspect the project's instructions, changed files, manifests, and CI checks.
Choose checks for the actual change and its acceptance criteria. Reuse the
project's installed tools and coverage requirements; do not add a test framework,
scanner, arbitrary coverage threshold, or complete ECC plugin just to run this skill.

## Run applicable checks

| Check | What to establish |
| --- | --- |
| Build or package | The changed application or distributable can be produced |
| Types and static checks | Relevant compiler and type constraints still hold |
| Lint | The project's configured style and correctness checks pass |
| Tests and behavior | Focused tests or a meaningful smoke test cover the changed behavior |
| Security | Relevant existing checks cover changed trust boundaries or dependencies |
| Change review | The full requested change is present and unrelated work is preserved |

Use the project's commands, not a fixed JavaScript checklist. A Python utility,
Roblox module, desktop app, and documentation-only change need different checks.
For a small reversible change, existing checks or direct inspection may suffice.
Mark an inapplicable check N/A with its reason. Mark an unavailable or unexecuted
check NOT RUN; never turn a skipped command into PASS.

Preserve native command exit codes. On Windows, capture `$LASTEXITCODE`
immediately, before summarizing output or running another native command. For
example, replace the test command below with the project's actual command:

```powershell
$checkOutput = & python -m unittest discover -s tests 2>&1
$checkExit = $LASTEXITCODE
$checkOutput | Select-Object -Last 40
if ($checkExit -ne 0) { exit $checkExit }
```

Avoid Bash-only `pipefail`, `tail`, `sed`, or `/dev/null` examples in native
PowerShell. Retain enough failure output to diagnose the check. Fix failures
caused by the requested work and rerun the affected checks; repeat broader tests
only when new edits or unresolved evidence justify it. Never suppress a failure
to obtain a green report.

## Review scope and target behavior

In Git, start with `git status --short`, inspect both unstaged and staged diffs,
and inspect relevant untracked files. Use an explicitly known task or PR base
when needed; `HEAD~1` is not a reliable baseline for arbitrary work. Keep unrelated
user changes intact. Outside a Git repository, review the actual output files
and available source snapshots instead.

Scope security inspection to the change and relevant existing tools. Redact any
secret findings; report the path and category without printing the secret.
Pattern searches alone do not establish a security audit.

If acceptance requires a running application, editor, browser, device, or remote
environment, record that target check separately from local checks. A successful
compile does not prove the application works in its target. Perform already
authorized target checks when available; do not deploy, upload, publish, or alter
an account without authorization for that action.

## Report the evidence

Give a concise result in the user's language: which checks passed, what failed
or was not run, and any material limitation. Include command or artifact evidence
where it helps review. Report target acceptance as VERIFIED, FAILED, NOT RUN, or
N/A with the environment and evidence when applicable. Do not claim complete
verification while a required check remains unexecuted.

Source and license: [ECC upstream skill](https://github.com/affaan-m/ECC/blob/3f14a103a8694e51c1df9a806217a6d0b5f7a6f7/skills/verification-loop/SKILL.md),
adapted for this Codex profile. The original MIT notice is in [LICENSE](LICENSE).
