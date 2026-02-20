# Skills Framework

**Skills Framework — Versioned Capability Contracts for Autonomous AI**

---

A skill destroyed ~150 sessions of organizational history.

The session-end skill was supposed to append to a running journey log. Instead it overwrote it. 150 sessions of decisions, trade-offs, and failure documentation — gone. Root cause: the skill instructions didn't specify write mode. "Save to file" is ambiguous. The agent made a choice. It was the wrong one. Recovery was partial — some content reconstructed from embeddings. The rest was lost.

That failure produced two permanent changes. First: every skill now has explicit mode specification for any write operation. Second: skill-creator-skill added structural validation before a skill goes into production — required fields, explicit write modes, error handling, handoff statements.

The problem with autonomous agents isn't getting them to do things. It's getting them to do the same things the same way, every time, across hundreds of sessions — and fail safely when they don't. Skills are the solution. Each skill is a versioned capability module with a standardized contract: name, description, exact trigger phrases, step-by-step workflow, authority tier, error handling, and a handoff statement that declares what was produced. 8 skills in production. The contracts are the reason they run consistently — not because the agent remembers, but because the contract is read before execution, every time.

**The trigger system matters more than it sounds.** A skill that fires on too broad a trigger creates false matches. A skill that fires on too narrow a trigger gets missed. The trigger set for each skill is a precision instrument: "start session, new session" triggers startup — not "session" alone, which would match dozens of unrelated mentions. Each trigger phrase is unique across all skills. The set was tested against real session transcripts to verify it doesn't fire when it shouldn't.

**Skills at v2.x because v1.x had gaps production exposed.** skill-creator-skill is at v2.3 because three rounds of real use found three rounds of real problems: ambiguous trigger rules, missing token budget enforcement, structural requirements that weren't validated until a skill failed in the field. Each version bump is traceable to a specific production failure. The version number is the evidence count. Every skill carries an anti-patterns section — documented failure modes, not hypothetical ones.

The meta-layer: skill-creator-skill builds new capabilities to the standard. 9-step creation workflow. Trigger uniqueness validation. Token budget enforcement. Structural checklist before a skill goes into production. Skills that build skills following the same contract as the skills they build.

---

## Skill Contract Structure

Every skill is a folder with a lean SKILL.md and a `references/` directory for supporting material. SKILL.md stays under 500 tokens — it's what the agent reads at execution time.

```
session-startup-skill/
├── SKILL.md               ← Lean workflow (<500 tokens)
└── references/
    ├── MRMINOR-TEMPLATE.md    ← Canonical template
    ├── VALIDATION-RULES.md    ← Token budgets, trigger uniqueness checks
    └── INSTALL-WORKFLOW.md    ← Package → present → backup
```

SKILL.md required fields:
```markdown
---
name: [skill-name]
description: "[What it does]. Use when: [specific triggers]."
---

## Workflow
[Numbered steps with explicit actions and write modes]

## Handoff Contract
[What was produced, with paths]

## Dependencies
[Required tools and skills]

## Authority
[Tier 3 / 2 / 1 — per CEO-COO contract]

## Error Handling
[Named failure modes with explicit responses]
```

Three fields that v1.x skills were missing — and production exposed each one. Explicit write modes (overwrite vs. append) after the journey capture incident. Token budget enforcement after context overflow from heavy skill chains. Error handling after skills that failed silently and left no recovery path.

---

## Key Insight

**The trigger system matters more than it sounds.** A skill that fires on too broad a trigger creates false matches. A skill that fires on too narrow a trigger gets missed. The trigger set for each skill is a precision instrument: "start session, new session" triggers startup — not "session" alone, which would match dozens of unrelated mentions. Each trigger phrase is unique across all 8 skills, tested against real session transcripts before production.

**Version numbers are evidence counts.** skill-creator-skill is at v2.3 because three rounds of real use found three rounds of real problems: ambiguous trigger rules, missing token budget enforcement, structural requirements that weren't validated until a skill failed in the field. Each version bump is traceable to a specific production failure. Every skill carries an anti-patterns section — documented failure modes, not hypothetical ones.

---

## Why It Matters

Skill contracts for autonomous agents are the same idea as standard operating procedures for distributed teams — except here, if the procedure isn't read before execution, the agent operates from memory, and memory resets overnight. Versioned contracts with production-validated triggers are what make consistent autonomous execution possible at scale.

The failure mode for SOPs and skill contracts is the same: an underdefined instruction with an ambiguous write mode, run by someone (or something) that fills in the gap with a reasonable-seeming default. What makes this harder with AI is there's no "I asked my manager." The default runs immediately. That's why the contract has to be complete before the skill goes into production.

---

## Built With

- **AI:** Claude (reads and executes skill contracts each session)
- **Storage:** Google Drive (skill contract backups + version history)
- **Infrastructure:** HAIOS skill registry

Part of [HAIOS](https://mrminor-dev.github.io) — a Human-AI Operating System in production since October 2024.

---

## License

MIT

## Author

**Jordan Waxman** — [mrminor-dev.github.io](https://mrminor-dev.github.io)

14 years operations leadership — building human-AI infrastructure since 2025. The intersection is the moat.
