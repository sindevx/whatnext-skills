---
name: whatnext
description: Tells which skill to use next, with an example prompt to copy. With no argument it looks at where you are (git state, chat) and suggests the next 1-3 skills. Use when the user types /whatnext, /whatnext <focus>, /whatnext all, asks "what next", "which skill should I use", "ใช้ skill ไหน", "ต้องใช้อะไรต่อ", or is unsure what to do next.
---

# whatnext — which skill for which job

## How to answer

Pick the mode from the argument.

### Mode A: no argument → "where am I, what next?"

1. Check the chat first. A failing test, an error, or a plan the user just wrote is the strongest signal.
2. Then run these read-only commands. Never run a command that changes files, branches, or remotes.
   - `git status --short --branch`
   - `git log --oneline -5`
   - `git diff --stat`
   - `gh pr view --json state,url` (skip quietly if `gh` is missing or there is no PR)
   Not a git repo: skip this step and say so in one line.
3. Match the state to the first row that fits in "State → next skill" below.
4. Answer in this shape:
   - **Where you are**: one line (branch, changed files, PR state).
   - **Next**: 1-3 skills, best first. Each with an example prompt filled with real names from step 1-2 (branch, file, ticket).
   - Last line: `/whatnext all` shows the full map.

### Mode B: `/whatnext all` → print the full map below, grouped by stage.

### Mode C: any other argument → focus search

1. The argument can be one word (`bug`, `ส่งงาน`) or a sentence ("I need to add a refund limit"). Match by meaning against the "Situation" column. Keywords are hints, not the only way to match.
2. Print only the matching rows (max 5).
3. Then add:
   - **Best pick**: one skill.
   - **Example**: the row's example prompt, rewritten with the user's own words, file, ticket, or error text.
   - **Then**: the next skill from "Common chains".
4. No match: say so in one line, show the stage names, ask the user to pick one.

### Rules for every mode

- Reply language follows the user. Default Thai. Skill names stay exact.
- Never run the suggested skill. Only suggest it. The user decides.
- A Skill cell can hold several names split by ` / `. The first name is the main pick. The others do the same job.
  **Best pick** = the first name that is in this session's skill list.
  None of them installed: still show the row, add "(not installed)", and say what to do instead in one line.

## How to write a good prompt for any skill

A good prompt has four parts. Say them in one or two lines.

1. **Skill**: start with `/skill-name` so the right skill loads.
2. **What**: one sentence, with a real noun (file, ticket, error text), not "fix it".
3. **Where**: the file, folder, branch, or ticket number.
4. **Done when**: how you will know it is finished (a test passes, a report file exists, a PR link).

| Weak prompt | Strong prompt |
|---|---|
| `fix the bug` | `/diagnosing-bugs RefundService.refund() throws NPE when amount is null. Done when a failing test passes.` |
| `review my code` | `/vtno-code-review since main. Check standards and ticket KKM-123.` |
| `make a plan` | `/grilling plan: move card limit check from Controller to Service. Ask me one question at a time.` |

## State → next skill (Mode A)

Use the first row that fits.

| State | Next skill | Why |
|---|---|---|
| Chat shows a failing test or an error | `superpowers:systematic-debugging` / `diagnosing-bugs` | Find the root cause before writing a fix |
| Merge conflict or rebase in progress | `agent-skills:git-workflow-and-versioning` | Finish the git operation first |
| Uncommitted changes, no test file changed | `tdd` | Add the test the change needs |
| Uncommitted changes, test files changed too | `code-review` | Check the diff before you commit |
| Feature branch, clean, commits not in a PR yet | `vtno-code-review` → `pr` | Review the branch, then write the PR body |
| PR is open | `redmine-report` → `dev-journal` | Report the finished work |
| PR merged, or clean on `main` / `master` / `develop` | `task-note` | See what is left and pick the next task |
| Not a git repo, nothing in chat | `superpowers:brainstorming` / `grilling` | Start by shaping the idea |

## Example

User: `/whatnext bug`

Answer:
| Situation | Skill | Example prompt |
|---|---|---|
| บั๊กยาก, ช้า, throw หรือ fail | `diagnosing-bugs` | `/diagnosing-bugs login throws 500 after token refresh` |
| บั๊ก/เทสต์พัง ต้องหา root cause | `superpowers:systematic-debugging` | `/superpowers:systematic-debugging TransferServiceTest fails only on CI` |

- **Best pick**: `diagnosing-bugs`
- **Example**: `/diagnosing-bugs login throws 500 after token refresh`
- **Then**: `tdd` (write the failing test) → `pr`

## Map

