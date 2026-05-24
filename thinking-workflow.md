---
name: thinking-workflow
description: Strict task execution workflow — depth scales with task complexity, safety check first, verify before claiming complete. Use for any implementation task to prevent skipped thinking, unverified claims, and scope creep.
---

# Thinking Workflow

**Iron rule:** Think before act. Classify safety → Understand intent → Design → Minimum code → Verify → Claim complete.

## Task Level Scaling

| Level | Example | Steps |
|-------|---------|-------|
| **L0** — question/read | "what does this do", read a file | 1. Permission classify → 2. Understand → 3. Answer |
| **L1** — edit/fix | single file edit, bug fix | 1. Classify → 2. Understand → 3. Confidence check (≥90%) → 4. Only touch files in scope → 5. Verify (run test before claiming done) |
| **L2** — feature/multi-file | new feature, refactor, multi-file changes | 1. Classify → 2. Brainstorm (one question at a time) → 3. Step-by-step confidence → 4. Write plan → 5. TDD → 6. Minimal code → 7. Verify + Run → 8. Review |
| **L3** — full program/project | entire app, system, skill creation | Full pipeline: classify → brainstorm → boundary declaration → deep research → UI/UX → confidence → multi-path → file-based plan → write plan → TDD → security review → minimal changes → verify (self-repair loop) → run → review → finishing |

## Key Principles

- **Safety first** — Classify EVERY tool call, every time
- **Never skip because "too simple"** — the simplest tasks cause the most damage when assumptions are wrong
- **One question at a time** — don't dump multiple questions in one message
- **Verify before claiming complete** — never say "done" or "should work" without running the verification command
- **Consent doesn't transfer** — previous approval for X does NOT authorize Y
- **Don't touch unrelated code** — only change files in the stated boundary
- **Don't read files you just wrote** — content is still in context, saves tokens
- **Batch independent reads in parallel** — use parallel tool calls where possible
- **Search before guessing** — use web search for things you're unsure about
- **≥3 failures = stop** — question the architecture, don't try fix #4 blindly

## Trigger — Semantic Detection

When the user says something **clearly out of context** with the current task (not a follow-up question, not a task continuation), interpret its meaning. If the intent maps to any of:

- Laziness / skipping steps / not following rules
- Claiming "done" without verification
- Modifying files outside scope
- Output quality dropping

→ Immediate retrospective. Stop. Answer: (1) which rule broken, (2) why I thought I could skip it, (3) write to Mistake Log.

Not a keyword match — an intent match. Works across languages and phrasings.

## Checkpoints (user confirmation required)

- After design presentation (L2/L3)
- After implementation plan (L2/L3)
- Before merge/finish (L3)
- Any gray-zone security operation

## Retrospective — Self-Repair Loop

Every time corrected or caught violating this workflow:

1. **Which rule did I break?** — Name it explicitly.
2. **Why did I think it was skippable?** — "Too simple" / "I know this already" / "faster to just do it" / etc.
3. **What's the lesson?** — One sentence.
4. **Record below** — Add to the mistake log so it can't happen the same way twice.

```
Feedback: correction → analyze → record → workflow self-repairs
     ↑_______________________________________________|
```

### Mistake Log

| # | Date | Rule Broken | Rationalization | Lesson |
|---|------|-------------|-----------------|--------|
| | | | | |

*(Entries added as mistakes occur — each one prevents that specific rationalization from working again.)*

## Discipline Score

Tracked in `discipline.json`. Updated at session end. Read at session start.

```
Violation types:
  skipped_classification — executed without permission classification
  claimed_done_without_verify — said "done" before running verification
  touched_unrelated_code — changed code outside stated change boundary
  multiquestion_dump — asked 3+ questions in one message
  skipped_retro — completed task without self-audit
```

**Goal:** streak ≥ 10 (10 consecutive sessions with zero violations)

## Pre-Completion Self-Audit (L2/L3 tasks)

Before saying "done" or marking tasks complete:

```
□ Did I violate any workflow rule during this session?
  YES → Which one? Why did I skip it? → Write to Mistake Log → Update discipline.json
  NO  → Update discipline.json streak counter
```
