---
description: Universal Implementation Plan Generator - Zero-assumption planning for code implementations and general tasks
argument-hint: [task description]
allowed-tools: Task, Read, Write, Glob, Grep, Bash(mkdir:*), Bash(ls:*), Bash(test:*), AskUserQuestion
---

# /ultraplan - Universal Implementation Plan Generator

## MODE SELECTION

**Task**: $ARGUMENTS

Before we begin, let me understand the context for this planning task.

**Please select the planning mode**:

1. **Code Implementation Mode** - For software development tasks (bug fixes, features, refactoring, integrations, etc.)
   - Uses technical investigation with file analysis, dependency mapping, code structure
   - Output optimized for Claude Code execution in VSCode/terminal
   - Documentation saved to `/Scrapbook/[task_type]/[task_name]/`

2. **General Task Planning Mode** - For non-coding tasks (workflows, processes, research, projects, etc.)
   - Uses same exhaustive methodology applied to non-code contexts
   - Investigates resources, prerequisites, workflows, deliverables
   - Documentation saved to `~/Documents/Plans/[task_name]/`

**Which mode should I use for this task?**

---

## UNIVERSAL PLANNING PROTOCOL

Once mode is selected, execute the following protocol:

---

### PHASE 1: TASK CLASSIFICATION

<task_assessment>
Analyze the provided task and document:

**Task Type** (select one based on mode):

**For Code Implementation Mode**:
- [ ] New Feature Implementation
- [ ] Bug Fix / Debugging
- [ ] Refactoring / Optimization
- [ ] Integration / API Work
- [ ] Infrastructure / Tooling
- [ ] Testing / Quality Assurance

**For General Task Planning Mode**:
- [ ] Workflow Design / Process Improvement
- [ ] Research & Analysis
- [ ] Project Planning & Coordination
- [ ] Content Creation / Documentation
- [ ] Resource Acquisition / Setup
- [ ] Learning / Skill Development

**Complexity Classification** (auto-determine for both modes):
- **Low**: Isolated change, 1-3 components/steps, <100 units affected (LOC for code, discrete actions for general)
- **Medium**: Moderate integration, 4-10 components/steps, 100-500 units affected
- **High**: Cross-cutting concerns, 10+ components/steps, 500+ units affected

**Investigation Depth Assignment**:
- Low Complexity → Single-pass audit (1-2 focused investigations)
- Medium Complexity → 2-3 targeted subagents
- High Complexity → 5+ parallel subagents
</task_assessment>

---

### PHASE 2: EXHAUSTIVE INVESTIGATION

<requirements_inventory>
#### Step 1: Comprehensive Requirements List

**For Code Implementation Mode**, document:
- Files that must exist, be modified, or be created
- Dependencies between components (imports, services, libraries)
- Data structures and schemas (database, API contracts, types)
- API contracts and endpoints
- UI elements and components
- State management requirements
- Configuration changes (env vars, config files)
- Testing requirements
- Build/deployment considerations

**For General Task Planning Mode**, document:
- Resources required (tools, access, information, materials)
- Prerequisites and dependencies (skills, permissions, prior tasks)
- Key stakeholders or collaborators
- Workflows and process steps
- Deliverables and outputs
- Documentation needs
- Success criteria and validation methods
- Timeline considerations and milestones
</requirements_inventory>

<parallel_investigation>
#### Step 2: Scaled Investigation Strategy

**For Low Complexity Tasks**:
1. Launch 1-2 focused investigation subagents
2. Each subagent audits specific area
3. Document findings in single pass

**For Medium Complexity Tasks**:
1. Divide requirements into 2-3 logical investigation chunks
2. Launch targeted subagents for each chunk
3. Each subagent documents:
   - **Code Mode**: Components that exist and function / exist but are broken / don't exist / modifications required
   - **General Mode**: Resources available / resources needed / workflows that exist / gaps in current approach

**For High Complexity Tasks**:
1. Divide requirements into 5+ logical investigation chunks
2. Launch parallel subagents for deep-dive analysis
3. Each subagent provides detailed report:
   - **Code Mode**: Current state with exact file paths and line numbers / broken or missing components / required changes with specifications / dependencies on other chunks
   - **General Mode**: Current state of systems/processes / gaps and missing elements / required actions with specifications / dependencies on other investigation areas

**Investigation Execution**:
- Use Task tool with appropriate subagent types (Explore, Plan, general-purpose)
- For code: Use Glob, Grep, Read tools to examine codebase
- For general: Use research, documentation review, web search as needed
- Document all findings in working markdown files as investigation proceeds
</parallel_investigation>

<iterative_refinement>
#### Step 3: Gap Analysis and Re-Investigation

