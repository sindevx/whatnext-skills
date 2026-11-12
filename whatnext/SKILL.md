---
name: whatnext
description: Skill map. Tells which skill to use for what you want to do now, with an example prompt to copy. Use when the user types /whatnext, /whatnext <focus>, asks "which skill should I use", "ใช้ skill ไหน", "ต้องใช้อะไรต่อ", or is unsure what to do next.
---

# whatnext — which skill for which job

## How to answer

1. Read the argument (the user's focus). Examples: `bug`, `review`, `plan`, `pr`, `test`, `ส่งงาน`.
2. No argument: print the full map below, grouped by stage. Keep the Thai text. Print the "Example prompt" column too.
3. With argument: match it to the "Situation" and "Keywords" columns. Print only the matching rows (max 5).
   Then add:
   - **Best pick**: one skill.
   - **Example**: copy the "Example prompt" from the row. If the user gave details (file, ticket, error), put them into the prompt.
   - **Then**: the next skill from "Common chains" below.
4. No match: say so in one line, show the stage names, ask the user to pick one.
5. Reply language follows the user. Default Thai. Skill names stay exact.
6. Never run the skill. Only suggest it. The user decides.
7. A skill name in the table that is not in this session's skill list: still show the row, add "(not installed)". Do not hide it.

## How to write a good prompt for any skill

A good prompt has four parts. Say them in one or two lines.

1. **Skill**: start with `/skill-name` so the right skill loads.
2. **What**: one sentence, with a real noun (file, ticket, error text), not "fix it".
3. **Where**: the file, folder, branch, or ticket number.
4. **Done when**: how you will know it is finished (a test passes, a report file exists, a PR link).

| Weak prompt | Strong prompt |
|---|---|
| `fix the bug` | `/diagnosing-bugs RefundService.refund() throws NPE when amount is null. Done when a failing test passes.` |
| `review my code` | `/code-review since main. Check standards and ticket KKM-123.` |
| `make a plan` | `/grilling plan: move card limit check from Controller to Service. Ask me one question at a time.` |

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
| ไม่รู้จะใช้ตัวไหน | `ask-matt` | `/ask-matt I have a vague idea for a refund report, where do I start?` | help, unsure, lost |
| อยากหา skill ใหม่มาติดตั้ง | `find-skills` | `/find-skills is there a skill for writing OpenAPI docs?` | find skill, install, extend |
| ตั้งค่า repo ครั้งแรก (issue tracker, label, โครง docs) | `setup-matt-pocock-skills` | `/setup-matt-pocock-skills set up this repo, we use Redmine for issues` | setup, init, first time |
| ยังไม่เข้าใจที่ AI พูด | `wait-what` | `/wait-what explain your last answer about idempotency keys again` | confused, explain again, ไม่เข้าใจ |
| อยากเรียนแนวคิดใหม่ในโปรเจกต์ | `teach` | `/teach how does the retry logic in PaymentClient work?` | learn, teach, เรียน |
| อธิบายโค้ดให้มือใหม่ | `eli5` | `/eli5 src/main/java/.../refund folder, for a new hire` | explain, beginner, onboarding |

### 1. Plan / design
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| ไอเดียหรือแผนยังไม่แน่น อยากโดนซัก | `grilling` | `/grilling plan: add daily transfer limit per customer. Ask one question at a time.` | grill, stress-test, plan |
| ทำฟีเจอร์ใหม่ ยังไม่รู้ต้องทำอะไร | `superpowers:brainstorming` | `/superpowers:brainstorming add QR payment status page` | new feature, idea |
| เขียน spec ก่อนลงมือ | `agent-skills:spec` | `/agent-skills:spec partial refund for BNPL orders` | spec, requirement |
| งานใหญ่เกิน 1 session | `wayfinder` | `/wayfinder move the whole batch job from cron to a queue` | huge, epic, roadmap |
| แตก spec เป็น ticket | `to-tickets` | `/to-tickets docs/refund/spec.md` | tickets, breakdown |
| แตกงานเป็น task พร้อมเกณฑ์ผ่าน | `agent-skills:plan` | `/agent-skills:plan from docs/refund/spec.md, each task needs a pass check` | tasks, estimate |
| ออกแบบ module, หาที่วาง seam | `codebase-design` | `/codebase-design where should the bank API client boundary be?` | module, interface, seam |
| ตรวจ architecture ทั้ง repo | `improve-codebase-architecture` | `/improve-codebase-architecture find shallow modules in src/` | architecture, deepen |
| ศัพท์สับสน, เขียน GLOSSARY หรือ ADR | `domain-modeling` | `/domain-modeling we use "customer", "client", "user" for the same thing, fix the glossary` | glossary, ADR, terms |
| หาข้อมูลจาก docs หรือ API | `research` | `/research what does the vendor API return for a duplicate request id? Save to docs/research/` | research, docs, API facts |
| วาดแผนภาพ | `archify` / `diagram-design:diagram-design` / `pr-lens` | `/archify sequence diagram of refund flow: App -> Gateway -> Bank` | diagram, flow, ERD |

### 2. Build
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| เขียนฟีเจอร์หรือแก้บั๊กแบบ test-first | `tdd` | `/tdd add amount limit check to TransferService` | test first, red-green |
| ลงมือ code ตาม ticket | `implement-spec` | `/implement-spec KKM-123` | implement, ticket |
| ทำ 1 PR หรือทีละ step พร้อมวน review | `implement` + `engineering-rules` | `/implement next step of docs/refund/plan.md` | PR, next step |
| ทำทีละส่วน build-test-commit | `agent-skills:build` | `/agent-skills:build task 2 from the plan, commit when tests pass` | incremental, build |
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
| รีวิว branch หรือ PR (standards + spec) | `code-review` | `/code-review since main, spec is ticket KKM-123` | review, branch, PR |
| รีวิวโค้ดห้ามิติ | `agent-skills:review` | `/agent-skills:review current diff` | review, quality |
| ตรวจ over-engineering | `ponytail:ponytail-review` | `/ponytail:ponytail-review last commit` | over-engineered |
| ตรวจความปลอดภัย | `security-audit` / `security-review` | `/security-audit src/ focus on SQL injection and logging of card numbers` | security, vuln, audit |

### 5. Ship / report
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| เขียน PR body | `pr` | `/pr for branch feat/refund-limit, ticket KKM-123` | pull request, description |
| git flow ประจำวัน (feat/bugfix/rel/hotfix) | `git-daily` | `feat start refund-limit` | feat start, release, hotfix |
| checklist ก่อนปล่อย | `agent-skills:ship` | `/agent-skills:ship release 2.4.0, go/no-go list` | go/no-go, launch |
| สร้างรายงาน release สำหรับ Redmine | `redmine-report` | `/redmine-report story #12345 from commits on feat/refund-limit` | redmine, release report |
| ต้องมีคนทำ step เอง (credential, CI secret, cutover) | `wizard` | `/wizard walk me through the production cutover steps I must do by hand` | cutover, deploy steps |

### 6. Notes / handoff / retro
| Situation | Skill | Example prompt | Keywords |
|---|---|---|---|
| จดงาน, งานค้าง, log งาน | `task-note` | `/task-note add task: write test for refund limit, due Friday` | note, task, งานค้าง |
| รายงานงานให้หัวหน้า / สรุปสัปดาห์ | `dev-journal` | `/dev-journal report this week for my manager` | weekly, report, journal |
| ส่งงานต่อ agent อื่น (เอกสาร) | `handoff` | `/handoff what is done, what is left, which files` | handoff |
| ส่งงานต่อให้ background agent ทันที | `claude-handoff` | `/claude-handoff finish the remaining tests in the background` | background agent |
| จบ session อยาก retro | `retro` | `/retro what went wrong in this session` | retro, lessons |
| เอกสารส่งมอบระบบ | `system-handover-guide` | `/system-handover-guide handover for the refund service` | handover |
| ทำ knowledge graph ของโค้ด | `graphify` | `/graphify src/` | graph, codebase map |

## Common chains

Use these for the **Then** line.

| Job | Chain |
|---|---|
| New feature | `grilling` → `agent-skills:spec` → `to-tickets` → `tdd` → `code-review` → `pr` |
| Bug | `diagnosing-bugs` → `tdd` (failing test first) → `code-review` → `pr` |
| Refactor | `codebase-design` → `refactor-simple` → `code-review` |
| Finish and report | `pr` → `redmine-report` → `dev-journal` |
| Stuck or confused | `wait-what` → `ask-matt` |

## Needs

This file is only a map. The skills it points to come from other places:
`superpowers`, `agent-skills` (addy), `mattpocock-skills`, `ponytail`, `diagram-design`,
plus own skills: `task-note`, `dev-journal`, `git-daily`, `redmine-report`, `refactor-simple`,
`naming`, `eli5`, `system-handover-guide`, `graphify`. Missing one is fine (rule 7).

## Keep this file true
Skill names change when plugins update. If a name above is not in the skills list of this session, say so in one line and use the closest match. Edit this one file to add or remove a skill. When you add a row, add its example prompt too.
