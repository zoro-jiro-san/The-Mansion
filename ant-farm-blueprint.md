# Ant Farm Blueprint: How to Spawn Teams

> **The Ant Farm is where all the work happens.**
> Created by: Factory Manager | Coordinated by: Moderator, Butler, Librarian, Gatekeeper

---

## What Is the Ant Farm?

The Ant Farm is the execution environment where sub-agents work in parallel lanes with embedded coordinators. It's not a concept — it's the actual structure that gets created for every task.

```
┌──────────────────────────────────────────────────────────┐
│                    ANT FARM STRUCTURE                      │
│                                                            │
│  ┌──────────────────────────────────────────────────┐    │
│  │           COORDINATORS (Embedded)                  │    │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌─────┐  │    │
│  │  │Moderator │ │  Butler  │ │Librarian │ │Gate-│  │    │
│  │  │(Coord)   │ │(Resource)│ │(Skills)  │ │keep │  │    │
│  │  └──────────┘ └──────────┘ └──────────┘ └─────┘  │    │
│  └──────────────────────────────────────────────────┘    │
│                                                            │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐            │
│  │ Lane 1   │    │ Lane 2   │    │ Lane 3   │            │
│  │ Team A   │    │ Team B   │    │ Team C   │            │
│  │ sa-001   │    │ sa-003   │    │ sa-005   │            │
│  │ sa-002   │    │ sa-004   │    │ sa-006   │            │
│  └──────────┘    └──────────┘    └──────────┘            │
│                                                            │
└──────────────────────────────────────────────────────────┘
```

---

## Ant Farm Creation Protocol (Factory Manager's Workflow)

### Phase 1: Task Analysis

```
1. Receive task from Zoro
2. Analyze task for:
   - Complexity (simple → 1 lane, complex → multiple lanes)
   - Parallelization opportunities (what can run simultaneously?)
   - Dependencies (what must be sequential?)
   - Resource requirements per component
3. Decompose into subtasks
4. Determine lane structure
```

### Phase 2: Resource Coordination

```
5. Contact Librarian:
   - Share PRDs for each subtask
   - Discuss skill requirements per lane
   - Receive skill recommendations
   - Confirm skill packages ready

6. Contact Butler:
   - Share resource requirements per lane
   - Request API key allocation per lane
   - Confirm rate limit capacity
   - Confirm context window availability

7. Both Librarian and Butler confirm readiness
```

### Phase 3: Ant Farm Construction

```
8. Create lane structure:
   {
     "ant_farm_id": "af-001",
     "task_id": "task-001",
     "lanes": [
       {
         "lane_id": "lane-1",
         "team": "team-a",
         "agents": ["sa-001", "sa-002"],
         "prd": "PRD-001",
         "skills": ["sk-react", "sk-typescript"],
         "api_key": "groq-key-1"
       },
       {
         "lane_id": "lane-2",
         "team": "team-b",
         "agents": ["sa-003", "sa-004"],
         "prd": "PRD-002",
         "skills": ["sk-python", "sk-database"],
         "api_key": "kimi-key-1"
       }
     ],
     "coordinators": ["moderator", "butler", "librarian", "gatekeeper"]
   }

9. Spawn sub-agents in each lane with:
   - Their PRD
   - Their skill packages (from Librarian)
   - Their API key (from Butler)
   - Their lane assignment
   - Coordinator communication channels
```

### Phase 4: Handoff

```
10. Hand off entire Ant Farm to Moderator:
    - Complete lane structure
    - All sub-agent assignments
    - All PRDs
    - Coordinator readiness confirmation

11. Moderator begins execution monitoring
12. Factory Manager tracks lifecycle from outside
```

---

## Lane Design Principles

### When to Use 1 Lane
- Simple task, single component
- No parallelization possible
- Sequential dependencies throughout

### When to Use Multiple Lanes
- Task has independent components
- Multiple services/features can be built simultaneously
- Testing can run parallel to development
- Frontend and backend can be separate

### Lane Independence
- Each lane has its own API key (from Butler)
- Each lane has its own skills (from Librarian)
- Each lane has its own PRD
- Lanes can fail independently without affecting others
- Cross-lane dependencies are tracked by Moderator

---

## Team Composition Guidelines

### Small Task (1 Lane, 1-2 Agents)
```
Lane 1: 1-2 sub-agents
Total: 1-2 agents + 4 coordinators
```

### Medium Task (2-3 Lanes, 3-6 Agents)
```
Lane 1: 2 sub-agents (e.g., frontend)
Lane 2: 2 sub-agents (e.g., backend)
Lane 3: 1-2 sub-agents (e.g., testing)
Total: 5-6 agents + 4 coordinators
```

### Large Task (4+ Lanes, 7+ Agents)
```
Lane 1: 2-3 agents (feature A)
Lane 2: 2-3 agents (feature B)
Lane 3: 2-3 agents (feature C)
Lane 4: 1-2 agents (integration/testing)
Total: 7-11 agents + 4 coordinators
```

---

## Ant Farm Data Structure (JSON)

```json
{
  "ant_farm_id": "af-001",
  "task_id": "task-001",
  "created_by": "factory-manager",
  "created_at": "2026-02-15T10:00:00Z",
  "status": "active|completed|failed",
  "lanes": [
    {
      "lane_id": "lane-1",
      "team_name": "team-frontend",
      "agents": [
        {
          "agent_id": "sa-001",
          "prd_id": "PRD-001",
          "skills": ["sk-react", "sk-typescript"],
          "api_key_id": "groq-key-1",
          "status": "active"
        }
      ],
      "dependencies": {
        "depends_on_lanes": [],
        "blocks_lanes": ["lane-3"]
      }
    }
  ],
  "coordinators": {
    "moderator": "active",
    "butler": "active",
    "librarian": "active",
    "gatekeeper": "active"
  },
  "metrics": {
    "total_agents": 6,
    "total_lanes": 3,
    "completion_percentage": 0,
    "active_blockers": 0
  }
}
```

---

## Critical Rules

1. **Always use Ant Farm structure**, even for single agents — the overhead is minimal, the benefits compound
2. **Coordinators go INSIDE**, not outside — they're embedded
3. **Every lane gets its own resources** — API keys, skills, PRDs
4. **Factory Manager creates, Moderator manages** — clear handoff
5. **Lanes are independent** — one lane failing doesn't kill the others
6. **No shortcuts** — don't spawn agents without going through this process