If initial investigation reveals:
- Incomplete understanding of current state
- Assumptions required to proceed
- Unclear dependencies or relationships
- Ambiguous requirements or specifications

Then:
1. Identify specific knowledge gaps
2. Launch additional targeted subagents to fill gaps
3. Repeat investigation until zero-assumption clarity achieved
4. Document all findings in working .md files
5. Update findings as new information emerges
</iterative_refinement>

---

### PHASE 3: DOCUMENTATION STRUCTURE

<file_organization>
**Base Path**:
- **Code Implementation Mode**: `/Scrapbook/[task_type]/[task_name]/`
- **General Task Planning Mode**: `~/Documents/Plans/[task_name]/`

**Required Files** (all modes):
1. `investigation_findings.md` - Complete audit results from all subagents
2. `implementation_plan.md` - **PRIMARY DELIVERABLE** - Step-by-step execution blueprint
3. `dependencies_map.md` - Component/task relationships and execution sequence
4. `validation_checklist.md` - Testing and verification procedures

**Additional Files for Code Mode**:
- `testing_strategy.md` - Test cases, coverage requirements, validation methods
- `rollback_plan.md` - Rollback procedures and safe stopping points

**Additional Files for General Mode**:
- `resources_list.md` - All required resources with acquisition methods
- `alternatives_analysis.md` - Alternative approaches and trade-offs

**Formatting Standards**:
- Detailed without verbosity - every word serves a purpose
- Concise and actionable - executor can follow without clarification
- Exact paths and references (absolute paths for code, specific resource links for general)
- Line numbers when modifying existing code
- Clear dependency markers and execution order
- No time estimates (focus on sequence, not duration)
- Zero assumptions or ambiguity
</file_organization>

---

### PHASE 4: IMPLEMENTATION PLAN CREATION

<deliverable_structure>
Create the **PRIMARY DELIVERABLE**: `implementation_plan.md`

#### Section 1: Current State Summary

**For Code Implementation Mode**:
```
**Components that exist and function correctly**:
- File: /exact/path/to/file.ts (lines X-Y)
- Functionality: [description]
- Dependencies: [what this depends on/provides]

**Components that exist but are broken**:
- File: /exact/path/to/file.ts (lines X-Y)
- Issue: [specific problem with evidence]
- Impact: [what this breaks downstream]
- Root cause: [why this is broken]

**Components that don't exist**:
- Required: [component name/description]
- Purpose: [why it's needed]
- Dependencies: [what depends on this]
- Integration points: [where this connects]
```

**For General Task Planning Mode**:
```
**Current State Analysis**:
- Existing workflows/processes: [description of what's in place]
- Current capabilities: [what can be done now]
- Available resources: [what you have access to]

**Gaps and Issues**:
- Missing elements: [what doesn't exist but should]
- Broken processes: [what exists but doesn't work]
- Resource gaps: [what's needed but not available]
- Blockers: [what's preventing progress]

**Required New Elements**:
- New workflows: [what needs to be established]
- New resources: [what needs to be acquired]
- New capabilities: [what needs to be developed]
- Dependencies: [what these new elements depend on]
```

#### Section 2: Required Changes

**For Code Implementation Mode**:
```
**Files to Create**:
- /path/to/new/file.ts - [purpose, what it provides, what depends on it]

**Files to Modify**:
- /path/to/existing/file.ts - [specific changes, affected lines, rationale]

**Files to Delete/Deprecate**:
- /path/to/old/file.ts - [reason for removal, migration plan for dependents]

**Configuration Updates**:
- [config file]: [specific changes with before/after examples]

**Dependencies to Add/Update**:
- [package name]@[version] - [purpose, why this version]

**Database/Schema Changes**:
- [migration description with DDL if applicable]
```

**For General Task Planning Mode**:
```
**Workflows to Create**:
- [workflow name] - [purpose, inputs, outputs, participants]

**Processes to Modify**:
- [process name] - [current state → desired state, specific changes]

**Resources to Acquire**:
- [resource name] - [purpose, acquisition method, setup requirements]

**Skills to Develop**:
- [skill/knowledge area] - [current level → target level, learning approach]

**Tools/Systems to Setup**:
- [tool name] - [purpose, installation method, configuration]

**Documentation to Create**:
- [document name] - [purpose, audience, key content areas]
```

#### Section 3: Execution Sequence

