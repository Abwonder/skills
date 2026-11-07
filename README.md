# skills

Personal agent skills for OpenCode. Each folder is one skill. Copy a folder into `~/.config/opencode/skills/` and the agent picks it up on the next session.

## Install

```bash
git clone https://github.com/Abwonder/skills.git /tmp/abwonder-skills
cp -r /tmp/abwonder-skills/*/ ~/.config/opencode/skills/
```

Or copy a single skill:

```bash
cp -r /tmp/abwonder-skills/linkedin-writing ~/.config/opencode/skills/
```

## Skills

| Skill | Triggers on | What it does |
|---|---|---|
| [`linkedin-writing`](linkedin-writing/) | "we are writing for LinkedIn", "write a LinkedIn post", "LinkedIn carousel", "write Day N", "series post" | Writes posts, series, carousels, comments and DMs in Abioye's voice. Enforces the no-AI writing rules. |

## Structure

```
<skill-name>/
  SKILL.md          required, holds the workflow and hard rules
  references/       optional, loaded on demand
    voice-rules.md
    post-patterns.md
    series-template.md
```

`SKILL.md` frontmatter needs `name` and `description`. The description is the trigger, so it names the phrases a person would actually type. Body stays under 500 lines. Anything long goes in `references/`.

## Adding a skill

1. Make a folder named in kebab-case.
2. Write `SKILL.md` with a description that lists the trigger phrases and at least one "Do NOT use for" exclusion.
3. Put supporting material in `references/`.
4. Add a row to the table above.
5. Commit and push.

## Licence

MIT.
