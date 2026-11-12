# whatnext-skills

A Claude Code skill map. Type `/whatnext` and it tells you which skill fits your job right now.
It only suggests. It never runs the skill for you.

## Install

```bash
git clone https://github.com/sindevx/whatnext-skills.git
cp -R whatnext-skills/whatnext ~/.claude/skills/whatnext
```

## Use

| You type | You get |
|---|---|
| `/whatnext` | Looks at the chat and your git state (read-only), then suggests the next 1-3 skills with filled-in prompts |
| `/whatnext bug` or `/whatnext I need to add a refund limit` | Up to 5 matching rows, one best pick, one example prompt, and the usual next skill |
| `/whatnext all` | The full map, grouped by stage (start, plan, build, debug, review, ship, notes) |

Every row has an example prompt you can copy. A "Common chains" table shows the usual next skill. Replies are in Thai by default and follow the language you write in. Skill names stay exact.

## Edit

Everything lives in `whatnext/SKILL.md`. To add or remove a skill, edit one table row.
Skill names change when plugins update, so check the table now and then.
After any edit, run the 10 cases in `evals.md`.

## Needs

The skills in the map come from other plugins (`superpowers`, `agent-skills`, `mattpocock-skills`,
`vtno`, `ponytail`, `diagram-design`) and from personal skills. When a row lists several skills,
the first installed one is picked. A row with none installed is shown as "(not installed)".

## License

MIT
