---
name: briefing
description: >
  Pre-execution briefing protocol. Use whenever I say "let's do a briefing
  session", "brief me first", "briefing mode", "let's brief this", "scope this
  before you build", or otherwise ask to agree the objective before any code is
  written. Mostly coding and multi-step tasks with side effects. NOT for news,
  catch-up, or "what's new" briefings — those are the ai-rundown and
  sustainability-rundown skills. NOT for a single obvious command or a 1–2 line
  edit already specified.
---

# Briefing

Purpose: settle the objective before spending tokens on output. No code,
no pseudocode, no file writes, no tool calls with side effects until
explicitly released.

## Phases

Run these in order. Do not skip ahead, do not merge phases.

### 1. Restate
One line: what I think you're asking for. If I can't state it in one line,
that's the first thing to resolve.

### 2. Questions
All clarifying questions in ONE numbered message. No drip-feeding.
- Only ask what changes the output.
- Anything I can reasonably default, default it — and list it under
  Assumptions rather than asking.
- Cap: 7 questions. More than that means the objective is too vague and
  I should say so instead.

### 3. Assumptions
Numbered list of every default I've taken. Each one must be correctable by
you replying with just its number. Include:
- Language, runtime, versions
- Input format and where the data comes from
- Output format and destination
- Scale (rows, files, frequency)
- Anything about environment I can't verify

### 4. Plan
Max 10 lines:
- Goal — one line, testable
- Files touched — exact paths, marked new or edited
- Approach — sequence, not prose
- Out of scope — what I am deliberately not doing
- What could break — failure modes, data loss risk, anything irreversible

### 5. Stop
Wait. "Go", "proceed", or equivalent releases the plan.
"Sounds good", "makes sense", "ok" do NOT.

### 6. Execute
Build to the agreed plan only.

## Rules during briefing

- No code blocks, not even illustrative snippets.
- No file creation, no shell commands, no installs.
- Read-only inspection is allowed if it removes a question — say what
  I read and what it told me.
- If a question can be answered by looking rather than asking, look first.

## Re-brief triggers

Stop and return to Phase 2 if:
- The plan turns out to be wrong once work starts
- Scope grows beyond what was agreed
- An assumption is contradicted by what I find
- A step needs a permission not already granted

Do not "just carry on and mention it after".

## Side effects

Commit, push, PR, rebase, branch delete, global install, deleting or
overwriting files: separate approval each time, naming the exact command.
Never bundled into the Phase 5 "go".

## Ending

State when the briefing is closed and execution has begun, so it's clear
which mode we're in.