### 0. Start / unsure
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| ไม่รู้จะใช้ตัวไหน | `agent-skills:using-agent-skills` / `ask-matt` | `/agent-skills:using-agent-skills I have a vague idea for a refund report, where do I start?` | help, unsure, lost |
| อยากหา skill ใหม่มาติดตั้ง | `find-skills` | `/find-skills is there a skill for writing OpenAPI docs?` | find skill, install, extend |
| ตั้งค่า repo ครั้งแรก (CLAUDE.md, issue tracker, label) | `init` / `setup-matt-pocock-skills` | `/init` | setup, init, first time |
| ยังไม่เข้าใจที่ AI พูด | `wait-what` | `/wait-what explain your last answer about idempotency keys again` | confused, explain again, ไม่เข้าใจ |
| อยากเข้าใจโค้ดหรือแนวคิดในโปรเจกต์ / อธิบายให้มือใหม่ | `eli5` / `teach` | `/eli5 the refund folder, for a new hire` | explain, learn, beginner, เรียน |

### 1. Plan / design
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| ไอเดียหรือแผนยังไม่แน่น อยากโดนซัก | `grilling` | `/grilling plan: add daily transfer limit per customer. Ask one question at a time.` | grill, stress-test, plan |
| ทำฟีเจอร์ใหม่ ยังไม่รู้ต้องทำอะไร | `superpowers:brainstorming` | `/superpowers:brainstorming add QR payment status page` | new feature, idea |
| เขียน spec ก่อนลงมือ | `agent-skills:spec-driven-development` | `/agent-skills:spec-driven-development partial refund for BNPL orders` | spec, requirement |
| งานใหญ่เกิน 1 session | `superpowers:writing-plans` / `wayfinder` | `/superpowers:writing-plans move the batch job from cron to a queue` | huge, epic, roadmap |
| แตก spec เป็น task หรือ ticket พร้อมเกณฑ์ผ่าน | `agent-skills:planning-and-task-breakdown` / `to-tickets` | `/agent-skills:planning-and-task-breakdown docs/refund/spec.md, each task needs a pass check` | tasks, tickets, breakdown |
| ออกแบบ module, หาที่วาง seam, ตรวจ architecture | `codebase-design` / `improve-codebase-architecture` | `/codebase-design where should the bank API client boundary be?` | module, interface, seam, architecture |
| ศัพท์สับสน, เขียน GLOSSARY หรือ ADR | `domain-modeling` | `/domain-modeling we use "customer", "client", "user" for the same thing, fix the glossary` | glossary, ADR, terms |
| หาข้อมูลจาก docs หรือ API | `research` | `/research what does the vendor API return for a duplicate request id? Save to docs/research/` | research, docs, API facts |
| วาดแผนภาพ | `archify` / `diagram-design:diagram-design` / `pr-lens` | `/archify sequence diagram of refund flow: App -> Gateway -> Bank` | diagram, flow, ERD |

### 2. Build
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| เขียนฟีเจอร์หรือแก้บั๊กแบบ test-first | `tdd` / `superpowers:test-driven-development` | `/tdd add amount limit check to TransferService` | test first, red-green |
| ลงมือ code ตาม plan หรือ ticket | `superpowers:executing-plans` / `implement-spec` | `/superpowers:executing-plans docs/refund/plan.md` | implement, ticket, plan |
| ทำ 1 PR หรือทีละ step พร้อมวน review | `vtno-implement` + `vtno-engineering-rules` / `implement` | `/vtno-implement next step of docs/refund/plan.md` | PR, next step |
| ทำทีละส่วน build-test-commit | `agent-skills:incremental-implementation` | `/agent-skills:incremental-implementation task 2 from the plan, commit when tests pass` | incremental, build |
| ทำความสะอาดโค้ด ไม่เปลี่ยน behavior | `refactor-simple` / `simplify` | `/refactor-simple RefundService, behavior must not change` | refactor, clean, simplify |
| อยากได้ code น้อยที่สุด ไม่ทำเกิน | `ponytail:ponytail` | `/ponytail add a null check for amount, smallest diff` | minimal, lazy, smallest diff |
| กัน AI เขียนเกิน / แก้กว้างเกิน | `karpathy-guidelines` | `/karpathy-guidelines fix only the date format in ReportService` | surgical, overcomplicate |
| ถามโค้ดว่าใครเรียกใคร / โครงสร้าง | `codebase-memory` | `/codebase-memory who calls RefundService.refund()?` | callers, call chain, dead code |
| ตั้งชื่อ method หรือ variable | `naming` | `/naming name for a method that gets a refund by order id` | name, rename |
| เขียน prompt ให้ AI ตัวอื่น | `prompt-master` | `/prompt-master write a Cursor prompt to add pagination to the order list` | prompt, cursor, midjourney |
| ใช้ git worktree แยกงาน | `superpowers:using-git-worktrees` | `/superpowers:using-git-worktrees start KKM-123 in its own worktree` | worktree, isolate |

