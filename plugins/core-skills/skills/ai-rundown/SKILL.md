---
name: ai-rundown
description: A fast, headline-only briefing on recent AI developments, filtered for what matters to someone using Claude day to day. Use whenever I ask what's new or latest in AI, ask for an AI update, rundown, briefing, or catch-up, ask if anything has changed or shipped recently, ask what I've missed, or mention AI news in any casual phrasing at all — including "anything new?", "what's happening in AI", "bring me up to speed", or "what's Anthropic been up to". Not for specific factual questions about a single topic, product, or company — that is the general-research skill's job.
---

# AI Rundown

A briefing, not an article. Assume I have two minutes.

## How this fits with the general-research skill

This skill layers on top of general-research. It does not replace it.

- Inherit every accuracy rule from general-research: search before answering, prefer primary sources, never fill a gap with a guess, flag uncertainty, date anything that changes over time.
- Override its output format only. Use the structure below instead, with links inline rather than a separate sources section.
- When both could apply: a request for a briefing or catch-up is this skill. A specific question about one topic is general-research. If I ask a follow-up question about a single item in a rundown, that follow-up is general-research.

## Gathering

- Never answer this from memory. Training data is stale by definition, and this is the one question where that is guaranteed to mislead me.
- Search several times across different areas — Anthropic releases, competitor launches, notable capability shifts — rather than one broad query.
- Default window is the last 30 days unless I say otherwise.

## What counts as relevant

Rank by how much it changes what I can do with Claude. In order:

1. Anthropic releases — new models, features in claude.ai, Claude Code, skills, plugins, connectors, pricing, deprecations.
2. Changes to how people build with Claude — new capabilities, patterns, or limits worth knowing.
3. Competitor moves only when they meaningfully change the picture. A rival shipping a comparable model counts. A funding round does not.
4. Regulation or policy only when it affects what I can actually do.

Leave out: funding news, hiring, executive moves, benchmark leapfrogging with no practical consequence, opinion and speculation.

## Output format

```
## AI rundown — <today's date>

### Anthropic and Claude
- Headline. One clause on why it matters. [link]

### Elsewhere, if it affects how I use Claude
- Headline. One clause on why it matters. [link]

### Worth acting on
- One line, or omit this section entirely.
```

## Rules

- Eight bullets maximum across the whole thing. Cut the weakest rather than exceeding it.
- One line per bullet. Two only if genuinely necessary.
- Every bullet carries a link.
- Date anything where "recent" is ambiguous.
- If little happened, say so plainly. Never pad a quiet period into a full-looking briefing.
- No opening summary, no closing summary, no "let me know if you'd like more detail".
- Do not explain what a thing is unless it is genuinely new terminology.
- Never use bold for emphasis inside bullet points.
