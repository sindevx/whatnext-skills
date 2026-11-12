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
| `/whatnext all` | One line per stage (start, plan, build, debug, review, ship, notes) with skill names |

Every row has an example prompt you can copy. A "Common chains" table shows the usual next skill. Replies are in Thai by default and follow the language you write in. Skill names stay exact.

## Edit

- `whatnext/SKILL.md`: rules, the "State" table for plain `/whatnext`, and chains. Loaded every time, so keep it small.
- `whatnext/map.md`: the full skill map with example prompts. Read only for `/whatnext all` and `/whatnext <focus>`.
  To add or remove a skill, edit one row here, and give it an example prompt.

Token rule: the `description` line is loaded in every session, and `SKILL.md` on every `/whatnext`.
Keep both short. Put long lists in `map.md`. Keep table text in English (Thai text costs more tokens);
the reply is still in the user's language.

Skill names change when plugins update, so check the tables now and then.
After any edit, run the 10 cases in `evals.md`.

## Needs

The skills in the map come from other plugins (`superpowers`, `agent-skills`, `mattpocock-skills`,
`vtno`, `ponytail`, `diagram-design`) and from personal skills. When a row lists several skills,
the first installed one is picked. A row with none installed is shown as "(not installed)".

## License

MIT
