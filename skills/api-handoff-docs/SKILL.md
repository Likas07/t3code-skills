---
name: api-handoff-docs
description: Create cross-team API handoff documentation in either direction — backend-to-frontend specs (endpoint details, DTOs, validation, edge cases for frontend integration) AND frontend-to-backend requirements (data needs, UI states, actions, business rules). Use when user says 'handoff', 'API docs', 'backend requirements', 'frontend handoff', 'what data do I need', or needs to document API contracts between teams.
---

# API Handoff Documentation

Cross-team API documentation covering both directions: backend documenting APIs for frontend, and frontend communicating data needs to backend.

**Core philosophy:** Good collaboration means requesting, not demanding. Each side owns its domain and invites the other to push back.

---

## Part 1: Backend to Frontend Handoff

> **No Chat Output**: Produce the handoff document only. No discussion, no explanation -- just the markdown block saved to the handoff file.

You are a backend developer completing API work. Your task is to produce a structured handoff document that gives frontend developers (or their AI) full business and technical context to build integration/UI without needing to ask backend questions.

> **When to use**: After completing backend API work -- endpoints, DTOs, validation, business logic -- run this mode to generate handoff documentation.

> **Simple API shortcut**: If the API is straightforward (CRUD, no complex business logic, obvious validation), skip the full template -- just provide the endpoint, method, and example request/response JSON. Frontend can infer the rest.

### Goal
Produce a copy-paste-ready handoff document with all context a frontend AI needs to build UI/integration correctly and confidently.

### Inputs
- Completed API code (endpoints, controllers, services, DTOs, validation).
- Related business context from the task/user story.
- Any constraints, edge cases, or gotchas discovered during implementation.

### Workflow

1. **Collect context** -- confirm feature name, relevant endpoints, DTOs, auth rules, and edge cases.
2. **Create/update handoff file** -- write the document to `.claude/docs/ai/<feature-name>/api-handoff.md`. Increment the iteration suffix (`-v2`, `-v3`, ...) if rerunning after feedback.
3. **Paste template** -- fill every section below with concrete data. Omit subsections only when truly not applicable (note why).
4. **Double-check** -- ensure payloads match actual API behavior, auth scopes are accurate, and enums/validation reflect backend logic.

### Output Format

Produce a single markdown block structured as follows. Keep it dense -- no fluff, no repetition.

---

```markdown
# API Handoff: [Feature Name]

## Business Context
[2-4 sentences: What problem does this solve? Who uses it? Why does it matter? Include any domain terms the frontend needs to understand.]

## Endpoints

### [METHOD] /path/to/endpoint
- **Purpose**: [1 line: what it does]
- **Auth**: [required role/permission, or "public"]
- **Request**:
  ```json
  {
    "field": "type -- description, constraints"
  }
  ```
- **Response** (success):
  ```json
  {
    "field": "type -- description"
  }
  ```
- **Response** (error): [HTTP codes and shapes, e.g., 422 validation, 404 not found]
- **Notes**: [edge cases, rate limits, pagination, sorting, anything non-obvious]

[Repeat for each endpoint]

## Data Models / DTOs
[List key models/DTOs the frontend will receive or send. Include field types, nullability, enums, and business meaning.]

```typescript
// Example shape for frontend typing
interface ExampleDto {
  id: number;
  status: 'pending' | 'approved' | 'rejected';
  createdAt: string; // ISO 8601
}
```

## Enums & Constants
[List any enums, status codes, or magic values the frontend needs to know. Include display labels if relevant.]

| Value | Meaning | Display Label |
|-------|---------|---------------|
| `pending` | Awaiting review | Pending |

## Validation Rules
[Summarize key validation rules the frontend should mirror for UX -- required fields, min/max, formats, conditional rules.]

## Business Logic & Edge Cases
- [Bullet each non-obvious behavior, constraint, or gotcha]
- [e.g., "User can only submit once per day", "Soft-deleted items excluded by default"]

## Integration Notes
- **Recommended flow**: [e.g., "Fetch list -> select item -> submit form -> poll for status"]
- **Optimistic UI**: [safe or not, why]
- **Caching**: [any cache headers, invalidation triggers]
- **Real-time**: [websocket events, polling intervals if applicable]

## Test Scenarios
[Key scenarios frontend should handle -- happy path, errors, edge cases. Use as acceptance criteria or test cases.]

1. **Happy path**: [brief description]
2. **Validation error**: [what triggers it, expected response]
3. **Not found**: [when 404 is returned]
4. **Permission denied**: [when 403 is returned]

## Open Questions / TODOs
[Anything unresolved, pending PM decision, or needs frontend input. If none, omit section.]
```

---

### Rules (Backend to Frontend)
- **NO CHAT OUTPUT** -- produce only the handoff markdown block, nothing else.
- Be precise: types, constraints, examples -- not vague prose.
- Include real example payloads where helpful.
- Surface non-obvious behaviors -- don't assume frontend will "just know."
- If backend made trade-offs or assumptions, document them.
- Keep it scannable: headers, tables, bullets, code blocks.
- No backend implementation details (no file paths, class names, internal services) unless directly relevant to integration.
- If something is incomplete or TBD, say so explicitly.

### After Generating
Write the final markdown into the handoff file only -- do not echo it in chat. (If the platform requires confirmation, reference the file path instead of pasting contents.)

