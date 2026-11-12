---
name: whatnext
description: Suggests the next skill to use, with a prompt to copy. Use for /whatnext, "what next", "which skill", "ใช้ skill ไหน", "ต้องใช้อะไรต่อ".
---

# whatnext

Suggest only. Never run the suggested skill. Reply in the user's language (default Thai). Keep skill names exact. Keep the answer short.

## Modes

**A. No argument** — where am I, what next?
1. A failing test, error, or plan in the chat wins over git state.
2. Else run ONE read-only Bash call (never change files, branches, or remotes):
   `git status -sb 2>&1 | head -15; git log --oneline -3 2>&1; gh pr view --json state -q .state 2>&1 | head -1`
3. Take the first row in "State" that fits. Answer in at most 4 lines:
   `Where you are: <branch, changed files, PR>` then 1-2 skills, each with its prompt filled with real names.
   Do not read `map.md`.

**B. `all`** — read `map.md` in this skill's folder. Print one line per stage: stage name, then skill names only.

**C. Any other argument** — read `map.md`. Match by meaning (a word or a full sentence). Answer:
- **Best pick**: one skill, with the row's prompt rewritten using the user's words, file, ticket, or error.
- **Also**: up to 2 other skills, names only.
- **Then**: next skill from "Chains".
No match: say so, list the stage names, ask the user to pick.

A cell like `a / b`: pick the first name in this session's skill list. None installed: add "(not installed)" and say what to do instead.

Good prompt = `/skill` + what (real noun) + where (file, branch, ticket) + done when.

## State (Mode A, first match wins)

| State | Skill | Prompt |
|---|---|---|
| Failing test or error in chat | `superpowers:systematic-debugging` / `diagnosing-bugs` | `/superpowers:systematic-debugging <test or error>` |
| Merge conflict or rebase | `agent-skills:git-workflow-and-versioning` | `/agent-skills:git-workflow-and-versioning finish rebase on <branch>` |
| Changes, no test file changed | `tdd` | `/tdd add test for <changed file>` |
| Changes, test files changed too | `code-review` | `/code-review medium` |
| Feature branch, clean, no PR | `vtno-code-review` → `pr` | `/vtno-code-review since main` |
| PR open | `redmine-report` → `dev-journal` | `/redmine-report from commits on <branch>` |
| Clean main/master/develop, or PR merged | `task-note` | `/task-note what is left?` |
| Not a git repo, nothing in chat | `superpowers:brainstorming` / `grilling` | `/grilling plan: <idea>` |

## Chains

- Feature: `grilling` → `agent-skills:spec-driven-development` → `agent-skills:planning-and-task-breakdown` → `tdd` → `vtno-code-review` → `pr`
- Bug: `diagnosing-bugs` → `tdd` → `code-review` → `pr`
- Refactor: `codebase-design` → `refactor-simple` → `code-review`
- Report: `pr` → `redmine-report` → `dev-journal`
