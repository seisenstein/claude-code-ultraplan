# Claude Code Ultraplan - Universal Implementation Plan Generator

**Zero-assumption planning for code implementations and general tasks**

Transform vague tasks into bulletproof, executable implementation plans. This slash command forces exhaustive investigation before planning, preventing assumptions that lead to failed implementations.

> 🎯 **Part of [Collaborative Prompt Engineering #001](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)** by [LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/) - A community initiative to build and refine the definitive implementation planning prompt for Claude Code.

## Table of Contents

- [What This Does](#what-this-does)
- [Quick Start](#quick-start)
- [Installation](#installation)
- [Usage Guide](#usage-guide)
- [Examples](#examples)
- [How It Works](#how-it-works)
- [Why This Matters](#why-this-matters)
- [Contributing](#contributing)
- [Version](#version)
- [Support](#support)

## What This Does

Ultraplan turns "fix this bug" or "add this feature" into comprehensive, executable plans through:
- **Dual-mode operation**: Code implementation mode + General task planning mode
- **Exhaustive investigation**: Parallel subagents audit your codebase/requirements
- **Zero assumptions**: Every ambiguity resolved through investigation
- **Persistent documentation**: Markdown files preserve context across sessions
- **Token efficiency**: Invest upfront in investigation, recover in execution

## Quick Start

### Choose Your Approach

**🔹 Option 1: Try It Once** (No installation)
- Perfect for: Testing, one-off tasks, seeing how it works first
- Takes: 2 minutes to start

**🔹 Option 2: Install Permanently** (Recommended for regular use)
- Perfect for: Regular workflow, want `/ultraplan` in all sessions
- Takes: 3 minutes to install

---

### Option 1: Try It Once (No Installation)

Clone and use immediately without installing:

```bash
git clone https://github.com/seisenstein/claude-code-ultraplan.git
cd claude-code-ultraplan
```

Then tell Claude Code:
```
Read ultraplan.md and apply its planning protocol to this task: [your task description]
```

**Example**:
```
Read ultraplan.md and apply its planning protocol to this task: add OAuth authentication to my Express app
```

Claude Code will read the prompt and generate a complete implementation plan.

**When to use one-time approach:**
- ✅ Testing ultraplan before committing to installation
- ✅ One-off planning task
- ✅ Want to see how it works first
- ✅ Don't need `/ultraplan` in future sessions

---

## Installation

### For Claude Code (Self-Installation)

**Copy and paste this prompt to Claude Code:**

```
Please install the ultraplan slash command to my global Claude Code commands directory:

1. First, ensure the global commands directory exists by running: mkdir -p ~/.claude/commands

2. Download the ultraplan.md file from the repository using curl:
   curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/master/ultraplan.md

3. Verify the installation by checking the file exists and showing its size:
   ls -lh ~/.claude/commands/ultraplan.md

4. Once complete, confirm that I can now use `/ultraplan [task description]` in any Claude Code session.

Example usage: /ultraplan add user authentication to my web app
```

**What Claude Code will do:**
- Create the `~/.claude/commands/` directory if it doesn't exist
- Download the ultraplan.md command file from the repository
- Verify the file was installed correctly (should be approximately 20-25 KB)
- Confirm the installation and provide usage examples

### Manual Installation

#### One-Line Install (Recommended)

```bash
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/master/ultraplan.md
```

#### Clone and Copy

```bash
# Clone the repository
git clone https://github.com/seisenstein/claude-code-ultraplan.git
cd claude-code-ultraplan

# Create commands directory if needed
mkdir -p ~/.claude/commands

# Copy ultraplan command
cp ultraplan.md ~/.claude/commands/

# Verify
ls ~/.claude/commands/ultraplan.md
```

#### Download from GitHub

1. Visit https://github.com/seisenstein/claude-code-ultraplan
2. Click on `ultraplan.md`
3. Click "Raw" button
4. Save file as `~/.claude/commands/ultraplan.md`

### Platform-Specific Notes

**macOS & Linux:**
- Global commands: `~/.claude/commands/`
- No additional permissions needed

**Windows:**
- Global commands: `%USERPROFILE%\.claude\commands\`
- PowerShell command:
  ```powershell
  Invoke-WebRequest -Uri "https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/master/ultraplan.md" -OutFile "$env:USERPROFILE\.claude\commands\ultraplan.md"
  ```

### Verify Installation

Restart Claude Code, then in any session:
```
/ultraplan test task
```

Claude Code should respond with mode selection prompt (Code Implementation or General Task Planning).

### Updating

To update to the latest version:

```bash
# Download latest version (overwrites existing)
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/master/ultraplan.md

# Restart Claude Code
```

### Uninstallation

To remove ultraplan:

```bash
rm ~/.claude/commands/ultraplan.md
```

Restart Claude Code for changes to take effect.

### Troubleshooting

**Command not appearing after installation:**
1. Restart Claude Code completely
2. Verify file exists: `ls ~/.claude/commands/ultraplan.md`
3. Check file extension is `.md` not `.md.txt`
4. Ensure file is in correct location (not project-specific `.claude/commands/`)

**Permission denied errors:**
```bash
mkdir -p ~/.claude/commands
chmod 755 ~/.claude/commands
```

**File exists but command doesn't work:**
1. Verify file contents: `head -20 ~/.claude/commands/ultraplan.md`
2. Check for YAML frontmatter at top of file
3. Ensure file wasn't corrupted during download
4. Re-download from repository

---

## Usage Guide

### Basic Invocation

```
/ultraplan [task description]
```

Claude Code will:
1. Ask you to select a mode (Code Implementation or General Task Planning)
2. Classify task complexity
3. Launch parallel investigation
4. Generate comprehensive implementation plan
5. Save plan to appropriate directory

### Mode Selection

#### Code Implementation Mode

**Use for:**
- Bug fixes and debugging
- New feature implementation
- Code refactoring and optimization
- API integrations
- Infrastructure and tooling setup
- Test suite creation

**Output location:** `/Scrapbook/[task_type]/[task_name]/`

**Example tasks:**
```
/ultraplan fix the authentication timeout bug
/ultraplan add OAuth 2.0 login with Google
/ultraplan refactor the payment processing module for better performance
/ultraplan integrate Stripe subscription API
/ultraplan setup CI/CD pipeline with GitHub Actions
```

#### General Task Planning Mode

**Use for:**
- Workflow design and process improvement
- Research and analysis projects
- Project planning and coordination
- Content creation and documentation
- Resource acquisition and setup
- Learning and skill development

**Output location:** `~/Documents/Plans/[task_name]/`

**Example tasks:**
```
/ultraplan create onboarding workflow for new engineers
/ultraplan research and compare project management tools
/ultraplan plan Q1 marketing content calendar
/ultraplan design technical documentation structure for API
/ultraplan setup new MacBook development environment
```

### Understanding Complexity Levels

Ultraplan auto-determines complexity and scales investigation accordingly:

**Low Complexity:**
- Indicators: 1-3 files/components, isolated change, <100 LOC affected
- Investigation: 1-2 focused subagents
- Time: 2-5 minutes planning phase
- Example: "Fix typo in error message"

**Medium Complexity:**
- Indicators: 4-10 files/components, moderate integration, 100-500 LOC affected
- Investigation: 2-3 targeted subagents
- Time: 5-12 minutes planning phase
- Example: "Add new API endpoint with validation"

**High Complexity:**
- Indicators: 10+ files/components, cross-cutting concerns, 500+ LOC affected
- Investigation: 5+ parallel subagents
- Time: 12-25 minutes planning phase
- Example: "Migrate database from PostgreSQL to MongoDB"

### Output Files Explained

#### All Modes Receive:

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

#### Code Mode Additional Files:

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

#### General Mode Additional Files:

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

### Executing the Plan

**Critical:** Ultraplan generates plans, it does NOT execute them.

#### Execution Workflow:

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

#### Why Separate Planning from Execution?

**Benefits:**
- ✅ Planning context doesn't pollute execution context
- ✅ Can review plan before committing
- ✅ Can hand off to different executor (human or AI)
- ✅ Can execute plan multiple times (similar projects)
- ✅ Can pause and resume without losing context

**Token Economics:**
- Planning session: 400-800 tokens
- Execution session (with plan): 100-300 tokens
- Execution session (without plan): 1000-2000 tokens

### Tips for Better Results

**1. Be Specific in Task Description**

❌ Vague: `/ultraplan fix the bug`
✅ Better: `/ultraplan fix the authentication timeout bug affecting users after 30 minutes of inactivity`

❌ Vague: `/ultraplan improve performance`
✅ Better: `/ultraplan optimize database queries in the user profile page that are causing 3+ second load times`

**2. Provide Context When Needed**

```
/ultraplan add rate limiting to API endpoints

Context: We're getting 10k requests/second from a single IP. Need to implement 100 requests/minute per IP with proper error responses and retry headers.
```

**3. Choose Correct Mode**

Code changes → Code Implementation Mode
Everything else → General Task Planning Mode

**4. Review Investigation Findings First**

Before executing, check `investigation_findings.md` to ensure investigation was complete.

**5. Use Validation Checkpoints**

Don't skip verification steps. They catch issues early before they compound.

---

## Examples

### Example 1: Bug Fix (Code Mode)

**Task Input:**
```
/ultraplan fix the authentication timeout bug where users are logged out after 30 minutes of inactivity
```

**Complexity:** Medium (4-8 files affected)
**Investigation Time:** 5-7 minutes
**Subagents:** 3 parallel investigators

**Output Directory:**
```
/Scrapbook/Bug_Fix/authentication_timeout_fix/
├── investigation_findings.md
├── implementation_plan.md
├── dependencies_map.md
├── validation_checklist.md
├── testing_strategy.md
└── rollback_plan.md
```

**Key Findings:**
- Found session timeout set to 1800 seconds (30 minutes) in config
- No token refresh logic implemented
- No automatic token refresh on user activity
- No warning before expiration

**Execution Sequence (5 steps):**
1. Create token refresh endpoint
2. Update frontend auth store
3. Implement activity detection
4. Add session warning UI
5. Update configuration

**Token Usage:**
- Planning: ~520 tokens
- Execution (with plan): ~180 tokens
- **Total: 700 tokens**
- Without ultraplan: ~1,400 tokens
- **Savings: 50%**

### Example 2: New Feature (Code Mode)

**Task Input:**
```
/ultraplan add a comment system to blog posts with support for nested replies, markdown formatting, and real-time updates
```

**Complexity:** High (12+ files, database schema, WebSocket integration)
**Investigation Time:** 12-15 minutes
**Subagents:** 5+ parallel investigators

**Output Directory:**
```
/Scrapbook/New_Feature_Implementation/blog_comment_system/
├── investigation_findings.md
├── implementation_plan.md
├── dependencies_map.md
├── validation_checklist.md
├── testing_strategy.md
└── rollback_plan.md
```

**Key Findings:**
- Blog posts table exists with proper schema
- WebSocket server operational
- Markdown rendering library installed
- No comments table or API endpoints exist

**Execution Sequence (16 steps):**
- Steps 1-3: Database (migration, comments table, indexes)
- Steps 4-7: Backend API (CRUD endpoints, WebSocket events, permissions)
- Steps 8-12: Frontend (comment list, form, nested replies, real-time)
- Steps 13-15: Testing (unit, integration, E2E)
- Step 16: Validation and deployment

**Token Usage:**
- Planning: ~815 tokens
- Execution: ~340 tokens
- **Total: 1,155 tokens**
- Without ultraplan: ~2,800 tokens
- **Savings: 59%**

### Example 3: Workflow Design (General Mode)

**Task Input:**
```
/ultraplan create an onboarding workflow for new software engineers joining our team
```

**Complexity:** Medium (6-8 workflow steps)
**Investigation Time:** 6-8 minutes
**Subagents:** 3 targeted investigators

**Output Directory:**
```
~/Documents/Plans/engineer_onboarding_workflow/
├── investigation_findings.md
├── implementation_plan.md
├── dependencies_map.md
├── validation_checklist.md
├── resources_list.md
└── alternatives_analysis.md
```

**Key Findings:**
- No formal onboarding process exists
- New hires get laptop and repository access only
- Tech stack documentation scattered across Notion
- Missing: architecture overview, coding standards, deployment guide

**Execution Sequence (6 steps):**
1. Document current architecture
2. Create onboarding checklist template
3. Build documentation hub
4. Establish buddy program
5. Create 30/60/90 day framework
6. Implement feedback loop

**Token Usage:**
- Planning: ~410 tokens
- Execution: ~150 tokens
- **Total: 560 tokens**
- Without structured approach: ~1,200 tokens
- **Savings: 53%**

### Comparison: With vs Without Ultraplan

**Without Ultraplan (Traditional Approach):**
```
Iteration 1: User: "Fix the auth timeout bug"
           Claude: "I'll update the token expiration to 24 hours"
           [Makes change, pushes code]

Iteration 2: User: "Users still getting logged out"
           Claude: "Oh, we need a refresh mechanism. Let me add that."
           [Adds refresh endpoint]

Iteration 3: User: "Better but users don't know they're about to be logged out"
           Claude: "We need a warning UI. Let me add that."
           [Adds warning component]

Iteration 4: User: "Warning appears but token doesn't refresh automatically"
           Claude: "We need activity detection. Let me add that."
           [Adds activity monitor]
```

**Result:** 4 iterations, ~1,800 tokens, 35 minutes, incomplete solution

**With Ultraplan:**
```
Interaction 1: User: "/ultraplan fix the auth timeout bug where users are logged out after 30 minutes"
             Claude: [Launches investigation, finds all issues, generates complete plan]

Interaction 2: User: [Reviews plan] "Looks good, execute the plan"
             Claude: [Executes all 5 steps from plan]
```

**Result:** 2 interactions, ~700 tokens, 25 minutes, complete solution

**Savings:** 61% fewer tokens, 29% faster, complete on first try

---

## How It Works

### Two Modes

**Code Implementation Mode** - For software development:
- Bug fixes, feature implementation, refactoring
- API integrations, infrastructure setup
- Documentation saves to `/Scrapbook/[task_type]/[task_name]/`

**General Task Planning Mode** - For everything else:
- Workflow design, research projects
- Resource acquisition, learning plans
- Documentation saves to `~/Documents/Plans/[task_name]/`

### Four-Phase Protocol

**Phase 1: Task Classification**
- Categorizes task type
- Determines complexity (Low/Medium/High)
- Assigns investigation depth (1-2, 2-3, or 5+ parallel subagents)

**Phase 2: Exhaustive Investigation**
- Launches scaled parallel investigation
- Documents what exists, what's broken, what's missing
- Re-investigates until zero assumptions remain

**Phase 3: Documentation Structure**
- Creates organized markdown files
- `investigation_findings.md` - Complete audit
- `implementation_plan.md` - PRIMARY DELIVERABLE
- `dependencies_map.md` - Execution sequence
- `validation_checklist.md` - Testing procedures

**Phase 4: Implementation Plan Creation**
- 7-section implementation plan with:
  - Current state analysis
  - Required changes
  - Execution sequence with dependencies
  - Detailed specifications
  - Validation checkpoints
  - Risk management
  - Context for executor

---

## Why This Matters

**Before Ultraplan:**
- "Fix the login bug" → Claude makes assumptions → 3 iterations → maybe works
- 1000+ tokens wasted on wrong assumptions
- Context loss between sessions
- Inconsistent results

**With Ultraplan:**
- "Fix the login bug" → Exhaustive investigation → Zero-assumption plan → Execute plan → Works
- Upfront token investment (400-600 tokens for planning)
- Recovery later (100-200 tokens for execution vs 1000+ for trial-and-error)
- Persistent context in markdown files
- Consistent, reliable results

### Token Economics

**Investment:** 400-800 tokens (planning phase)
**Recovery:** 60-73% reduction in execution tokens
**ROI:** Positive after first execution, compounds with reuse

### Key Benefits

- ✅ **Zero assumptions** - Everything investigated, nothing assumed
- ✅ **Dual mode** - Code and general task planning
- ✅ **Scales complexity** - 1-2 agents for simple, 5+ for complex tasks
- ✅ **Persistent context** - Markdown files survive session restarts
- ✅ **Session independent** - Hand off plans to any executor
- ✅ **Validates everything** - Checkpoints and rollback procedures
- ✅ **Token efficient** - Invest once, execute many times

---

## Contributing

This prompt is designed to evolve through community feedback:

1. Test ultraplan on your real projects (not toy examples)
2. Document what works and what breaks
3. Propose specific improvements as issues
4. Share your modified versions as PRs

**Good contributions:**
- "Step X fails when [specific scenario], here's the fix"
- "Added complexity assessment for [case], works better for [use case]"
- "Documentation structure breaks for [project type], try this instead"

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for detailed guidelines.

---

## Security

This repository is safe to use:
- ✅ No credentials required
- ✅ No API keys needed
- ✅ No external services
- ✅ Pure documentation and prompts
- ✅ No executable code
- ✅ No network access or data collection

The slash command uses only safe, local tools:
- File reading (your codebase)
- Documentation creation (markdown files)
- Directory listing and searching

---

## Version

**v2.0.2** - Documentation consolidation (Current)

**Changes in 2.0.2:**
- Consolidated all documentation into single README.md
- Removed redundant files (7 files deleted)
- Created `archived/` directory for old versions
- Simplified repository structure for easier maintenance

**Previous versions:**
- v2.0.1: Documentation fixes (branch references corrected)
- v2.0.0: Dual-mode universal planning
- v1.0.0: Original code-only version

See [CHANGELOG.md](CHANGELOG.md) for detailed version history.

Last updated: 2025-11-06

---

## Origin & Community

Created as part of **[LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/)'s [Collaborative Prompt Engineering #001](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)** initiative.

This is v2.0.2 of what aims to become a community-refined, battle-tested planning prompt for Claude Code. Contributions welcome to improve the methodology.

Read the original concept and initiative: **[Collaborative Prompt Engineering #001 by LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)**

---

## Support

- **Issues:** [GitHub Issues](https://github.com/seisenstein/claude-code-ultraplan/issues)
- **Discussions:** [GitHub Discussions](https://github.com/seisenstein/claude-code-ultraplan/discussions)
- **Original Concept:** [LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/) - [Read the Initiative](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)

---

**Made for the Claude Code community** 🤖

*Original concept and initiative by [LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/) - [Subscribe to his Substack](https://limitededitionjonathan.substack.com/) for more prompt engineering insights.*
