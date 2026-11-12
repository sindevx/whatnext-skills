# whatnext map

`a / b` = same job, pick the first installed. Keywords are hints; match by meaning.


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
| ลองไอเดียเร็ว ๆ ทำ prototype ทิ้ง | `mattpocock-skills:prototype` | `/mattpocock-skills:prototype transfer screen flow, throwaway` | prototype, spike, try |
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
| เขียน CLAUDE.md, skill, prompt ที่ agent ต้องอ่าน | `mattpocock-skills:writing-for-agents` | `/mattpocock-skills:writing-for-agents rewrite CLAUDE.md for this repo` | CLAUDE.md, agent docs |
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
| เขียน PR body | `mattpocock-skills:pr` / `pr` | `/mattpocock-skills:pr for branch feat/refund-limit, ticket KKM-123` | pull request, description |
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
