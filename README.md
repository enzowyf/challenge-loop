# Challenge Loop

Adversarial hardening for AI agent outputs. Two modes: inline self-refutation (zero cost) and independent challenger subagent.

## What It Does

When an AI agent produces a recommendation, analysis, or judgment, Challenge Loop adds adversarial scrutiny — either through a quick inline self-check or a full independent subagent review.

**Solves two problems:**
- **Sycophancy** — AI agreeing with everything you say
- **Overconfidence** — AI believing its own output is flawless

## Modes

| Mode | What happens | Cost | Trigger |
|---|---|---|---|
| **Inline** | 4-line self-refutation block | Zero | "挑战一下" / "帮我看看有没有问题" |
| **Subagent** | Independent challenger reviews output | Higher | "审一下" / "深度挑战" / "毁灭级挑战" |

### Inline Mode (Default)

Append 4 lines to any judgment-containing output:

```
**Strongest objection:** [best argument against]
**What would invalidate this:** [falsifiable condition]
**When [alternative] is better:** [concrete alternative + condition]
**Key assumptions:** [what must hold]
```

### Subagent Mode (Escalation)

Spawn an independent challenger subagent. Three intensity levels:

| Level | Rounds | Trigger phrases |
|---|---|---|
| ⚡ Light | 1 | "审一下" / "challenge this" |
| 🔥 Standard | 3 | "深度挑战" / "strict审查" / "deep challenge" |
| 💀 Brutal | 5 | "毁灭级挑战" / "往死里挑" / "brutal challenge" |

## Platform Support

| Platform | Mechanism |
|---|---|
| **Hermes** | `delegate_task` |
| **OpenClaw** | `sessions_spawn` |
| **Claude Code** | `Agent` tool |

All platforms use the same canonical prompt template.

## Installation

### Hermes
Copy `SKILL.md` to `~/.hermes/skills/challenge-loop/SKILL.md`

### OpenClaw / Claude Code
Include `SKILL.md` content as a skill or system prompt instruction.

## File Structure

```
challenge-loop/
├── SKILL.md          # Core skill definition
└── README.md         # This file
```

## Usage Examples

**Inline (zero cost):**
> User: "I recommend PostgreSQL. 挑战一下"
> Agent: [recommendation] + inline 4-line self-refutation block

**Subagent review:**
> User: "深度挑战"
> Agent: spawns 🔥 Standard challenger → revises → spawns again → outputs hardened result

**Skip:**
> User: "直接给"
> Agent: outputs without challenge

## License

MIT-0 — free to use, modify, and redistribute. No attribution required.