**Universal Format** (applies to both modes):
```
**Step 1: [Task Description]**
- Action: [specific action required with concrete details]
- Dependencies: [what must be complete first - "none" if first step]
- Rationale: [why this step is necessary and why in this order]
- Success criteria: [how to know this step is complete]
- Potential issues: [what could go wrong, how to detect]

**Step 2: [Task Description]**
- Action: [specific action required]
- Dependencies: Step 1 [explain the dependency relationship]
- Rationale: [why this order]
- Success criteria: [completion indicators]
- Potential issues: [risks and detection methods]

**Step 3: [Task Description]**
- Action: [specific action required]
- Dependencies: Step 2 [or "Steps 1 and 2" if both required]
- Rationale: [why this order]
- Success criteria: [completion indicators]
- Potential issues: [risks and detection methods]

[Continue for all steps...]

**Step N: Final Validation**
- Action: [comprehensive validation of entire implementation]
- Dependencies: All previous steps
- Rationale: [why this validates the complete solution]
- Success criteria: [final acceptance criteria]
```

#### Section 4: Detailed Specifications

**For Code Implementation Mode**:
```
**File**: /exact/path/to/file.ts

**Modification Type**: [Create New | Modify Existing | Delete]

**Current State** (if modifying):
Lines X-Y:
[Relevant existing code or detailed description]

**Required Changes**:
[Exact code changes, pseudocode, or detailed specifications]
[Include function signatures, type definitions, key algorithms]

**Rationale**:
[Why this change is necessary]
[How it solves the problem]
[Alternative approaches considered and rejected]

**Dependencies**:
- Depends on: [what this requires to function]
- Depended on by: [what will use this]
- Side effects: [what else this affects]

**Testing Requirements**:
- Unit tests: [what needs unit test coverage]
- Integration tests: [what integrations to test]
- Edge cases: [specific edge cases to verify]
```

**For General Task Planning Mode**:
```
**Workflow/Process**: [name]

**Type**: [Create New | Modify Existing | Replace]

**Current State** (if modifying):
[Detailed description of how things work now]
[Pain points and inefficiencies]

**Required Changes**:
[Step-by-step procedure for new/modified workflow]
[Inputs, transformations, outputs at each step]
[Roles and responsibilities]

**Rationale**:
[Why this workflow is necessary]
[Problems it solves]
[Benefits over current approach]

**Dependencies**:
- Requires: [what must be in place first]
- Enables: [what this makes possible]
- Impacts: [what this affects]

**Validation Methods**:
- Success indicators: [measurable outcomes]
- Testing approach: [how to validate before full rollout]
- Monitoring: [how to track effectiveness]
```

#### Section 5: Validation Checkpoints

**Universal Format**:
```
**After Step X: [checkpoint name]**
- Validation: [what to verify at this point]
- Expected outcome: [what success looks like]
- Validation method: [how to verify - test commands, manual checks, etc.]
- Failure indicators: [what suggests this step failed]
- Recovery procedure: [what to do if validation fails]

**After Step Y: [checkpoint name]**
- Validation: [what to verify]
- Expected outcome: [success criteria]
- Validation method: [verification approach]
- Failure indicators: [failure symptoms]
- Recovery procedure: [how to recover]

[Continue for all major milestones...]

**Final Validation: Complete Solution**
- Validation: [end-to-end verification]
- Expected outcome: [complete success criteria]
- Validation method: [comprehensive test approach]
- Acceptance criteria: [when to consider fully complete]
```

#### Section 6: Risk Management

**For Code Implementation Mode**:
```
**Safe Stopping Points**:
- After Step X: [system state - what's changed, what hasn't, is system functional?]
- After Step Y: [system state]

**Rollback Procedures**:
- From Step X: [specific commands/actions to undo]
- From Step Y: [rollback approach]

**Data Preservation**:
- Database: [backup requirements, migration rollback]
- File system: [what to backup before changes]
- State: [how to preserve application state]

**Known Risks**:
- [Risk description]: Mitigation strategy, detection method
- [Risk description]: Mitigation strategy, detection method
```

**For General Task Planning Mode**:
```
**Safe Stopping Points**:
- After Step X: [state of project/workflow - what's complete, what's pending]
- After Step Y: [project state]

**Rollback/Pivot Options**:
- From Step X: [how to reverse or modify approach]
- From Step Y: [alternative paths available]

**Continuity Planning**:
- Work products: [what to save/document at each stage]
- Knowledge transfer: [key information to preserve]
- Handoff points: [where others could take over]

**Known Risks**:
- [Risk description]: Mitigation strategy, early warning signs
- [Risk description]: Mitigation strategy, early warning signs
```

#### Section 7: Context for Executor

**Universal Section**:
```
**Background**:
[Why this task exists, business/personal context, goals]

**Constraints**:
[Limitations, requirements, non-negotiables]

**Success Definition**:
[What "done" looks like, acceptance criteria, quality standards]

**Assumptions**:
[Explicit list of assumptions made during planning - should be minimal]

**Open Questions**:
[Anything still unclear that executor may need to clarify - should be rare]

**Handoff Notes**:
[Key information for anyone executing this plan]
[Common pitfalls to avoid]
[Useful resources or references]
```

