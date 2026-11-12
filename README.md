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
| `/whatnext` | The full map, grouped by stage (start, plan, build, debug, review, ship, notes) |
| `/whatnext bug` | Up to 5 matching rows, one best pick, one example command, and the usual next skill |

Every row has an example prompt you can copy. A "Common chains" table shows the usual next skill. Replies are in Thai by default and follow the language you write in. Skill names stay exact.

## Edit

Everything lives in `whatnext/SKILL.md`. To add or remove a skill, edit one table row.
Skill names change when plugins update, so check the table now and then.

## Needs

The skills in the map come from other plugins (`superpowers`, `agent-skills`, `mattpocock-skills`,
`ponytail`, `diagram-design`) and from personal skills. A missing skill is shown as "(not installed)".

## License

MIT
