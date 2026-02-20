# Skills Framework

**Skills Framework — Versioned Capability Contracts for Autonomous AI**

---

The problem with autonomous agents isn't getting them to do things. It's getting them to do the same things the same way, every time, across hundreds of sessions.

Skills are the solution. Each skill is a versioned capability module with a standardized contract: name, description, exact trigger phrases, step-by-step workflow, authority tier, error handling, and a handoff statement that declares what was produced. 8 skills in production. The contracts are the reason they run consistently — not because the agent remembers, but because the contract is read before execution, every time.

**The trigger system matters more than it sounds.** A skill that fires on too broad a trigger creates false matches. A skill that fires on too narrow a trigger gets missed. The trigger set for each skill is a precision instrument: "start session, new session" triggers startup — not "session" alone, which would match dozens of unrelated mentions. Each trigger phrase is unique across all skills. The set was tested against real session transcripts to verify it doesn't fire when it shouldn't.

**Skills at v2.x because v1.x had gaps production exposed.** skill-creator-skill is at v2.3 because three rounds of real use found three rounds of real problems: ambiguous trigger rules, missing token budget enforcement, structural requirements that weren't validated until a skill failed in the field. Each version bump is traceable to a specific production failure. The version number is the evidence count. Every skill carries an anti-patterns section — documented failure modes, not hypothetical ones.

The meta-layer: skill-creator-skill builds new capabilities to the standard. 9-step creation workflow. Trigger uniqueness validation. Token budget enforcement. Structural checklist before a skill goes into production. Skills that build skills following the same contract as the skills they build.

**Why it matters:** Skill contracts for autonomous agents are the same idea as standard operating procedures for distributed teams — except here, if the procedure isn't read before execution, the agent operates from memory, and memory resets overnight. Versioned contracts with production-validated triggers are what make consistent autonomous execution possible at scale.
