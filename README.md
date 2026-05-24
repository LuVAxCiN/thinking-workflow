# Thinking Workflow — Agent Discipline Memory

A self-enforcing behavioral framework for AI coding agents. Prevents the three most common agent failure modes: **skipping thinking**, **claiming completion without verification**, and **touching code outside the stated boundary.**

**Important:** This is a **memory file**, not a skill. Skills trigger on keywords. Memory loads at session start — always active, no trigger needed. Behavioral rules belong in memory.

## Quick Install

```bash
# 1. Clone
git clone https://github.com/LuVAxCiN/thinking-workflow.git

# 2. Copy to memory directory
cp thinking-workflow/memory/thinking-workflow.md ~/.claude/projects/<your-project>/memory/
cp thinking-workflow/discipline.json ~/.claude/

# 3. Register in MEMORY.md
echo "- [Thinking workflow](thinking-workflow.md) — L0-L3 scaled task pipeline" >> ~/.claude/projects/<your-project>/memory/MEMORY.md

# 4. Restart Claude Code
```

**Claude Code Plugin Market (alternative):**
```
/plugin marketplace add LuVAxCiN/thinking-workflow
```

Then manually copy the files to your memory directory using the steps above.

## File Structure

```
thinking-workflow/
├── README.md                          ← You're reading this
├── memory/
│   └── thinking-workflow.md           ← The workflow itself (copy to memory/)
└── discipline.json                    ← Score tracker (copy to ~/.claude/)
```

## How It Works

```
Session Start
    │
    ▼
┌──────────────────────────────────────┐
│ Memory auto-loads thinking-workflow  │
│ → Classify EVERY tool call           │
│ → Never skip because "too simple"    │
│ → Verify before saying "done"        │
└──────────────────────────────────────┘
    │
    ▼
Task arrives → L0-L3 Router → Depth scales to complexity
    │
    ├── L0: "What does this do?" → 3 steps
    ├── L1: Bug fix → 5 steps
    ├── L2: Feature → 8 steps
    └── L3: Full project → 15 steps
    │
    ▼
User corrects agent → Intent-based trigger
    │
    ▼
Retrospective loop: analyze → record → prevent
    │
    ▼
discipline.json: quantified compliance across sessions
```

## All Features

### L0-L3 Depth-Scaled Pipeline

| Level | Scope | Steps | Overhead |
|-------|-------|-------|----------|
| **L0** | Question / read | 3 | ~0 tokens |
| **L1** | Edit / fix | 5 | ~50 tokens |
| **L2** | Feature / multi-file | 8 | ~200 tokens |
| **L3** | Full project | 15 | ~500 tokens |

The pipeline scales with the task — no one-size-fits-all checklist. Simple tasks don't get buried in process. Complex tasks don't get cowboy-coded.

### 10 Immutable Principles

1. **Safety first** — classify every tool call
2. **Never skip because "too simple"** — simple things cause catastrophic failures
3. **One question at a time** — don't dump multiple questions
4. **Verify before claiming complete** — evidence before assertions
5. **Consent doesn't transfer** — previous approval ≠ current approval
6. **Don't touch unrelated code** — only files in stated boundary
7. **Don't read files just written** — context still has them
8. **Batch independent reads** — parallel tool calls
9. **Search before guessing** — web search for unknowns
10. **≥3 failures = stop** — architectural problem, not a fixing problem

### Semantic Trigger Detection

Not keyword matching. When the user says something out of context — across languages, across phrasings — the agent interprets *intent*:

- "You're being lazy" / "你又偷懒了" / "跳步骤了吧" / "skipped again"
- "Did you actually verify that?" / "验证了吗"
- "Why did you touch that file?" / "这文件你也改了"

All map to the same response: **immediate retrospective → root cause → mistak log → prevent recurrence.**

### Retrospective Self-Repair Loop

```
User correction → Agent stops → Identifies broken rule
    → Names the rationalization ("I thought it was too simple")
    → Records lesson in Mistake Log
    → Same excuse cannot work twice
    ↑_____________________________________________|
```

### Quantified Discipline Tracking

`discipline.json` tracks violations across sessions:

```json
{
  "sessions": 24,
  "violations": {
    "skipped_classification": 3,
    "claimed_done_without_verify": 5,
    "touched_unrelated_code": 2
  },
  "streak": 7
}
```

Gives both the user and the agent visibility into whether discipline is improving or degrading.

### Checkpoints

Three explicit user confirmation gates in L2/L3:
- After design presentation
- After implementation plan
- Before merge / publish

## auto-mode alone vs auto-mode + thinking-workflow

| Scenario | auto-mode only | auto-mode + thinking-workflow |
|----------|---------------|-------------------------------|
| `rm -rf /` | Blocked by hook | Blocked by hook |
| `curl \| sh` | Blocked by hook | Blocked by hook |
| Agent writes file outside project | Classified (skill layer) | Classified + principle #6 forbids it |
| Agent says "done" without testing | Nothing stops it | Pre-completion audit catches it |
| Agent asks 5 questions at once | Nothing stops it | Principle #3 flagges it |
| Agent changes variable name "while there" | Nothing stops it | Principle #6 catches scope creep |
| Agent claims confidence without checking | Nothing stops it | Confidence gate (≥90%) enforced |
| Agent uses the same bad excuse twice | Nothing stops it | Mistake Log blocks repeats |
| User says "你又偷懒了" | No special behavior | Immediate retrospective |
| Three consecutive denials | Circuit breaker trips | Circuit breaker trips |
| Cross-session trend | Not tracked | discipline.json shows streak |

**Bottom line:** auto-mode handles *what you can and can't do.* thinking-workflow handles *how you do it.* One without the other leaves a gap.

## Requirements

- Claude Code or any AI coding agent with memory support
- Recommended: [auto-mode](https://github.com/LuVAxCiN/ClaudeCode-AutoMode) for permission classification

## License

MIT