</deliverable_structure>

---

## SUCCESS CRITERIA

<validation_checklist>
The implementation plan is complete when ALL criteria are met:

**Investigation Completeness**:
- [ ] Current state is fully documented with exact references (file paths for code, specific resources for general)
- [ ] All broken/missing/incomplete elements are specifically identified with evidence
- [ ] All required changes are concretely specified (no hand-waving)
- [ ] Dependencies and relationships are explicitly mapped

**Zero-Assumption Standard**:
- [ ] No assumptions made - all ambiguities resolved through investigation
- [ ] Every "should" or "might" replaced with concrete findings
- [ ] All unknowns investigated or explicitly flagged as open questions
- [ ] Plan is actionable without additional research

**Executor Readiness**:
- [ ] Executor (human or AI) can follow plan without clarification questions
- [ ] Each step has clear success criteria and validation methods
- [ ] Dependencies between steps are explicit and justified
- [ ] Rollback/recovery procedures are documented

**Context Preservation**:
- [ ] Complete investigation findings preserved in markdown files
- [ ] Documentation enables clean hand-offs between sessions
- [ ] Future Claude Code sessions can execute from these artifacts
- [ ] Maximum context in minimal tokens (efficient rehydration)

**Quality Standards**:
- [ ] Writing is detailed but not verbose (every word serves purpose)
- [ ] Execution sequence is logical and dependency-aware
- [ ] Risk mitigation strategies are practical and specific
- [ ] Documentation structure is consistent and navigable
</validation_checklist>

---

## STRATEGIC CONTEXT

<purpose_statement>
**Why This Methodology Matters**:

This protocol invests tokens upfront in exhaustive investigation to prevent:
- Wasted effort from incorrect assumptions
- Rework from incomplete understanding
- Context loss between sessions
- Execution failures from missing information

**Token Economics**:
- **Invest NOW**: Thorough investigation with parallel subagents
- **Recover LATER**: Execute from plans without re-investigation
- **Session Transitions**: New Claude Code instances read plans, don't recreate them
- **Handoff Ready**: Artifacts work for any executor (human or AI)

**Why Markdown Documentation**:
These files are conversation save points and execution blueprints:
- Persist complete investigation findings permanently
- Enable context preservation across sessions
- Provide maximum information density for token efficiency
- Create shareable artifacts for collaboration
- Support iterative refinement as situation evolves

**Philosophy - Zero Assumptions**:
Assumptions are the enemy of reliable execution. Every assumption is:
- A potential point of failure
- A blocker requiring backtracking
- A token cost when it proves wrong
- A source of wasted implementation effort

This protocol eliminates assumptions through exhaustive investigation.
</purpose_statement>

---

## OUTPUT GUARANTEE

<expected_deliverables>
Upon protocol completion, you will have:

1. **Complete Investigation**: All findings from parallel subagents documented
2. **Bulletproof Plan**: Zero-assumption execution blueprint ready to follow
3. **Dependency Map**: Clear understanding of execution sequence and relationships
4. **Validation Framework**: Testing/verification procedures at each checkpoint
5. **Risk Management**: Rollback procedures and safe stopping points identified
6. **Preserved Context**: Full state saved for future reference or handoff

**Critical Boundary**:
This protocol STOPS after planning is complete. The next phase is execution, which should be:
- A separate Claude Code session (for clean context)
- Executed by reading the implementation_plan.md file
- Validated at each checkpoint using validation_checklist.md

**Do NOT mix planning and execution** - separation of concerns ensures quality in both phases.
</expected_deliverables>

---

## USAGE INSTRUCTIONS

To use this protocol:

1. Invoke with task description: `/ultraplan [your task]`
2. Select mode when prompted (Code Implementation or General Task Planning)
3. Wait for complete investigation phase (multiple parallel subagents may launch)
4. Review generated plan in appropriate directory:
   - Code: `/Scrapbook/[task_type]/[task_name]/`
   - General: `~/Documents/Plans/[task_name]/`
5. Execute plan in separate session by reading `implementation_plan.md`

**Key Principle**: Planning and execution are separate phases. Complete planning before beginning execution.

---

## EXECUTION BEGINS NOW

Based on your task and selected mode, I will now:

1. **Classify the task** and determine complexity
2. **Launch investigation subagents** in parallel (scaled to complexity)
3. **Analyze findings** and conduct re-investigation if gaps exist
4. **Create documentation** in mode-appropriate location
5. **Generate implementation plan** with zero assumptions

Let's begin. **Please specify which mode**: Code Implementation or General Task Planning?
