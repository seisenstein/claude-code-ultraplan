# Ultraplan Usage Guide

Complete guide to using the `/ultraplan` slash command effectively.

## Basic Invocation

```
/ultraplan [task description]
```

Claude Code will:
1. Ask you to select a mode (Code Implementation or General Task Planning)
2. Classify task complexity
3. Launch parallel investigation
4. Generate comprehensive implementation plan
5. Save plan to appropriate directory

## Mode Selection

### Code Implementation Mode

**Use for**:
- Bug fixes and debugging
- New feature implementation
- Code refactoring and optimization
- API integrations
- Infrastructure and tooling setup
- Test suite creation

**Output location**: `/Scrapbook/[task_type]/[task_name]/`

**Example tasks**:
```
/ultraplan fix the authentication timeout bug
/ultraplan add OAuth 2.0 login with Google
/ultraplan refactor the payment processing module for better performance
/ultraplan integrate Stripe subscription API
/ultraplan setup CI/CD pipeline with GitHub Actions
```

### General Task Planning Mode

**Use for**:
- Workflow design and process improvement
- Research and analysis projects
- Project planning and coordination
- Content creation and documentation
- Resource acquisition and setup
- Learning and skill development

**Output location**: `~/Documents/Plans/[task_name]/`

**Example tasks**:
```
/ultraplan create onboarding workflow for new engineers
/ultraplan research and compare project management tools
/ultraplan plan Q1 marketing content calendar
/ultraplan design technical documentation structure for API
/ultraplan setup new MacBook development environment
```

## Understanding Complexity Levels

Ultraplan auto-determines complexity and scales investigation accordingly:

### Low Complexity
- **Indicators**: 1-3 files/components, isolated change, <100 LOC affected
- **Investigation**: 1-2 focused subagents
- **Time**: 2-5 minutes planning phase
- **Example**: "Fix typo in error message"

### Medium Complexity
- **Indicators**: 4-10 files/components, moderate integration, 100-500 LOC affected
- **Investigation**: 2-3 targeted subagents
- **Time**: 5-12 minutes planning phase
- **Example**: "Add new API endpoint with validation"

### High Complexity
- **Indicators**: 10+ files/components, cross-cutting concerns, 500+ LOC affected
- **Investigation**: 5+ parallel subagents
- **Time**: 12-25 minutes planning phase
- **Example**: "Migrate database from PostgreSQL to MongoDB"

## Output Files Explained

### All Modes Receive

**1. `investigation_findings.md`**
- Complete audit results from all subagents
- What exists and works correctly
- What exists but is broken
- What doesn't exist but is needed
- Exact file paths and line numbers (code mode)
- Resource availability and gaps (general mode)

**2. `implementation_plan.md` ⭐ PRIMARY DELIVERABLE**
- Section 1: Current state summary
- Section 2: Required changes
- Section 3: Execution sequence with dependencies
- Section 4: Detailed specifications
- Section 5: Validation checkpoints
- Section 6: Risk management and rollback
- Section 7: Context for executor

**3. `dependencies_map.md`**
- Component/task relationships
- Execution sequence with rationale
- Dependency graph
- Parallel execution opportunities

**4. `validation_checklist.md`**
- Testing procedures
- Verification methods
- Success criteria for each checkpoint
- Failure indicators and recovery

### Code Mode Additional Files

**5. `testing_strategy.md`**
- Unit test requirements
- Integration test scenarios
- Edge cases to verify
- Test coverage goals

**6. `rollback_plan.md`**
- Safe stopping points
- Rollback procedures from each phase
- Data preservation requirements
- Known risks and mitigation

### General Mode Additional Files

**5. `resources_list.md`**
- Required resources with acquisition methods
- Tool/access requirements
- Budget considerations
- Timeline dependencies

**6. `alternatives_analysis.md`**
- Alternative approaches considered
- Trade-offs and comparisons
- Rejected options with rationale
- Pivot points if primary approach fails

## Reading the Implementation Plan

The `implementation_plan.md` is structured for execution:

### Section 1: Current State Summary
Shows exactly what you're starting with—no assumptions.

### Section 2: Required Changes
Concrete list of files to create/modify/delete, or workflows to establish.

### Section 3: Execution Sequence
**This is your execution roadmap**:
```
Step 1: [Task]
- Action: [specific details]
- Dependencies: none
- Rationale: [why this first]
- Success criteria: [how to verify]
- Potential issues: [what could go wrong]

Step 2: [Task]
- Dependencies: Step 1 [why dependent]
...
```

Follow steps in order. Each step is independently verifiable.

### Section 4: Detailed Specifications
File-by-file or workflow-by-workflow details:
- Exact code changes or process steps
- Rationale for each change
- Dependencies and side effects
- Testing requirements

### Section 5: Validation Checkpoints
After each major step, verify:
- What to check
- Expected outcome
- How to verify
- What to do if validation fails

### Section 6: Risk Management
Safe stopping points where you can pause or rollback without breaking things.

### Section 7: Context for Executor
Background, constraints, and handoff notes for anyone executing this plan.

## Executing the Plan

**Critical**: Ultraplan generates plans, it does NOT execute them.

### Execution Workflow

**1. Review the Plan**
```bash
# Open the implementation plan
open /Scrapbook/[task_type]/[task_name]/implementation_plan.md
```

