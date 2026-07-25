# claude-skills

My personal library of Claude skills, kept under version control.

## What this is

Skills are reusable instructions that Claude loads automatically when they're
relevant — so I don't have to re-explain the same preferences in every chat.

This repo is the single source of truth for mine. Every change is recorded,
so I can see what I changed, when, and why, and roll back anything that makes
Claude's output worse.

## How it's wired up

Claude syncs directly from this repo as a plugin marketplace. Edit here,
release, and the skills update in claude.ai. No copying files around.

## Layout

| Path | What it is |
|---|---|
| `.claude-plugin/marketplace.json` | Catalogue. Marks this repo as a marketplace. |
| `plugins/core-skills/.claude-plugin/plugin.json` | Bundle name and version number. |
| `plugins/core-skills/skills/<name>/SKILL.md` | The skills themselves. |

## Skills

| Skill | What it does |
|---|---|
| `general-research` | Search first, cite sources, flag uncertainty, stay concise. |
| `ai-rundown` | Headline-only briefing on recent AI news relevant to using Claude. |

## Releasing a change

1. Edit the `SKILL.md`, commit with a message describing the change.
2. Bump `version` in `plugin.json`.
3. In Claude: Plugins → marketplace `...` menu → Check for updates.
4. Then open the plugin and click Update.

Steps 3 and 4 are separate. Skipping the version bump means Claude sees no
change and does nothing.

## Adding a skill

Create `plugins/core-skills/skills/<new-name>/SKILL.md`, with frontmatter:

    ---
    name: new-name
    description: What it does, and the situations that should trigger it.
    ---

The folder name and the `name` field must match. The file must be called
`SKILL.md` in capitals. The `description` is what Claude reads to decide
whether to use the skill, so it needs to name the situation, not just the topic.