### 3. Debug
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| บั๊กยาก, ช้า, throw หรือ fail | `diagnosing-bugs` | `/diagnosing-bugs /orders endpoint takes 8s since last release` | bug, slow, error, fail |
| บั๊ก/เทสต์พัง ต้องหา root cause | `superpowers:systematic-debugging` | `/superpowers:systematic-debugging RefundServiceTest.shouldRejectZero fails after merge` | root cause, test failure |

### 4. Review / security
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| รีวิว branch หรือ PR เทียบ standards + spec | `vtno-code-review` / `mattpocock-skills:code-review` | `/vtno-code-review since main, spec is ticket KKM-123` | review, branch, PR, spec |
| หาบั๊กใน diff ปัจจุบัน ก่อน commit | `code-review` | `/code-review medium` | bugs, diff, before commit |
| รีวิวโค้ดห้ามิติ (correctness, readability, security, ...) | `agent-skills:code-review-and-quality` | `/agent-skills:code-review-and-quality current diff` | review, quality |
| ตรวจ over-engineering | `ponytail:ponytail-review` | `/ponytail:ponytail-review last commit` | over-engineered |
| ตรวจความปลอดภัย | `security-audit` / `security-review` | `/security-audit src/ focus on SQL injection and logging of card numbers` | security, vuln, audit |

### 5. Ship / report
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| เขียน PR body | `pr` | `/pr for branch feat/refund-limit, ticket KKM-123` | pull request, description |
| git flow ประจำวัน (feat/bugfix/rel/hotfix) | `git-daily` | `feat start refund-limit` | feat start, release, hotfix |
| checklist ก่อนปล่อย | `agent-skills:shipping-and-launch` | `/agent-skills:shipping-and-launch release 2.4.0, go/no-go list` | go/no-go, launch |
| สร้างรายงาน release สำหรับ Redmine | `redmine-report` | `/redmine-report story #12345 from commits on feat/refund-limit` | redmine, release report |
| ต้องมีคนทำ step เอง (credential, CI secret, cutover) | `wizard` | `/wizard walk me through the production cutover steps I must do by hand` | cutover, deploy steps |

### 6. Notes / handoff / retro
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| จดงาน, งานค้าง, log งาน | `task-note` | `/task-note add task: write test for refund limit, due Friday` | note, task, งานค้าง |
| รายงานงานให้หัวหน้า / สรุปสัปดาห์ | `dev-journal` | `/dev-journal report this week for my manager` | weekly, report, journal |
| ส่งงานต่อ agent อื่น หรือ background agent | `handoff` / `claude-handoff` | `/handoff what is done, what is left, which files` | handoff, background agent |
| จบ session อยาก retro | `retro` | `/retro what went wrong in this session` | retro, lessons |
| เอกสารส่งมอบระบบ | `system-handover-guide` | `/system-handover-guide handover for the refund service` | handover |
| ทำ knowledge graph ของโค้ด | `graphify` | `/graphify src/` | graph, codebase map |

## Common chains

Use these for the **Then** line.

| Job | Chain |
|---|---|
| New feature | `grilling` → `agent-skills:spec-driven-development` → `agent-skills:planning-and-task-breakdown` → `tdd` → `vtno-code-review` → `pr` |
| Bug | `diagnosing-bugs` → `tdd` (failing test first) → `code-review` → `pr` |
| Refactor | `codebase-design` → `refactor-simple` → `code-review` |
| Finish and report | `pr` → `redmine-report` → `dev-journal` |
| Stuck or confused | `wait-what` → `agent-skills:using-agent-skills` |

## Needs

This file is only a map. The skills it points to come from other places:
`superpowers`, `agent-skills` (addy), `mattpocock-skills`, `vtno`, `ponytail`, `diagram-design`,
plus own skills: `task-note`, `dev-journal`, `git-daily`, `redmine-report`, `refactor-simple`,
`naming`, `eli5`, `system-handover-guide`, `graphify`. A missing one is fine (see "Rules for every mode").

## Keep this file true

Skill names change when plugins update. Edit this one file to add or remove a skill.
When you add a row, add its example prompt too. After any edit, run the cases in `evals.md` (root of the `whatnext-skills` repo).
