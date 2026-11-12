---
name: whatnext
description: Suggests the next skill to use, with a prompt to copy. Use for /whatnext, "what next", "which skill", "ใช้ skill ไหน", "ต้องใช้อะไรต่อ".
---

# whatnext

Suggest only. Never run the suggested skill. Reply in the user's language (default Thai). Keep skill names exact. Short, but every pick gets a one-line reason: the user must see why, not only what.

## Modes

**A. No argument** — where am I, what next?
1. A failing test, error, or plan in the chat wins over git state.
2. Else run ONE read-only Bash call (never change files, branches, or remotes):
   `git status -sb 2>&1 | head -15; git log --oneline -3 2>&1; gh pr view --json state -q .state 2>&1 | head -1`
3. Take the first row in "State" that fits. Answer in at most 6 lines:
   - **Where you are**: branch, changed files, PR.
   - **Next**: 1-2 skills. Each: skill, one-line why tied to this state, prompt filled with real names.
   - **Then**: the skill after it.
   Do not read `map.md`.

**B. `all`** — read `map.md` in this skill's folder. Print the full map grouped by stage (Situation | Skill | Example prompt). Drop the Keywords column.

**C. Any other argument** — read `map.md` (skip if already read in this session). Match by meaning (a word or a full sentence). Answer:
- A table of the matching map rows (max 5): Situation | Skill | Example prompt. Skill = first installed name.
- **Best pick**: one skill + one-line why it fits this request.
- **Prompt**: the row's prompt rewritten with the user's words, file, ticket, or error. Real names, not `<placeholders>`, when the chat has them.
- **Also**: skills from the table not picked, each with a 3-5 word purpose. Skip if the table already shows them.
- **Then**: next skill from "Chains".
- **Watch out**: one line, only if a real risk applies (money/auth/card data → `security-audit`; behavior must not change → write a test first; skill not installed → say the fallback).
Request has 2+ jobs (e.g. feature and refactor): list the jobs in the order to do them, one best pick each, with a one-line reason for the order.
No match: say so, list the stage names, ask the user to pick.
Only suggest skills in this session's skill list. If the best fit is outside the map but installed, you may add it under **Also**.

A cell like `a / b`: pick the first name in this session's skill list. None installed: add "(not installed)" and say what to do instead.

Good prompt = `/skill` + what (real noun) + where (file, branch, ticket) + done when.

## State (Mode A, first match wins)

| State | Skill | Prompt |
|---|---|---|
| Failing test or error in chat | `superpowers:systematic-debugging` / `diagnosing-bugs` | `/superpowers:systematic-debugging <test or error>` |
| Merge conflict or rebase | `agent-skills:git-workflow-and-versioning` | `/agent-skills:git-workflow-and-versioning finish rebase on <branch>` |
| Changes, no test file changed | `tdd` | `/tdd add test for <changed file>` |
| Changes, test files changed too | `code-review` | `/code-review medium` |
| Feature branch, clean, no PR | `vtno-code-review` → `mattpocock-skills:pr` | `/vtno-code-review since main` |
| PR open | `redmine-report` → `dev-journal` | `/redmine-report from commits on <branch>` |
| Clean main/master/develop, or PR merged | `task-note` | `/task-note what is left?` |
| Not a git repo, nothing in chat | `superpowers:brainstorming` / `grilling` | `/grilling plan: <idea>` |

## Chains

- Feature: `grilling` → `agent-skills:spec-driven-development` → `agent-skills:planning-and-task-breakdown` → `tdd` → `vtno-code-review` → `mattpocock-skills:pr`
- Bug: `diagnosing-bugs` → `tdd` → `code-review` → `mattpocock-skills:pr`
- Refactor: `codebase-design` → `refactor-simple` → `code-review`
- Report: `mattpocock-skills:pr` → `redmine-report` → `dev-journal`
