# Decision Tree: When to Escalate & Who to Contact

## Quick Reference Matrix

```
┌─────────────────────────┬──────────────────┬─────────────────────┐
│ SITUATION               │ CONTACT          │ ESCALATE TO         │
├─────────────────────────┼──────────────────┼─────────────────────┤
│ Need skills             │ Librarian        │ Moderator if stuck  │
│ Need API key            │ Butler           │ Security Officer    │
│ Need new agent          │ Factory Manager  │ Zoro if critical    │
│ Hit a blocker           │ Moderator        │ (Moderator routes)  │
│ Need code review        │ Gatekeeper       │ Moderator if stuck  │
│ Need .env access        │ Security Officer │ Zoro if denied      │
│ Need transaction done   │ Security Officer │ Zoro if high-value  │
│ Task complete           │ Moderator        │ Zoro (completion)   │
│ Agent failed            │ Moderator        │ Factory Manager     │
│ Security incident       │ Security Officer │ Zoro immediately    │
│ API exhausted           │ Butler           │ Moderator if stuck  │
│ Context overflow        │ Butler           │ Moderator if stuck  │
└─────────────────────────┴──────────────────┴─────────────────────┘
```

---

## Decision Flow: "I'm Blocked — What Do I Do?"

```
START: You're blocked on something

├── Is it a SKILL problem?
│   ├── YES → Contact Librarian
│   │   ├── Librarian resolves → Continue
│   │   └── Librarian can't resolve → Moderator escalates
│   └── NO ↓

├── Is it a RESOURCE problem (API, rate limit, context)?
│   ├── YES → Contact Butler
│   │   ├── Butler rotates/allocates → Continue
│   │   └── All APIs exhausted → Moderator → Zoro
│   └── NO ↓

├── Is it a CODE problem (review needed, merge conflict)?
│   ├── YES → Contact Gatekeeper
│   │   ├── Gatekeeper reviews → Continue
│   │   └── Architectural issue → Moderator → Factory Manager
│   └── NO ↓

├── Is it a SECURITY problem (.env, keys, transaction)?
│   ├── YES → Contact Security Officer
│   │   ├── Officer resolves → Continue
│   │   └── Policy violation → Zoro
│   └── NO ↓

├── Do you need ANOTHER AGENT?
│   ├── YES → Contact Moderator → Factory Manager spawns
│   └── NO ↓

└── Unknown blocker?
    └── Contact Moderator with full description
        └── Moderator classifies and routes
```

---

## Decision Flow: "Who Makes This Decision?"

```
DECISION TYPE                    AUTHORITY
─────────────────────────────    ──────────────────
Strategic direction              Zoro
Task decomposition               Factory Manager
Agent creation/spawning          Factory Manager
API key assignment               Butler
API rotation                     Butler
Skill selection                  Librarian
Code approval                   Gatekeeper
Git push authorization           Gatekeeper
Transaction approval             Security Officer
.env modifications               Security Officer
Blocker routing                  Moderator
Cleanup authorization            Moderator (after ALL tasks done)
Critical escalation              Zoro (final authority)
```

---

## Escalation Levels

### Level 1: Self-Resolve (Sub-Agent)
**Try first**: Can you solve this with your assigned skills and resources?
- Duration: Up to 2 minutes
- If resolved → Continue
- If not → Escalate to Level 2

### Level 2: Moderator Routes
**Moderator classifies** the blocker and routes to the right specialist.
- Duration: Specialist should resolve within SLA (1-5 min depending on type)
- If resolved → Continue
- If not → Level 3

### Level 3: Specialist Resolves
**The right specialist** handles the issue with full authority in their domain.
- Librarian: Provides skills, suggests alternatives
- Butler: Rotates APIs, reallocates resources
- Gatekeeper: Reviews code, provides specific feedback
- Security Officer: Handles sensitive resource access
- Factory Manager: Spawns replacement agents
- Duration: Should resolve within 5 minutes
- If not → Level 4

### Level 4: Zoro Decides
**Only for**:
- Critical blockers that specialists can't resolve
- Decisions requiring strategic judgment
- Resource conflicts between lanes
- Security incidents
- All APIs exhausted with no alternatives

---

## When to Go Directly to Zoro

**IMMEDIATELY** (skip all levels):
- Security breach or suspected compromise
- All API keys exhausted across all providers
- Fundamental task misalignment discovered
- Human user needs to be consulted

**NEVER** go directly to Zoro for:
- Routine skill requests (→ Librarian)
- API rotations (→ Butler)
- Code review results (→ Gatekeeper)
- Resource allocation (→ Butler)

---

## Decision Flow: "Is This Safe to Do?"

```
ACTION TYPE                      AUTONOMOUS?
─────────────────────────────    ──────────────
Read files                       ✅ Yes
Write/edit files                 ✅ Yes
Generate code                    ✅ Yes
Internal analysis                ✅ Yes
Inter-agent communication        ✅ Yes
Monitoring & reporting           ✅ Yes

Git push                         ❌ Needs Gatekeeper approval
External API calls               ⚠️ Context-dependent
High-value transactions          ❌ Needs Security Officer approval
.env modifications               ❌ Needs Security Officer approval
Cleanup operations               ❌ Needs Moderator summons
Critical escalations             ❌ Needs Zoro approval
```

---

## Conflict Resolution

When two specialists disagree:
1. Moderator facilitates discussion
2. Each specialist presents their case
3. Apply PRINCIPLES.md tension resolution:
   - Safety > Speed
   - Learning > Completion
   - Transparency > Efficiency
   - Prevention > Recovery
4. If still unresolved → Zoro decides
