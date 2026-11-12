---
name: whatnext
description: Skill map. Tells which skill to use for what you want to do now. Use when the user types /whatnext, /whatnext <focus>, asks "which skill should I use", "ใช้ skill ไหน", "ต้องใช้อะไรต่อ", or is unsure what to do next.
---

# whatnext — which skill for which job

## How to answer

1. Read the argument (the user's focus). Examples: `bug`, `review`, `plan`, `pr`, `test`, `ส่งงาน`.
2. No argument: print the full map below, grouped by stage. Keep the Thai text.
3. With argument: match it to the "Situation" and "Keywords" columns. Print only the matching rows (max 5).
   Then add:
   - **Best pick**: one skill.
   - **Example**: one line the user can type, like `/tdd add amount limit check`.
   - **Then**: the usual next skill after it.
4. No match: say so in one line, show the stage names, ask the user to pick one.
5. Reply language follows the user. Default Thai. Skill names stay exact.
6. Never run the skill. Only suggest it. The user decides.
7. A skill name in the table that is not in this session's skill list: still show the row, add "(not installed)". Do not hide it.

## Example

User: `/whatnext bug`

Answer:
| Situation | Skill |
|---|---|
| บั๊กยาก, ช้า, throw หรือ fail | `diagnosing-bugs` |
| บั๊ก/เทสต์พัง ต้องหา root cause | `superpowers:systematic-debugging` |

- **Best pick**: `diagnosing-bugs`
- **Example**: `/diagnosing-bugs login throws 500 after token refresh`
- **Then**: `tdd` (write the failing test) → `pr`

## Map

### 0. Start / unsure
| Situation | Skill | Keywords |
|---|---|---|
| ไม่รู้จะใช้ตัวไหน | `ask-matt` | help, unsure, lost |
| อยากหา skill ใหม่มาติดตั้ง | `find-skills` | find skill, install, extend |
| ตั้งค่า repo ครั้งแรก (issue tracker, label, โครง docs) | `setup-matt-pocock-skills` | setup, init, first time |
| ยังไม่เข้าใจที่ AI พูด | `wait-what` | confused, explain again, ไม่เข้าใจ |
| อยากเรียนแนวคิดใหม่ในโปรเจกต์ | `teach` | learn, teach, เรียน |
| อธิบายโค้ดให้มือใหม่ | `eli5` | explain, beginner, onboarding |

### 1. Plan / design
| Situation | Skill | Keywords |
|---|---|---|
| ไอเดียหรือแผนยังไม่แน่น อยากโดนซัก | `grilling` | grill, stress-test, plan |
| ทำฟีเจอร์ใหม่ ยังไม่รู้ต้องทำอะไร | `superpowers:brainstorming` | new feature, idea |
| เขียน spec ก่อนลงมือ | `agent-skills:spec` | spec, requirement |
| งานใหญ่เกิน 1 session | `wayfinder` | huge, epic, roadmap |
| แตก spec เป็น ticket | `to-tickets` | tickets, breakdown |
| แตกงานเป็น task พร้อมเกณฑ์ผ่าน | `agent-skills:plan` | tasks, estimate |
| ออกแบบ module, หาที่วาง seam | `codebase-design` | module, interface, seam |
| ตรวจ architecture ทั้ง repo | `improve-codebase-architecture` | architecture, deepen |
| ศัพท์สับสน, เขียน GLOSSARY หรือ ADR | `domain-modeling` | glossary, ADR, terms |
| หาข้อมูลจาก docs หรือ API | `research` | research, docs, API facts |
| วาดแผนภาพ | `archify` / `diagram-design:diagram-design` / `pr-lens` | diagram, flow, ERD |

### 2. Build
| Situation | Skill | Keywords |
|---|---|---|
| เขียนฟีเจอร์หรือแก้บั๊กแบบ test-first | `tdd` | test first, red-green |
| ลงมือ code ตาม ticket | `implement-spec` | implement, ticket |
| ทำ 1 PR หรือทีละ step พร้อมวน review | `implement` + `engineering-rules` | PR, next step |
| ทำทีละส่วน build-test-commit | `agent-skills:build` | incremental, build |
| ทำความสะอาดโค้ด ไม่เปลี่ยน behavior | `refactor-simple` / `simplify` | refactor, clean, simplify |
| อยากได้ code น้อยที่สุด ไม่ทำเกิน | `ponytail:ponytail` | minimal, lazy, smallest diff |
| กัน AI เขียนเกิน / แก้กว้างเกิน | `karpathy-guidelines` | surgical, overcomplicate |
| ถามโค้ดว่าใครเรียกใคร / โครงสร้าง | `codebase-memory` | callers, call chain, dead code |
| เขียน prompt ให้ AI ตัวอื่น | `prompt-master` | prompt, cursor, midjourney |
| ตั้งชื่อ method หรือ variable | `naming` | name, rename |
| ใช้ git worktree แยกงาน | `superpowers:using-git-worktrees` | worktree, isolate |

### 3. Debug
| Situation | Skill | Keywords |
|---|---|---|
| บั๊กยาก, ช้า, throw หรือ fail | `diagnosing-bugs` | bug, slow, error, fail |
| บั๊ก/เทสต์พัง ต้องหา root cause | `superpowers:systematic-debugging` | root cause, test failure |

### 4. Review / security
| Situation | Skill | Keywords |
|---|---|---|
| รีวิว branch หรือ PR (standards + spec) | `code-review` | review, branch, PR |
| รีวิวโค้ดห้ามิติ | `agent-skills:review` | review, quality |
| ตรวจ over-engineering | `ponytail:ponytail-review` | over-engineered |
| ตรวจความปลอดภัย | `security-audit` / `security-review` | security, vuln, audit |

### 5. Ship / report
| Situation | Skill | Keywords |
|---|---|---|
| เขียน PR body | `pr` | pull request, description |
| git flow ประจำวัน (feat/bugfix/rel/hotfix) | `git-daily` | feat start, release, hotfix |
| checklist ก่อนปล่อย | `agent-skills:ship` | go/no-go, launch |
| สร้างรายงาน release สำหรับ Redmine | `redmine-report` | redmine, release report |
| ต้องมีคนทำ step เอง (credential, CI secret, cutover) | `wizard` | cutover, deploy steps |

### 6. Notes / handoff / retro
| Situation | Skill | Keywords |
|---|---|---|
| จดงาน, งานค้าง, log งาน | `task-note` | note, task, งานค้าง |
| รายงานงานให้หัวหน้า / สรุปสัปดาห์ | `dev-journal` | weekly, report, journal |
| ส่งงานต่อ agent อื่น (เอกสาร) | `handoff` | handoff |
| ส่งงานต่อให้ background agent ทันที | `claude-handoff` | background agent |
| จบ session อยาก retro | `retro` | retro, lessons |
| เอกสารส่งมอบระบบ | `system-handover-guide` | handover |
| ทำ knowledge graph ของโค้ด | `graphify` | graph, codebase map |

## Needs

This file is only a map. The skills it points to come from other places:
`superpowers`, `agent-skills` (addy), `mattpocock-skills`, `ponytail`, `diagram-design`,
plus own skills: `task-note`, `dev-journal`, `git-daily`, `redmine-report`, `refactor-simple`,
`naming`, `eli5`, `system-handover-guide`, `graphify`. Missing one is fine (rule 7).

## Keep this file true
Skill names change when plugins update. If a name above is not in the skills list of this session, say so in one line and use the closest match. Edit this one file to add or remove a skill.
