# Ultraplan Examples

Real-world examples showing ultraplan input, process, and output structure.

## Table of Contents

1. [Code Example: Bug Fix](#code-example-bug-fix)
2. [Code Example: New Feature](#code-example-new-feature)
3. [General Example: Workflow Design](#general-example-workflow-design)
4. [Complex Example: System Refactoring](#complex-example-system-refactoring)
5. [Output File Samples](#output-file-samples)

---

## Code Example: Bug Fix

### Task Input

```
/ultraplan fix the authentication timeout bug where users are logged out after 30 minutes of inactivity
```

### Mode Selection
**Selected**: Code Implementation Mode

### Complexity Classification
- **Task Type**: Bug Fix / Debugging
- **Complexity**: Medium (4-8 files affected, session handling across backend/frontend)
- **Investigation Depth**: 2-3 targeted subagents

### Investigation Phase (5-7 minutes)

**Subagent 1**: Audit authentication system
- Examined `/src/auth/authService.ts` - JWT implementation
- Found session timeout set to 1800 seconds (30 minutes) in config
- No token refresh logic implemented

**Subagent 2**: Audit frontend token management
- Examined `/src/stores/authStore.ts` - Token storage
- No automatic token refresh on activity
- No warning before expiration

**Subagent 3**: Check API endpoints
- Examined `/src/api/middleware/auth.ts` - Auth middleware
- Token validation but no refresh endpoint exists

### Output Directory
```
/Scrapbook/Bug_Fix/authentication_timeout_fix/
├── investigation_findings.md
├── implementation_plan.md
├── dependencies_map.md
├── validation_checklist.md
├── testing_strategy.md
└── rollback_plan.md
```

### Key Findings Summary

**Components that exist and function correctly**:
- JWT token generation (`/src/auth/authService.ts:15-42`)
- Token validation middleware (`/src/api/middleware/auth.ts:8-35`)
- Login endpoint (`/src/api/routes/auth.ts:12-28`)

**Components that exist but are broken**:
- Session timeout configuration is too aggressive (30 min vs desired 24 hr)
- No token refresh mechanism

**Components that don't exist**:
- Token refresh endpoint
- Frontend activity detector
- Token refresh logic in frontend store
- "Session expiring soon" user warning

### Execution Sequence (from implementation_plan.md)

**Step 1: Create Token Refresh Endpoint**
- Action: Add POST `/api/auth/refresh` endpoint that accepts valid JWT and returns new JWT with extended expiration
- Dependencies: none
- Files: `/src/api/routes/auth.ts`

**Step 2: Update Frontend Auth Store**
- Action: Add `refreshToken()` method and automatic refresh logic
- Dependencies: Step 1 (refresh endpoint must exist)
- Files: `/src/stores/authStore.ts`

**Step 3: Implement Activity Detection**
- Action: Track user activity (clicks, keyboard input) and trigger token refresh
- Dependencies: Step 2
- Files: `/src/utils/activityMonitor.ts` (new file)

**Step 4: Add Session Warning UI**
- Action: Show warning 5 minutes before expiration
- Dependencies: Step 2
- Files: `/src/components/SessionWarning.tsx` (new file)

**Step 5: Update Configuration**
- Action: Change token expiration to 24 hours in config
- Dependencies: Steps 1-4 (refresh logic must be in place first)
- Files: `/.env`, `/src/config/auth.ts`

### Token Usage
- Planning phase: ~520 tokens
- Execution phase (with plan): ~180 tokens
- **Total**: 700 tokens
- **Without ultraplan**: ~1,400 tokens (multiple iterations)
- **Savings**: 50%

---

## Code Example: New Feature

### Task Input

```
/ultraplan add a comment system to blog posts with support for nested replies, markdown formatting, and real-time updates
```

### Mode Selection
**Selected**: Code Implementation Mode

### Complexity Classification
- **Task Type**: New Feature Implementation
- **Complexity**: High (12+ files, database schema, WebSocket integration, new UI components)
- **Investigation Depth**: 5+ parallel subagents

### Investigation Phase (12-15 minutes)

**Subagent 1**: Database schema analysis
- Current blog posts table structure
- No comments table exists
- Need foreign keys and nested structure support

**Subagent 2**: API endpoint architecture
- REST API structure review
- No comment endpoints exist
- WebSocket server exists at `/src/websocket/server.ts`

**Subagent 3**: Frontend component structure
- Blog post display at `/src/components/BlogPost.tsx`
- No comment components exist
- Markdown renderer exists (`react-markdown` installed)

**Subagent 4**: Authentication & permissions
- User authentication works via JWT
- Need permission checks for comment CRUD operations

**Subagent 5**: Real-time infrastructure
- WebSocket server operational
- Need new event types for comment updates

### Output Directory
```
/Scrapbook/New_Feature_Implementation/blog_comment_system/
├── investigation_findings.md
├── implementation_plan.md
├── dependencies_map.md
├── validation_checklist.md
├── testing_strategy.md
└── rollback_plan.md
```

### Key Findings Summary

**What exists**:
- Blog posts table with proper schema
- WebSocket server for real-time updates
- Markdown rendering library
- User authentication system

**What's missing**:
- Comments table (database schema)
- API endpoints (GET, POST, PUT, DELETE comments)
- Comment UI components (CommentList, CommentForm, CommentItem)
- WebSocket event handlers for comments
- Comment permissions and moderation

### Execution Sequence Highlights

**Step 1-3**: Database (create migration, comments table, indexes)
**Step 4-7**: Backend API (CRUD endpoints, WebSocket events, permissions)
**Step 8-12**: Frontend Components (comment list, form, nested replies, real-time updates)
**Step 13-15**: Testing (unit tests, integration tests, E2E tests)
**Step 16**: Final validation and deployment

### Token Usage
- Planning phase: ~815 tokens
- Execution phase (with plan): ~340 tokens
- **Total**: 1,155 tokens
- **Without ultraplan**: ~2,800 tokens (multiple back-and-forth iterations)
- **Savings**: 59%

---

## General Example: Workflow Design

### Task Input

```
/ultraplan create an onboarding workflow for new software engineers joining our team
```

### Mode Selection
**Selected**: General Task Planning Mode

### Complexity Classification
- **Task Type**: Workflow Design / Process Improvement
- **Complexity**: Medium (6-8 workflow steps, multiple stakeholders, documentation requirements)
- **Investigation Depth**: 2-3 targeted subagents

### Investigation Phase (6-8 minutes)

**Subagent 1**: Current onboarding state
- No formal onboarding process exists
- New hires get laptop and repository access
- Learning happens ad-hoc

**Subagent 2**: Required resources and access
- GitHub organization access
- Development environment setup (MacOS + Docker + IDE)
- Slack channels, Notion workspace, AWS access
- Meeting invites (standup, sprint planning)

**Subagent 3**: Team structure and knowledge areas
- 3 teams: Backend, Frontend, DevOps
- Technology stack: Node.js, React, PostgreSQL, AWS
- Code review process exists but undocumented
- No architectural decision records

### Output Directory
```
~/Documents/Plans/engineer_onboarding_workflow/
├── investigation_findings.md
├── implementation_plan.md
├── dependencies_map.md
├── validation_checklist.md
├── resources_list.md
└── alternatives_analysis.md
```

### Key Findings Summary

**Current capabilities**:
- Can provision accounts (GitHub, Slack, AWS)
- Have tech stack documentation (scattered across Notion)
- Buddy system exists informally

**Gaps**:
- No structured timeline (what to do week 1, week 2, etc.)
- No onboarding checklist
- Missing: architecture overview, coding standards docs, deployment guide
- No feedback loop to improve onboarding

**Required new elements**:
- Day-by-day onboarding schedule
- Onboarding checklist (automated)
- Documentation hub for new engineers
- 30/60/90 day check-ins
- Onboarding metrics tracking

### Execution Sequence (from implementation_plan.md)

**Step 1: Document Current Architecture**
- Create architecture overview document with diagrams
- Map all services, databases, external integrations

**Step 2: Create Onboarding Checklist Template**
- GitHub issue template with all tasks
- Checklist items for Day 1, Week 1, Month 1

**Step 3: Build Documentation Hub**
- Centralized Notion page with all resources
- Links to repos, environments, tools, processes

**Step 4: Establish Buddy Program**
- Formal buddy assignment process
- Buddy responsibilities checklist
- Weekly check-in template

**Step 5: Create 30/60/90 Day Framework**
- Goals for each milestone
- Check-in meeting agendas
- Success criteria

**Step 6: Implement Feedback Loop**
- Exit survey for onboarding process
- Monthly review of onboarding metrics
- Continuous improvement cycle

### Token Usage
- Planning phase: ~410 tokens
- Execution phase: ~150 tokens
- **Total**: 560 tokens
- **Without structured approach**: ~1,200 tokens
- **Savings**: 53%

---

## Complex Example: System Refactoring

### Task Input

```
/ultraplan refactor the monolithic payment processing module into microservices with proper event sourcing and CQRS pattern
```

### Mode Selection
**Selected**: Code Implementation Mode

### Complexity Classification
- **Task Type**: Refactoring / Optimization
- **Complexity**: High (25+ files, architectural change, database migration, message queue integration)
- **Investigation Depth**: 8+ parallel subagents

### Investigation Phase (18-25 minutes)

**Subagent 1-2**: Current payment module analysis
- Monolithic `PaymentService` class (1,200 LOC)
- Handles: billing, subscriptions, invoicing, refunds, webhooks
- Direct database writes to single `payments` table

**Subagent 3-4**: Database schema and data migration
- Current schema: single `payments` table with 35 columns
- 150k+ payment records
- Foreign keys to users, subscriptions, products

**Subagent 5-6**: Integration points and dependencies
- Stripe webhook handler
- Subscription renewal cron job
- Invoice generation service
- Analytics pipeline depends on payment data

**Subagent 7-8**: Event sourcing and message queue infrastructure
- RabbitMQ exists but underutilized
- No event store exists
- No CQRS read models implemented

### Output Directory
```
/Scrapbook/Refactoring_Optimization/payment_microservices_migration/
├── investigation_findings.md            (8 pages)
├── implementation_plan.md               (15 pages - PRIMARY)
├── dependencies_map.md                  (dependency graph with 30+ nodes)
├── validation_checklist.md              (25 validation checkpoints)
├── testing_strategy.md                  (integration tests, E2E tests, load tests)
└── rollback_plan.md                     (detailed rollback for each phase)
```

### Key Architectural Decisions (from plan)

**Microservices to Create**:
1. **Payment Command Service** - Handles write operations (charge, refund)
2. **Payment Query Service** - Handles read operations (get payment, list payments)
3. **Subscription Service** - Manages subscription lifecycle
4. **Invoice Service** - Generates and sends invoices
5. **Event Store Service** - Stores all payment events
6. **Notification Service** - Sends payment-related emails/webhooks

### Execution Sequence Highlights (35 steps)

**Phase 1 (Steps 1-8): Infrastructure**
- Setup event store database (PostgreSQL)
- Configure RabbitMQ exchanges and queues
- Create base event sourcing framework
- Implement event store service

**Phase 2 (Steps 9-18): Command Side**
- Extract payment command handlers
- Implement event publishing
- Create aggregate roots
- Add command validation

**Phase 3 (Steps 19-26): Query Side**
- Build read models
- Implement event subscribers
- Create query service
- Setup projection rebuilding

**Phase 4 (Steps 27-30): Migration**
- Migrate existing data to event store
- Dual-write period (old + new system)
- Gradual traffic shift to new services
- Decommission old monolith

**Phase 5 (Steps 31-35): Validation & Cleanup**
- End-to-end testing
- Load testing
- Production validation
- Cleanup old code

### Safe Stopping Points
- After Step 8: Infrastructure ready, can pause
- After Step 18: Commands working, reads still on old system
- After Step 26: Both systems operational, can run in parallel
- After Step 30: New system primary, old system backup

### Token Usage
- Planning phase: ~1,250 tokens
- Execution phase (with plan): ~550 tokens
- **Total**: 1,800 tokens
- **Without ultraplan**: ~5,000+ tokens (many failed attempts, backtracking)
- **Savings**: 64%

---

## Output File Samples

### Sample: investigation_findings.md

```markdown
# Investigation Findings: Authentication Timeout Bug Fix

**Task**: Fix authentication timeout bug where users are logged out after 30 minutes

**Investigation Date**: 2025-11-05
**Mode**: Code Implementation
**Complexity**: Medium
**Subagents Launched**: 3

---

## FINDINGS SUMMARY

### Files Investigated
- `/src/auth/authService.ts` (152 lines)
- `/src/api/middleware/auth.ts` (89 lines)
- `/src/stores/authStore.ts` (201 lines)
- `/src/api/routes/auth.ts` (145 lines)
- `/config/auth.config.js` (28 lines)
- `/.env` (configuration file)

### Components That Exist and Function Correctly

**JWT Token Generation** (`/src/auth/authService.ts:15-42`)
- Functionality: Generates JWT tokens with user payload
- Library: `jsonwebtoken` v9.0.0
- Works correctly, no issues found

**Token Validation Middleware** (`/src/api/middleware/auth.ts:8-35`)
- Functionality: Validates incoming JWT tokens
- Properly checks signature and expiration
- Returns 401 on invalid tokens
- Works correctly

... [continues with detailed findings]
```

### Sample: implementation_plan.md

```markdown
# Implementation Plan: Authentication Timeout Bug Fix

**Generated**: 2025-11-05
**Task Type**: Bug Fix / Debugging
**Complexity**: Medium
**Est. Implementation Scope**: 4 files modified, 1 file created

---

## SECTION 1: CURRENT STATE SUMMARY

### Components that exist and function correctly

**File**: `/src/auth/authService.ts` (lines 15-42)
- **Functionality**: JWT token generation with user payload (id, email, role)
- **Dependencies**: Depends on `jsonwebtoken` library, used by login endpoint
- **Status**: ✅ Working correctly

... [continues with all components]

### Components that exist but are broken

**File**: `/config/auth.config.js` (line 8)
- **Issue**: JWT_EXPIRATION set to '30m' instead of '24h'
- **Impact**: Users are logged out after 30 minutes, causing UX issues
- **Root cause**: Configuration was set for testing and never updated for production

... [continues]

### Components that don't exist

**Required**: Token refresh endpoint
- **Purpose**: Allow frontend to request new JWT before expiration
- **Dependencies**: None
- **Integration points**: Called by frontend auth store

... [continues]

---

## SECTION 2: REQUIRED CHANGES

### Files to Modify

**File**: `/src/api/routes/auth.ts`
**Changes**: Add POST `/refresh` endpoint (lines 85-110, new)
**Rationale**: Enable token refresh without re-authentication

... [continues with all required changes]

---

## SECTION 3: EXECUTION SEQUENCE

**Step 1: Create Token Refresh Endpoint**
- **Action**: Add POST `/api/auth/refresh` to `/src/api/routes/auth.ts`
  - Accept current valid JWT in request header
  - Validate current token
  - Generate new token with extended expiration
  - Return new token in response
- **Dependencies**: none (first step)
- **Rationale**: Backend capability must exist before frontend can use it
- **Success criteria**: Can POST to `/api/auth/refresh` with valid token and receive new token
- **Potential issues**: Token validation might reject nearly-expired tokens; handle gracefully

... [continues for all 5 steps]

---

## SECTION 4: DETAILED SPECIFICATIONS

**File**: `/src/api/routes/auth.ts`

**Modification Type**: Modify Existing

**Current State** (lines 1-84):
[Existing auth routes: login, logout, verify]

**Required Changes** (add after line 84):
```typescript
// Token refresh endpoint
router.post('/refresh', async (req, res) => {
  try {
    const token = req.headers.authorization?.split(' ')[1];
    if (!token) {
      return res.status(401).json({ error: 'No token provided' });
    }

    // Validate current token
    const decoded = jwt.verify(token, process.env.JWT_SECRET);

    // Generate new token with same payload but fresh expiration
    const newToken = jwt.sign(
      { id: decoded.id, email: decoded.email, role: decoded.role },
      process.env.JWT_SECRET,
      { expiresIn: process.env.JWT_EXPIRATION }
    );

    res.json({ token: newToken, expiresIn: process.env.JWT_EXPIRATION });
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
});
```

**Rationale**:
- Allows authenticated users to refresh tokens without re-entering credentials
- Uses existing JWT verification logic
- Returns new token with fresh expiration

**Dependencies**:
- Depends on: JWT_SECRET and JWT_EXPIRATION environment variables
- Depended on by: Frontend auth store (Step 2)
- Side effects: None (stateless operation)

**Testing Requirements**:
- Unit test: Verify endpoint returns new token for valid input
- Unit test: Verify endpoint rejects invalid/expired tokens
- Integration test: Full refresh flow from frontend
- Edge case: Token refresh with 1 second until expiration

... [continues for all files]

---

## SECTION 5: VALIDATION CHECKPOINTS

**After Step 1: Refresh Endpoint Created**
- **Validation**: POST request to `/api/auth/refresh` with valid token returns new token
- **Expected outcome**: 200 response with `{ token: "...", expiresIn: "24h" }`
- **Validation method**:
  ```bash
  curl -X POST http://localhost:3000/api/auth/refresh \
    -H "Authorization: Bearer [valid-token]"
  ```
- **Failure indicators**: 401 response, 500 error, or no token in response
- **Recovery procedure**: Review endpoint code, check JWT_SECRET env var

... [continues for all checkpoints]

---

## SECTION 6: RISK MANAGEMENT

### Safe Stopping Points

**After Step 1**: Refresh endpoint exists but not used
- **System state**: Backend has new endpoint, frontend unchanged
- **Is system functional?**: Yes, existing login flow still works
- **Risk**: None (additive change)

... [continues]

### Rollback Procedures

**From Step 1**: Remove refresh endpoint
```bash
git revert [commit-hash]
# Or manually remove lines 85-110 from /src/api/routes/auth.ts
```

... [continues]

### Known Risks

**Risk**: Token refresh could fail if JWT_SECRET changes between token issuance and refresh
- **Mitigation**: Document JWT_SECRET as critical secret, include in secret rotation process
- **Detection**: Monitor refresh endpoint error rates

... [continues]

---

## SECTION 7: CONTEXT FOR EXECUTOR

**Background**:
Users reported being unexpectedly logged out during active sessions. Investigation revealed 30-minute token expiration. Business requirement: Users should remain logged in for 24 hours unless they explicitly log out.

**Constraints**:
- Must maintain backward compatibility with existing login flow
- Cannot require users to re-authenticate during fix deployment
- Must work across browser tabs (token refresh in one tab should update others)

**Success Definition**:
- Users remain logged in for 24 hours of activity
- Warning appears 5 minutes before expiration
- Token automatically refreshes on user activity
- No breaking changes to authentication API

**Assumptions**:
- Users want to remain logged in (not a security-focused application)
- Browser supports localStorage for token storage
- Network connectivity available for token refresh

**Open Questions**:
None (all ambiguities resolved during investigation)

**Handoff Notes**:
- Test thoroughly in production after deployment
- Monitor token refresh endpoint for errors
- Consider adding metrics for token lifetime analytics

**Common Pitfalls to Avoid**:
- Don't change JWT_EXPIRATION before implementing refresh logic
- Ensure activity monitor doesn't cause performance issues
- Test cross-tab synchronization

**Useful Resources**:
- JWT best practices: https://example.com/jwt-best-practices
- Our auth middleware docs: /docs/authentication.md
```

---

## Comparison: With vs Without Ultraplan

### Without Ultraplan (Traditional Approach)

**Interaction 1**:
```
User: Fix the auth timeout bug
Claude: I'll update the token expiration to 24 hours
[Makes change, pushes code]
```

**Iteration 2**:
```
User: Users still getting logged out
Claude: Oh, we need a refresh mechanism. Let me add that.
[Adds refresh endpoint]
```

**Iteration 3**:
```
User: It's better but users don't know they're about to be logged out
Claude: We need a warning UI. Let me add that.
[Adds warning component]
```

**Iteration 4**:
```
User: Warning appears but token doesn't refresh automatically
Claude: We need activity detection. Let me add that.
[Adds activity monitor]
```

**Result**: 4 iterations, ~1,800 tokens, 35 minutes, incomplete solution

### With Ultraplan

**Interaction 1**:
```
User: /ultraplan fix the auth timeout bug where users are logged out after 30 minutes
Claude: [Launches investigation, finds all issues, generates complete plan]
```

**Interaction 2**:
```
User: [Reviews plan] Looks good, execute the plan
Claude: [Executes all 5 steps from plan]
```

**Result**: 2 interactions, ~700 tokens, 25 minutes, complete solution

**Savings**: 61% fewer tokens, 29% faster, complete on first try

---

## Key Takeaways from Examples

1. **Zero assumptions prevent rework**: Investigation finds all issues upfront
2. **Complete plans save tokens**: Execute confidently without back-and-forth
3. **Scales with complexity**: Simple tasks finish fast, complex tasks get thorough planning
4. **Persistent documentation**: Plans work across sessions and team members
5. **Risk management built-in**: Every plan includes rollback procedures

---

**Next**: Try ultraplan on your own projects and share results!
