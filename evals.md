# whatnext test cases

Run each case after you edit `whatnext/SKILL.md`. Set up the state, type the input,
and check that **Best pick** (or the first skill under **Next**) matches.
A case fails if the pick is wrong or if the skill runs anything that changes files.

| # | State | Input | Expected best pick |
|---|---|---|---|
| 1 | Any repo | `/whatnext bug` | `diagnosing-bugs` |
| 2 | Any repo | `/whatnext ส่งงาน` | `pr` |
| 3 | Any repo | `/whatnext I need to add a refund limit and I'm not sure how` | `superpowers:brainstorming` or `grilling` |
| 4 | Any repo | `/whatnext unsure` | `agent-skills:using-agent-skills` (not `ask-matt` when `ask-matt` is not installed) |
| 5 | Feature branch, one file edited, no test file changed | `/whatnext` | `tdd` |
| 6 | Feature branch, clean, 2 commits ahead of `main`, no PR | `/whatnext` | `vtno-code-review`, then `pr` |
| 7 | Clean `main` | `/whatnext` | `task-note` |
| 8 | Folder that is not a git repo, empty chat | `/whatnext` | `superpowers:brainstorming` or `grilling`, and one line saying it is not a git repo |
| 9 | Any repo | `/whatnext all` | Full map with all 7 stages |
| 10 | Any repo | `/whatnext retro` | `retro`, marked "(not installed)" if missing, with one line on what to do instead |
