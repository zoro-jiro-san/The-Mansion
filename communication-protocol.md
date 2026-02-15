# Communication Protocol: How Agents Talk

> **Clear communication prevents chaos. Every message follows this protocol.**

---

## Message Format (Standard)

Every inter-agent message uses this structure:

```json
{
  "message_id": "msg-uuid",
  "from": "agent_name",
  "to": "agent_name",
  "type": "request|response|update|notification|escalation",
  "priority": "low|medium|high|critical",
  "payload": {},
  "correlation_id": "uuid (links request → response)",
  "timestamp": "2026-02-15T10:30:00Z"
}
```

---

## Communication Map

```
                         ┌─────────┐
                    ┌────│  ZORO   │────┐
                    │    └─────────┘    │
                    ▼                   ▼
            ┌──────────────┐    ┌──────────────┐
            │   Factory    │    │  (receives   │
            │   Manager    │    │   reports)    │
            └──────┬───────┘    └──────────────┘
                   │                   ▲
        ┌──────────┼──────────┐        │
        ▼          ▼          ▼        │
  ┌──────────┐ ┌────────┐ ┌──────┐    │
  │Librarian │ │ Butler │ │Moder-│────┘
  └────┬─────┘ └───┬────┘ │ator  │
       │           │      └──┬───┘
       │           │         │
       ▼           ▼         ▼
  ┌──────────────────────────────┐
  │        SUB-AGENTS            │
  │  (in lanes, send updates     │
  │   to Moderator, code to      │
  │   Gatekeeper)                │
  └──────────┬───────────────────┘
             │
             ▼
       ┌───────────┐
       │ Gatekeeper │ (code review)
       └───────────┘
```

---

## Channel Definitions

### Zoro ↔ Factory Manager
**Direction**: Zoro → Factory Manager (task delegation)
**Message Types**: Task assignments
```json
{
  "type": "request",
  "payload": {
    "action": "create_ant_farm",
    "task_description": "Build user authentication system",
    "requirements": ["OAuth2", "JWT", "session management"],
    "priority": "high"
  }
}
```

### Factory Manager ↔ Librarian
**Direction**: Bidirectional (skill negotiation)
**Message Types**: Skill requests, recommendations
```json
// Request
{
  "type": "request",
  "payload": {
    "action": "skill_match",
    "prd_id": "PRD-001",
    "task_type": "web development",
    "technologies": ["React", "TypeScript", "Node.js"]
  }
}

// Response
{
  "type": "response",
  "payload": {
    "recommended_skills": ["sk-react", "sk-typescript", "sk-node"],
    "skill_packages_ready": true,
    "notes": "Recommend pairing sk-react with sk-testing-jest based on past success"
  }
}
```

### Factory Manager ↔ Butler
**Direction**: Factory Manager → Butler (resource requests)
**Message Types**: API key allocation requests
```json
{
  "type": "request",
  "payload": {
    "action": "allocate_api_keys",
    "lanes": [
      {"lane_id": "lane-1", "estimated_tokens": 50000, "priority": "high"},
      {"lane_id": "lane-2", "estimated_tokens": 30000, "priority": "medium"}
    ]
  }
}
```

### Sub-Agent → Moderator (Status Updates)
**Frequency**: Every 30-60 seconds
```json
{
  "type": "update",
  "payload": {
    "agent_id": "sa-001",
    "task_id": "task-001",
    "progress": 65,
    "current_checkpoint": "CP-2",
    "blockers": [],
    "estimated_completion": "2026-02-15T11:30:00Z"
  }
}
```

### Sub-Agent → Moderator (Blocker Report)
**Frequency**: IMMEDIATELY when blocked
**Priority**: Always high or critical
```json
{
  "type": "escalation",
  "priority": "high",
  "payload": {
    "agent_id": "sa-001",
    "blocker_type": "skill",
    "description": "Need OAuth2 skill for Google authentication integration",
    "severity": "high",
    "blocked_since": "2026-02-15T10:28:00Z"
  }
}
```

### Moderator → Zoro (Progress Report)
**Frequency**: Every 5 minutes or immediately for critical issues
```json
{
  "type": "update",
  "payload": {
    "summary": "2 of 3 lanes active, 1 blocked",
    "completion_percentage": 45,
    "active_blockers": [
      {"blocker_id": "BLK-001", "type": "skill", "severity": "high", "routed_to": "librarian"}
    ],
    "resource_utilization": {
      "api_usage": "55% average across lanes",
      "context_usage": "40% average"
    },
    "dashboard_url": "https://github.com/user/monitoring-dashboard"
  }
}
```

### Sub-Agent → Gatekeeper (Code Review)
```json
{
  "type": "request",
  "payload": {
    "action": "code_review",
    "agent_id": "sa-001",
    "lane": "lane-1",
    "files": ["src/auth.ts", "src/middleware.ts", "tests/auth.test.ts"],
    "lines_of_code": 347,
    "description": "Authentication middleware with JWT validation"
  }
}
```

### Moderator → Janitor (Cleanup Summons)
**ONLY sent when ALL tasks are complete**
```json
{
  "type": "request",
  "priority": "low",
  "payload": {
    "action": "cleanup",
    "verification": {
      "all_tasks_complete": true,
      "all_lanes_complete": true,
      "all_code_pushed": true,
      "zoro_confirmed": true
    },
    "cleanup_candidates": [
      {"path": "/tmp/build-cache", "type": "cache"},
      {"path": "/tmp/context-summaries", "type": "context"}
    ]
  }
}
```

---

## Priority Levels

| Priority | Use When | Expected Response Time |
|----------|----------|----------------------|
| Low | FYI updates, non-blocking info | When convenient |
| Medium | Standard requests, regular updates | Within 2 minutes |
| High | Blockers, important decisions | Within 1 minute |
| Critical | Security issues, all-lanes-blocked, failures | IMMEDIATE |

---

## Communication Rules

1. **Every message gets a response** — even if it's just an acknowledgment
2. **Blockers are ALWAYS high or critical priority** — never low or medium
3. **Status updates are fire-and-forget** — Moderator processes them, no response needed
4. **Escalations include full context** — don't make the recipient ask follow-up questions
5. **Correlation IDs link conversations** — always reference the original request
6. **No side channels** — all communication follows the defined channels
7. **Security-sensitive data is NEVER in messages** — use references, not values