---

## Part 2: Frontend to Backend Requirements

You are a frontend developer documenting what data you need from backend. You describe the **what**, not the **how**. Backend owns implementation details.

> **No Chat Output**: ALL responses go to `.claude/docs/ai/<feature-name>/backend-requirements.md`
> **No Implementation Details**: Don't specify endpoints, field names, or API structure -- that's backend's call.

### The Point

This mode is for frontend devs to communicate data needs:
- What data do I need to render this screen?
- What actions should the user be able to perform?
- What business rules affect the UI?
- What states and errors should I handle?

**You're requesting, not demanding.** Backend may push back, suggest alternatives, or ask clarifying questions. That's healthy collaboration.

### What You Own vs. What Backend Owns

| Frontend Owns | Backend Owns |
|---------------|--------------|
| What data is needed | How data is structured |
| What actions exist | Endpoint design |
| UI states to handle | Field names, types |
| User-facing validation | API conventions |
| Display requirements | Performance/caching |

### Workflow

#### Step 1: Describe the Feature

Before listing requirements:

1. **What is this?** -- Screen, flow, component
2. **Who uses it?** -- User type, permissions
3. **What's the goal?** -- What does success look like?

#### Step 2: List Data Needs

For each screen/component, describe:

**Data I need to display:**
- What information appears on screen?
- What's the relationship between pieces?
- What determines visibility/state?

**Actions user can perform:**
- What can the user do?
- What's the expected outcome?
- What feedback should they see?

**States I need to handle:**
- Loading, empty, error, success
- Edge cases (partial data, expired, etc.)

#### Step 3: Surface Uncertainties

List what you're unsure about:
- Business rules you don't fully understand
- Edge cases you're not sure how to handle
- Places where you're guessing

**These invite backend to clarify or push back.**

#### Step 4: Leave Room for Discussion

End with open questions:
- "Would it make sense to...?"
- "Should I expect...?"
- "Is there a simpler way to...?"

### Output Format

Create `.claude/docs/ai/<feature-name>/backend-requirements.md`:

```markdown
# Backend Requirements: <Feature Name>

## Context
[What we're building, who it's for, what problem it solves]

## Screens/Components

### <Screen/Component Name>
**Purpose**: What this screen does

**Data I need to display**:
- [Description of data piece, not field name]
- [Another piece]
- [Relationships between pieces]

**Actions**:
- [Action description] -> [Expected outcome]
- [Another action] -> [Expected outcome]

**States to handle**:
- **Empty**: [When/why this happens]
- **Loading**: [What's being fetched]
- **Error**: [What can go wrong, what user sees]
- **Special**: [Any edge cases]

**Business rules affecting UI**:
- [Rule that changes what's visible/enabled]
- [Permissions that affect actions]

### <Next Screen/Component>
...

## Uncertainties
- [ ] Not sure if [X] should show when [Y]
- [ ] Don't understand the business rule for [Z]
- [ ] Guessing that [A] means [B]

## Questions for Backend
- Would it make sense to combine [X] and [Y]?
- Should I expect [Z] to always be present?
- Is there existing data I can reuse for [W]?

## Discussion Log
[Backend responses, decisions made, changes to requirements]
```

### Good vs. Bad Requests

**Bad (Dictating Implementation):**
> "I need a GET /api/contracts endpoint that returns an array with fields: id, title, status, created_at"

**Good (Describing Needs):**
> "I need to show a list of contracts. Each item shows the contract title, its current status, and when it was created. User should be able to filter by status."

**Bad (Assuming Structure):**
> "The provider object should be nested inside the contract response"

**Good (Describing Relationship):**
> "For each contract, I need to show who the provider is (their name and maybe logo)"

**Bad (No Context):**
> "I need contract data"

**Good (With Context):**
> "On the dashboard, there's a 'Recent Contracts' widget showing the 5 most recent contracts. User clicks one to go to detail page."

### Encouraging Pushback

Include these prompts in your requirements:

- "Let me know if this doesn't make sense for how the data is structured"
- "Open to suggestions on a better approach"
- "Not sure if this is the right way to think about it"
- "Push back if this complicates things unnecessarily"

**Good collaboration = frontend describes the problem, backend proposes the solution.**

### Rules (Frontend to Backend)

- **NO IMPLEMENTATION DETAILS** -- don't specify endpoints, methods, field names
- **DESCRIBE, DON'T PRESCRIBE** -- say what you need, not how to provide it
- **INCLUDE CONTEXT** -- why you need it helps backend make better choices
- **SURFACE UNKNOWNS** -- don't hide confusion, invite clarification
- **INVITE PUSHBACK** -- explicitly ask for backend's input
- **UPDATE THE DOC** -- add backend responses to Discussion Log
- **STAY HUMBLE** -- you're asking, not demanding

### After Backend Responds

Update the requirements doc:
1. Add responses to Discussion Log
2. Adjust requirements based on feedback
3. Mark resolved uncertainties
4. Note any decisions made

The doc becomes the source of truth for what was agreed.

---

## The Bottom Line

**Backend to Frontend:** Be precise, be complete, surface the non-obvious. Frontend should never need to read your source code.

**Frontend to Backend:** Describe the problem, not the solution. Invite pushback. The best API contracts come from both sides collaborating.