**2. Start Fresh Claude Code Session (Recommended)**
- Separates planning from execution
- Cleaner context
- Better token efficiency

**3. Load the Plan**
```
Read and execute the implementation plan at /Scrapbook/[task_type]/[task_name]/implementation_plan.md
```

**4. Execute Step-by-Step**
Claude Code will follow each step, verify at checkpoints, and handle issues.

**5. Validate at Checkpoints**
Refer to `validation_checklist.md` to verify each phase completed correctly.

### Why Separate Planning from Execution?

**Benefits**:
- ✅ Planning context doesn't pollute execution context
- ✅ Can review plan before committing
- ✅ Can hand off to different executor (human or AI)
- ✅ Can execute plan multiple times (similar projects)
- ✅ Can pause and resume without losing context

**Token Economics**:
- Planning session: 400-800 tokens
- Execution session (with plan): 100-300 tokens
- Execution session (without plan): 1000-2000 tokens

## Advanced Usage

### Chaining Ultraplan Outputs

Use one plan's output as input to another:

```
/ultraplan design authentication system
# Review output plan

/ultraplan implement the authentication system designed in /Scrapbook/New_Feature_Implementation/authentication_system/
```

### Iterative Refinement

If initial investigation reveals gaps:

```
/ultraplan investigate database performance issues
# Initial plan identifies slow queries

/ultraplan optimize the slow queries identified in /Scrapbook/Refactoring_Optimization/database_performance/investigation_findings.md
```

### Team Handoffs

Plans are designed for handoffs:

```
Developer A: /ultraplan create new payment flow
# Generates plan, commits to repo

Developer B (new session): Execute implementation plan at /Scrapbook/New_Feature_Implementation/payment_flow/implementation_plan.md
```

## Tips for Better Results

### 1. Be Specific in Task Description

❌ **Vague**: `/ultraplan fix the bug`
✅ **Better**: `/ultraplan fix the authentication timeout bug affecting users after 30 minutes of inactivity`

❌ **Vague**: `/ultraplan improve performance`
✅ **Better**: `/ultraplan optimize database queries in the user profile page that are causing 3+ second load times`

### 2. Provide Context When Needed

If task requires understanding:
```
/ultraplan add rate limiting to API endpoints

Context: We're getting 10k requests/second from a single IP. Need to implement 100 requests/minute per IP with proper error responses and retry headers.
```

### 3. Choose Correct Mode

Code changes → Code Implementation Mode
Everything else → General Task Planning Mode

### 4. Review Investigation Findings First

Before executing, check `investigation_findings.md` to ensure investigation was complete.

### 5. Use Validation Checkpoints

Don't skip verification steps. They catch issues early before they compound.

## Common Patterns

### Pattern 1: Bug Fix

```
/ultraplan debug and fix the user login failing with 500 error
# Investigates error, finds root cause, generates fix plan
# Execute plan to implement fix
```

### Pattern 2: New Feature

```
/ultraplan add comment system to blog posts with nested replies
# Investigates current blog structure, DB schema, UI components
# Generates complete implementation plan for comment system
# Execute plan to build feature
```

### Pattern 3: Refactoring

```
/ultraplan refactor authentication module to use JWT instead of sessions
# Investigates current auth flow, session dependencies
# Generates migration plan with rollback strategy
# Execute plan to refactor safely
```

### Pattern 4: Integration

```
/ultraplan integrate SendGrid email service for transactional emails
# Investigates email sending requirements, API contracts
# Generates integration plan with error handling
# Execute plan to integrate SendGrid
```

### Pattern 5: General Planning

```
/ultraplan create technical documentation strategy for API
# Investigates API surface, existing docs, user needs
# Generates documentation structure and process
# Execute plan to create docs
```

## Troubleshooting

### "Ultraplan makes assumptions instead of investigating"

**Cause**: Task description too vague
**Fix**: Provide more specific task description with context

### "Investigation phase takes too long"

**Cause**: High complexity task launched too many subagents
**Fix**: Break into smaller tasks, or wait—thorough investigation prevents execution failures

### "Plan is too detailed / not detailed enough"

**Cause**: Complexity misclassified
**Fix**: Provide hints in task description:
```
/ultraplan [task] (this is a simple change)
/ultraplan [task] (this affects many components)
```

### "Plan doesn't match my codebase structure"

**Cause**: Investigation didn't find correct files
**Fix**: Provide file paths in task description:
```
/ultraplan add validation to /src/api/users.ts endpoint
```

### "Generated plan has open questions"

**Cause**: Ambiguity couldn't be resolved through investigation
**Fix**: Answer open questions, then re-run ultraplan with clarifications

## Best Practices

1. **Trust the process** - Let investigation complete before judging results
2. **Read the plan** - Don't execute blindly, understand the approach
3. **Validate at checkpoints** - Catch issues early
4. **Save successful plans** - Reuse for similar projects
5. **Contribute improvements** - If you find gaps, share fixes with community
6. **Separate planning from execution** - Better results, better token economy

## Next Steps

- See [`EXAMPLES.md`](EXAMPLES.md) for real-world scenarios and full output examples
- See [`CONTRIBUTING.md`](CONTRIBUTING.md) to improve ultraplan
- Join discussions: [GitHub Discussions](https://github.com/[USERNAME]/claude-code-ultraplan/discussions)

---

**Questions?** Open an issue or start a discussion on GitHub.
