# Skills

## Install

Install with the [skills CLI](https://github.com/vercel-labs/skills), which works with Claude Code, Cursor, Codex and other agents:

```
npx skills add ya-nsh/skills
```

To install a single skill:

```
npx skills add ya-nsh/skills --skill unslop-ui
```

Or, in Claude Code, add this repo as a plugin marketplace:

```
/plugin marketplace add ya-nsh/skills
```

Then install a skill with the command in its row of the table below.

To install by hand instead, copy a skill's folder into `~/.claude/skills/`.

## Skills

| Skill | Description | Install |
| --- | --- | --- |
| [unslop-ui](skills/unslop-ui/SKILL.md) | Make a UI stop looking AI-generated. | `/plugin install unslop-ui@ya-nsh-skills` |

## Adding a skill

1. Create `skills/<name>/SKILL.md`.
2. Add an entry for it to `plugins` in [.claude-plugin/marketplace.json](.claude-plugin/marketplace.json).
3. Add a row to the table above.

## License

[MIT](LICENSE)
