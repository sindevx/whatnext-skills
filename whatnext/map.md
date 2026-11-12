# whatnext map

`a / b` = same job, pick the first installed.

## Start
| Situation | Skill | Prompt |
|---|---|---|
| Unsure which skill | `agent-skills:using-agent-skills` / `ask-matt` | `/agent-skills:using-agent-skills vague idea for a refund report, where to start?` |
| Find a new skill to install | `find-skills` | `/find-skills skill for OpenAPI docs?` |
| First setup of a repo | `init` / `setup-matt-pocock-skills` | `/init` |
| Did not understand the AI | `wait-what` | `/wait-what explain your last answer again` |
| Understand code or a concept, explain to a beginner | `eli5` / `teach` | `/eli5 the refund folder, for a new hire` |

## Plan
| Situation | Skill | Prompt |
|---|---|---|
| Stress-test an idea or plan | `grilling` | `/grilling plan: daily transfer limit. One question at a time.` |
| New feature, not sure what to build | `superpowers:brainstorming` | `/superpowers:brainstorming QR payment status page` |
| Write a spec first | `agent-skills:spec-driven-development` | `/agent-skills:spec-driven-development partial refund for BNPL` |
| Work bigger than one session | `superpowers:writing-plans` / `wayfinder` | `/superpowers:writing-plans move batch job from cron to queue` |
| Split spec into tasks or tickets | `agent-skills:planning-and-task-breakdown` / `to-tickets` | `/agent-skills:planning-and-task-breakdown docs/refund/spec.md` |
| Module design, seams, architecture | `codebase-design` / `improve-codebase-architecture` | `/codebase-design where should the bank client boundary be?` |
| Confusing terms, glossary, ADR | `domain-modeling` | `/domain-modeling customer vs client vs user, fix glossary` |
| Facts from docs or an API | `research` | `/research vendor API reply for duplicate request id` |
| Diagram | `archify` / `diagram-design:diagram-design` / `pr-lens` | `/archify sequence: App -> Gateway -> Bank` |

## Build
| Situation | Skill | Prompt |
|---|---|---|
| Test-first feature or fix | `tdd` / `superpowers:test-driven-development` | `/tdd amount limit check in TransferService` |
| Code from a plan or ticket | `superpowers:executing-plans` / `implement-spec` | `/superpowers:executing-plans docs/refund/plan.md` |
| One PR per step with review loop | `vtno-implement` / `implement` | `/vtno-implement next step of docs/refund/plan.md` |
| Small steps: build, test, commit | `agent-skills:incremental-implementation` | `/agent-skills:incremental-implementation task 2, commit when green` |
| Clean code, same behavior | `refactor-simple` / `simplify` | `/refactor-simple RefundService, no behavior change` |
| Smallest possible change | `ponytail:ponytail` | `/ponytail null check for amount, smallest diff` |
| Stop the AI doing too much | `karpathy-guidelines` | `/karpathy-guidelines fix only the date format in ReportService` |
| Who calls what, structure | `codebase-memory` | `/codebase-memory who calls RefundService.refund()?` |
| Name a method or variable | `naming` | `/naming method that gets a refund by order id` |
| Prompt for another AI tool | `prompt-master` | `/prompt-master Cursor prompt: paginate order list` |
| Separate work in a worktree | `superpowers:using-git-worktrees` | `/superpowers:using-git-worktrees KKM-123` |

## Debug
| Situation | Skill | Prompt |
|---|---|---|
| Hard bug, slow, throws, fails | `diagnosing-bugs` | `/diagnosing-bugs /orders takes 8s since last release` |
| Test fails, need root cause | `superpowers:systematic-debugging` | `/superpowers:systematic-debugging RefundServiceTest fails after merge` |

## Review
| Situation | Skill | Prompt |
|---|---|---|
| Review branch vs standards and spec | `vtno-code-review` / `mattpocock-skills:code-review` | `/vtno-code-review since main, spec KKM-123` |
| Find bugs in the diff before commit | `code-review` | `/code-review medium` |
| Five-axis quality review | `agent-skills:code-review-and-quality` | `/agent-skills:code-review-and-quality current diff` |
| Over-engineering check | `ponytail:ponytail-review` | `/ponytail:ponytail-review last commit` |
| Security | `security-audit` / `security-review` | `/security-audit src/ SQL injection, card numbers in logs` |

## Ship
| Situation | Skill | Prompt |
|---|---|---|
| PR body | `pr` | `/pr feat/refund-limit, KKM-123` |
| Daily git flow | `git-daily` | `feat start refund-limit` |
| Release checklist | `agent-skills:shipping-and-launch` | `/agent-skills:shipping-and-launch release 2.4.0` |
| Redmine release report | `redmine-report` | `/redmine-report story #12345 from feat/refund-limit` |
| Steps a human must do (secrets, cutover) | `wizard` | `/wizard production cutover steps` |

## Notes
| Situation | Skill | Prompt |
|---|---|---|
| Notes, open tasks, work log | `task-note` | `/task-note add task: refund limit test, due Friday` |
| Weekly report for manager | `dev-journal` | `/dev-journal report this week` |
| Hand work to another agent | `handoff` / `claude-handoff` | `/handoff done, left, files` |
| Session retro | `retro` | `/retro what went wrong` |
| System handover document | `system-handover-guide` | `/system-handover-guide refund service` |
| Code knowledge graph | `graphify` | `/graphify src/` |
