# Thinking Workflow — Agent Discipline System

A self-enforcing behavioral framework for AI coding agents. Built from months of real agent sessions and two independent security reviews. Complements [auto-mode](https://github.com/LuVAxCiN/ClaudeCode-AutoMode) as the internal discipline layer — auto-mode handles tool-call safety classification; this handles *process adherence*.

## What It Does

AI agents default to three failure modes: **skip thinking before coding**, **claim completion without verification**, and **touch code outside the stated change boundary**. This workflow prevents all three by making discipline a structured process rather than a request.

## Architecture

```
L0-L3 Task Router → Scales depth to complexity
    │
    ▼
Key Principles → 10 immutable rules (safety first, verify before claim, consent doesn't transfer)
    │
    ▼
Semantic Trigger → Intent detection instead of keyword matching. "You're being lazy" and "你跳步骤了" trigger the same retrospective — not by string match, by meaning.
    │
    ▼
Retrospective Loop → Correction → Root cause → Mistake log → Workflow self-repairs
    │
    ▼
Discipline Score → Quantified compliance, trend visible across sessions
```

## Task Level Scaling

| Level | Scope | Steps |
|-------|-------|-------|
| **L0** | Question / read a file | Safety check → Understand → Answer |
| **L1** | Edit / fix a bug | Safety → Understand → Confidence ≥90% → Only touch files in scope → Verify before claiming done |
| **L2** | Feature / multi-file changes | Safety → Brainstorm (one question at a time) → Confidence → Plan → TDD → Minimal code → Verify + Run → Review |
| **L3** | Full program / project | Full 15-step pipeline including boundary declaration, deep research, UI/UX design, multi-path evaluation, security review |

## Installation

1. Copy `thinking-workflow.md` to your agent's memory directory
2. Create `discipline.json` (template included)
3. Install a permission classifier (recommended: [auto-mode](https://github.com/LuVAxCiN/ClaudeCode-AutoMode))
4. Restart your agent

## Key Concepts

- **Iron Rule**: Think first. Safety → Understand → Design → Minimum code → Verify → Claim complete.
- **Never skip because it's "too simple"**: The simplest tasks cause the most catastrophic failures when assumptions are wrong.
- **Consent doesn't transfer**: Previous approval for X does NOT authorize Y.
- **Evidence before claims**: Never say "done" or "should work" without running the verification.
- **≥3 failures = architectural problem**: Stop. Discuss. Don't try a 4th blind fix.

## What Makes This Different

1. **Semantic Trigger Detection**: Not keyword matching. When the user says something out of context, interpret the *intent* — is this "you're being lazy"? Works across languages and phrasings.

2. **Self-Repair Loop**: Every correction feeds back into the workflow. The agent records why it failed, what rationalization it used, and updates the prevention table. The same excuse can't work twice.

3. **Quantified Discipline**: `discipline.json` tracks violations across sessions. Streak count, violation types, trend visible. Both the user and the agent can audit.

4. **Depth-Scaled**: Not a one-size-fits-all checklist. L0 tasks get 3 steps. L3 gets 15. The overhead matches the complexity.

## Requirements

- An AI coding agent (Claude Code, Cursor, Codex, Copilot, etc.)
- A permission classifier (recommended: [auto-mode](https://github.com/LuVAxCiN/ClaudeCode-AutoMode))

## License

MIT
