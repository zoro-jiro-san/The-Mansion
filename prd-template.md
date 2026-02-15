# PRD Template (Product Requirements Document)

> **Every task in The Mansion gets a PRD. No exceptions.**
> Created by: Factory Manager | Used by: Sub-Agents, Moderator, Gatekeeper

---

## PRD-[ID]: [Task Title]

### Meta
```json
{
  "prd_id": "PRD-001",
  "created_by": "factory-manager",
  "created_at": "2026-02-15T10:00:00Z",
  "assigned_to": ["sa-001", "sa-002"],
  "lane": "lane-1",
  "priority": "low|medium|high|critical",
  "estimated_duration": "2 hours",
  "status": "draft|active|completed|failed"
}
```

---

### 1. Task Description

**What**: Clear, unambiguous description of what needs to be built/done.

**Why**: Business context — why does this matter?

**Scope**:
- ✅ In scope: [list what IS included]
- ❌ Out of scope: [list what is NOT included]

---

### 2. Roadmap (Step-by-Step)

```
Step 1: [Action]
  └── Expected output: [what this step produces]

Step 2: [Action]
  └── Expected output: [what this step produces]
  └── Depends on: Step 1

Step 3: [Action]
  └── Expected output: [what this step produces]
  └── Depends on: Step 1, Step 2

...
```

---

### 3. Checkpoints

Each checkpoint is a validation gate. Sub-agents must pass each checkpoint before proceeding.

| Checkpoint | Validation Criteria | Tests |
|-----------|-------------------|-------|
| CP-1: [Name] | [How to verify this is done correctly] | [Specific test cases] |
| CP-2: [Name] | [How to verify this is done correctly] | [Specific test cases] |
| CP-3: [Name] | [How to verify this is done correctly] | [Specific test cases] |

---

### 4. Success Criteria

The task is COMPLETE when ALL of the following are true:

- [ ] Criterion 1: [Specific, measurable outcome]
- [ ] Criterion 2: [Specific, measurable outcome]
- [ ] Criterion 3: [Specific, measurable outcome]
- [ ] All checkpoints passed
- [ ] Code reviewed by Gatekeeper
- [ ] Tests passing

---

### 5. Dependencies

| Dependency | Type | Provider | Status |
|-----------|------|----------|--------|
| [What's needed] | skill/resource/agent/code | [Who provides] | pending/ready |

---

### 6. Skills Required

```json
{
  "required_skills": ["skill-a", "skill-b"],
  "recommended_skills": ["skill-c"],
  "provided_by": "librarian",
  "skill_package_status": "pending|assigned"
}
```

---

### 7. Resource Requirements

```json
{
  "api_provider": "groq|kimi|other",
  "estimated_tokens": 50000,
  "estimated_requests": 100,
  "context_window_needs": "small|medium|large",
  "assigned_api_key": "pending|[key-id]",
  "provided_by": "butler"
}
```

---

### 8. Timeline

```
Start: [datetime]
CP-1 due: [datetime]
CP-2 due: [datetime]
CP-3 due: [datetime]
Completion: [datetime]
Buffer: [time for rework/review]
```

---

### 9. Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Risk description] | low/med/high | low/med/high | [How to handle] |

---

### 10. Learning Goals (Meta-Principle)

Beyond completing this task, what should we learn?

- [ ] [Pattern to watch for]
- [ ] [Skill combination to evaluate]
- [ ] [Process improvement to test]

---

## PRD JSON Format (Machine-Readable)

```json
{
  "prd_id": "PRD-001",
  "task": "Clear task description",
  "scope": {
    "in": ["item 1", "item 2"],
    "out": ["item 3"]
  },
  "roadmap": [
    {"step": 1, "action": "Step description", "output": "Expected output", "depends_on": []},
    {"step": 2, "action": "Step description", "output": "Expected output", "depends_on": [1]}
  ],
  "checkpoints": [
    {
      "id": "CP-1",
      "name": "Checkpoint name",
      "validation": "How to validate",
      "tests": ["Test 1", "Test 2"]
    }
  ],
  "success_criteria": ["Criterion 1", "Criterion 2"],
  "dependencies": [
    {"name": "Dep name", "type": "skill|resource|agent|code", "provider": "agent", "status": "pending|ready"}
  ],
  "skills_required": ["skill-a", "skill-b"],
  "resources": {
    "api_provider": "groq",
    "estimated_tokens": 50000,
    "context_needs": "medium"
  },
  "timeline": {
    "start": "2026-02-15T10:00:00Z",
    "estimated_completion": "2026-02-15T12:00:00Z"
  },
  "priority": "medium",
  "learning_goals": ["Pattern to observe"]
}
```
