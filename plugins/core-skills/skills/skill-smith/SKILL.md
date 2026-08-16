---
name: skill-smith
description: >
  How to author, edit, and release skills in my claude-skills repo. Use whenever
  I ask to add a new skill, write a skill, change or tighten an existing
  SKILL.md, work out why a skill isn't triggering, split or merge skills, or
  publish and release skill changes to claude.ai — including casual phrasings
  like "make a skill for this", "add that to my skills", "why didn't it use the
  rundown skill", or "push the skill update". Also use when I describe a
  preference I clearly want to stop repeating. NOT for general coding in other
  repos, and NOT for using a skill — only for building them.
---

# Skill Smith

Rules for working on the skills library itself. The repo is the source of truth;
claude.ai syncs from it as a plugin marketplace.

## Layout

| Path | What it is |
|---|---|
| `.claude-plugin/marketplace.json` | Marks the repo as a marketplace. Rarely changes. |
| `plugins/core-skills/.claude-plugin/plugin.json` | Bundle name and `version`. Changes on every release. |
| `plugins/core-skills/skills/<name>/SKILL.md` | One skill. |

Hard constraints, all three of which silently break the skill if wrong:

- The folder name and the frontmatter `name` must be identical.
- The file must be `SKILL.md`, capitals exactly.
- The frontmatter must be valid YAML between `---` fences, with `name` and
  `description` present.

## Writing the description

This is the only part Claude reads when deciding whether to load the skill, so
it does the entire job of triggering. The body is never consulted until after
the description has already won.

- Name the situations, not the topic. "About sustainability" triggers on
  nothing. "Whenever I ask what's changed in Part L" triggers reliably.
- Include the phrasings I actually use, casual ones included. List several.
  This is the single highest-leverage thing in the file.
- State what the skill is NOT for, and name the sibling skill that owns those
  cases. Every skill in this library disclaims its neighbours; keep that.
- Write it in my voice — "Use whenever I ask…" — matching the existing skills.
- Use a YAML block scalar (`description: >`) once it runs past a line or two.

## Writing the body

- Imperative rules addressed to Claude. Not documentation, not explanation.
- Lead with the constraint that matters most. No preamble, no restating the
  frontmatter.
- Give output formats as fenced skeletons rather than describing them in prose.
  Every rundown skill here does this and it is why they hold their shape.
- Negative rules earn their place: "never pad a quiet period", "no closing
  summary". They stop the failure modes that generic instructions won't.
- Keep it under roughly 150 lines. If it's longer, the skill is doing two jobs,
  or the reference material belongs in a sibling file in the same folder that
  the SKILL.md points to by name.
- Assume expertise. Never write primers for things I do for a living.

## Overlap discipline

`general-research` is the accuracy base. Anything that answers questions from
the world inherits its rules and overrides only the output format — say so
explicitly, the way `ai-rundown` and `sustainability-rundown` both do.

When a new skill's territory touches an existing one, edit both descriptions in
the same commit so the boundary is stated from each side. A boundary described
only once is a skill that fires at the wrong time.

## Before committing

Check, and report the result rather than assuming:

- Folder name equals frontmatter `name`.
- Filename is `SKILL.md`.
- Frontmatter parses and has both required keys.
- The description names at least three trigger phrasings and one exclusion.
- No sibling skill now overlaps without a stated boundary.

`ls plugins/core-skills/skills/` and reading the neighbouring descriptions is
enough. There is no build step and nothing to lint.

## Releasing

In this order, all in one commit unless I say otherwise:

1. Write or edit the `SKILL.md`.
2. Update the Skills table in `README.md` — new skills, renamed skills, and
   changed purpose all belong there. It goes stale otherwise.
3. Bump `version` in `plugin.json`. Patch for wording and rule changes, minor
   for a new skill or a removed one.
4. Commit with a message naming the skill and what changed about its behaviour,
   not just "update skill".
5. Push.

Then tell me to do the two steps in claude.ai, because I cannot do them from
here and skipping either means nothing happens:

- Plugins → marketplace `...` menu → Check for updates
- Open the plugin → Update

Without the version bump in step 3, Claude sees no change and neither step does
anything. Never push a skill edit without it.

## When a skill isn't firing

Assume the description before anything else. In order of likelihood:

1. The description names a topic instead of a situation.
2. My actual phrasing isn't in it — add the exact words I used.
3. A sibling skill is winning; the boundary needs stating in both.
4. The version wasn't bumped, or the two-step update wasn't run, so claude.ai
   is still serving the old file.

Fix the description first. Rewriting the body will not change what triggers.

## What not to turn into a skill

One-off instructions, anything true only for a single project, and preferences
better expressed as a single sentence in a chat. A skill earns its place by
being something I'd otherwise re-explain repeatedly. If it isn't that, say so
rather than adding it.
