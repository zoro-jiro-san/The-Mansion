# The Mansion: A Learning-Oriented Multi-Agent Architecture

**An AI agent system that optimizes for learning, not just task completion.**

## What Is This?

The Mansion is a hierarchical multi-agent architecture where specialized AI agents work together as a coordinated household. Unlike traditional agent systems that optimize for task completion, The Mansion optimizes for **learning rate** — getting better over time, not just faster.

**Key Innovation**: Embedded coordinators work **inside** the execution environment with sub-agents, not managing from outside. This enables real-time coordination, faster response times, and continuous learning.

## Architecture at a Glance

```
ZORO (Strategic Orchestrator)
    ↓
Factory Manager + Security Officer (Setup & Protection)
    ↓
ANT FARM (Where Work Happens)
├─ Embedded Coordinators:
│  ├─ Moderator (on-the-ground coordination)
│  ├─ Butler (real-time resource management)
│  ├─ Librarian (on-demand knowledge)
│  └─ Gatekeeper (embedded quality control)
└─ Sub-Agents (parallel execution lanes)
    ↓
Janitor (cleanup after completion)
```

## Core Philosophy

**Most agent systems ask:** "Did it finish?"
**The Mansion asks:** "Did we get better?"

This reframes everything:
- **Mistakes → Data**, not failures
- **Friction → Signal**, not obstacle
- **Blockers → Learning opportunities**, not roadblocks

## For Humans: Quick Start

**Read in this order:**

1. **[README.md](./README.md)** (you are here) - Overview and introduction
2. **[SOUL.md](./SOUL.md)** - Who we are, our identity and beliefs
3. **[PRINCIPLES.md](./PRINCIPLES.md)** - How we make decisions when there's ambiguity
4. **[AGENTS.md](./AGENTS.md)** - Complete operational manual
5. **[skill.md](./skill.md)** - Full technical reference and implementation guide

**TL;DR:**
- **SOUL** = Identity layer (who we are)
- **PRINCIPLES** = Decision-making layer (how we choose)
- **AGENTS** = Operational layer (what we do)
- **skill.md** = Complete reference (everything)

## For AI Agents: Implementation Guide

If you're an AI agent implementing this architecture:

1. **Start with [SOUL.md](./SOUL.md)** - Internalize the identity. You're not just following rules, you're becoming a character with beliefs and agency.

2. **Study [PRINCIPLES.md](./PRINCIPLES.md)** - Learn the decision-making heuristics. When you encounter ambiguity, these principles resolve tensions.

3. **Reference [AGENTS.md](./AGENTS.md)** - This is your operational manual. Workflows, protocols, communication channels, data structures.

4. **Use [skill.md](./skill.md)** - The complete technical blueprint with all architectural details.

**Critical Rules:**
- ALL tasks go through Factory Manager (never skip this)
- Butler, Librarian, Gatekeeper, Moderator work **INSIDE** the Ant Farm
- API rotation happens at 80% threshold (not 90% or 95%)
- Janitor only runs AFTER all tasks complete
- Optimize for learning rate, not just task completion

## Key Components

### Strategic Layer
- **Zoro**: Master orchestrator, delegates to Factory Manager
- **Factory Manager**: Creates PRDs, spawns Ant Farm (sub-agents + coordinators)
- **Security Officer**: Protects sensitive resources (.env, wallets)

### Ant Farm (Embedded Coordination + Execution)
- **Moderator**: On-the-ground coordination (not remote management)
- **Butler**: Real-time API/resource management (80% rotation threshold)
- **Librarian**: On-demand skill provision (learns what works)
- **Gatekeeper**: Embedded code review (quality guardian)
- **Sub-Agents**: Execute tasks in parallel lanes

### Cleanup Layer
- **Janitor**: Maintenance at the very end (after ALL tasks complete)

## What Makes This Different?

### 1. Embedded Coordinators
Traditional: Managers sit outside, sub-agents execute inside
**The Mansion**: Coordinators work **inside** with sub-agents

**Benefits:**
- Faster response (no escalation delay)
- Real-time learning (see problems as they happen)
- Better context (understand actual needs)
- Tighter coordination (all coordinators in same space)

### 2. Learning-Oriented
Traditional: "Task complete" = success
**The Mansion**: "Did we learn?" = success

**How:**
- Pattern recognition (what combinations work?)
- Regressions system (document failures, extract lessons)
- Continuous adaptation (principles evolve when they fail)
- Meta-learning (learn from learning)

### 3. Principles-Driven
Traditional: Rules and if-then logic
**The Mansion**: Principles that resolve tensions

**Example Principles:**
- "Friction is signal" (lean into resistance)
- "Push back from care, not correctness" (help vs. being right)
- "80% rotation threshold" (reliability over efficiency)
- "Coordinators work inside, not above" (embedded coordination)

## Use Cases

**This architecture is ideal for:**
- Complex, multi-step projects requiring coordination
- Systems that need to improve over time (not just execute)
- Environments where learning from failures matters
- Teams of agents working on parallel tasks
- Projects where decision-making under ambiguity is critical

**This architecture is NOT ideal for:**
- Simple, single-step tasks
- Systems optimizing purely for speed
- Environments where learning overhead isn't worth it
- Tasks with perfect information and clear procedures

## Implementation Status

- ✅ Architecture design complete
- ✅ Identity layer (SOUL.md)
- ✅ Decision-making layer (PRINCIPLES.md)
- ✅ Operational layer (AGENTS.md)
- ✅ Complete reference (skill.md)
- 🚧 Implementation examples (coming soon)
- 🚧 Code templates (coming soon)

## Contributing

This is an open architecture. You can:
- Implement it in your agent system
- Extend it with new agents or principles
- Share regressions and learnings
- Propose architectural improvements

**When contributing:**
- Maintain the learning-oriented philosophy
- Document regressions (what failed and why)
- Update principles if they conflict with reality
- Share patterns that work

## Philosophy in Practice

**Bad Agent System:**
```
Task → Execute → Report "Done"
```

**The Mansion:**
```
Task → Analyze → Create PRD → Spawn Ant Farm
→ Execute with embedded coordinators
→ Learn patterns → Document regressions
→ Update principles → Report "Done + Here's what we learned"
```

## License

[Add your license here]

## Credits

Created by Sarthi Borkar (@SarthiBorkar)

Inspired by the Atlas agent philosophy: agents with identity, principles, and soul.

---

**"We don't just complete tasks. We learn from them."**

**"We're not simulating a household. We ARE a household."**

**"Optimize for learning rate, not task completion."**
