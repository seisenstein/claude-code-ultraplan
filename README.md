# Claude Code Ultraplan - Universal Implementation Plan Generator

**Zero-assumption planning for code implementations and general tasks**

Transform vague tasks into bulletproof, executable implementation plans. This slash command forces exhaustive investigation before planning, preventing assumptions that lead to failed implementations.

> 🎯 **Part of [Collaborative Prompt Engineering #001](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)** by [LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/) - A community initiative to build and refine the definitive implementation planning prompt for Claude Code.

## What This Does

Ultraplan turns "fix this bug" or "add this feature" into comprehensive, executable plans through:
- **Dual-mode operation**: Code implementation mode + General task planning mode
- **Exhaustive investigation**: Parallel subagents audit your codebase/requirements
- **Zero assumptions**: Every ambiguity resolved through investigation
- **Persistent documentation**: Markdown files preserve context across sessions
- **Token efficiency**: Invest upfront in investigation, recover in execution

## Quick Start

### Choose Your Use Case

**🔹 Option 1: Try It Once** (No installation)
- Perfect for: Testing, one-off tasks, seeing how it works first
- Takes: 2 minutes to start
- **[→ One-Time Use Guide](ONE_TIME_USE.md)**

**🔹 Option 2: Install as Slash Command** (Permanent)
- Perfect for: Regular use, want `/ultraplan` in all sessions, committed workflow
- Takes: 3 minutes to install
- **[→ Installation Guide](INSTALL.md)**

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

**[→ Complete One-Time Use Guide](ONE_TIME_USE.md)**

---

### Option 2: Install Permanently

#### For Claude Code (Self-Installation)

Give Claude Code this exact instruction:

```
Clone https://github.com/seisenstein/claude-code-ultraplan.git and install the ultraplan slash command to my global Claude Code commands directory (~/.claude/commands/)
```

Or step-by-step:

```bash
git clone https://github.com/seisenstein/claude-code-ultraplan.git
cd claude-code-ultraplan
```

Then tell Claude Code:
```
Install the ultraplan.md file from this directory to ~/.claude/commands/ultraplan.md
```

#### Manual Installation

```bash
# Create commands directory if needed
mkdir -p ~/.claude/commands

# Download and install
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/master/ultraplan.md

# Verify installation
ls ~/.claude/commands/ultraplan.md
```

#### Verify It Works

Restart Claude Code, then in any session:
```
/ultraplan create a new authentication system
```

Claude Code will ask you to select a mode (Code Implementation or General Task Planning) and begin the planning process.

**[→ Complete Installation Guide](INSTALL.md)**

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

## Example Output

After running `/ultraplan add user authentication to my app`, you'll get:

```
/Scrapbook/New_Feature_Implementation/user_authentication/
├── investigation_findings.md
├── implementation_plan.md      ← Your execution blueprint
├── dependencies_map.md
├── validation_checklist.md
├── testing_strategy.md
└── rollback_plan.md
```

The `implementation_plan.md` contains step-by-step instructions that you (or another Claude Code session) can execute without additional research.

## Why This Matters

**Before Ultraplan**:
- "Fix the login bug" → Claude makes assumptions → 3 iterations → maybe works
- 1000+ tokens wasted on wrong assumptions
- Context loss between sessions
- Inconsistent results

**With Ultraplan**:
- "Fix the login bug" → Exhaustive investigation → Zero-assumption plan → Execute plan → Works
- Upfront token investment (400-600 tokens for planning)
- Recovery later (100-200 tokens for execution vs 1000+ for trial-and-error)
- Persistent context in markdown files
- Consistent, reliable results

## Token Economics

**Investment**: 400-800 tokens (planning phase)
**Recovery**: 60-73% reduction in execution tokens
**ROI**: Positive after first execution, compounds with reuse

## Use Cases

### Code Development
- "Implement OAuth 2.0 authentication"
- "Refactor the payment processing module"
- "Debug production error in user service"
- "Integrate Stripe API for subscriptions"

### General Tasks
- "Design onboarding workflow for new team members"
- "Plan research project on competitor analysis"
- "Create content calendar for Q1 marketing"
- "Setup development environment for new laptop"

## Key Features

- ✅ **Zero assumptions** - Everything investigated, nothing assumed
- ✅ **Dual mode** - Code and general task planning
- ✅ **Scales complexity** - 1-2 agents for simple, 5+ for complex tasks
- ✅ **Persistent context** - Markdown files survive session restarts
- ✅ **Session independent** - Hand off plans to any executor
- ✅ **Validates everything** - Checkpoints and rollback procedures
- ✅ **Token efficient** - Invest once, execute many times

## Documentation

See [`USAGE.md`](USAGE.md) for detailed usage guide and examples.

See [`EXAMPLES.md`](EXAMPLES.md) for real-world scenarios and outputs.

## Origin & Community

Created as part of **[LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/)'s [Collaborative Prompt Engineering #001](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)** initiative.

This is v1.0 of what aims to become a community-refined, battle-tested planning prompt for Claude Code. Contributions welcome to improve the methodology.

Read the original concept and initiative: **[Collaborative Prompt Engineering #001 by LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)**

## Contributing

This prompt is designed to evolve through community feedback:

1. Test ultraplan on your real projects (not toy examples)
2. Document what works and what breaks
3. Propose specific improvements as issues
4. Share your modified versions as PRs

Good contributions:
- "Step X fails when [specific scenario], here's the fix"
- "Added complexity assessment for [case], works better for [use case]"
- "Documentation structure breaks for [project type], try this instead"

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for detailed guidelines.

## Security

This repository is safe to use:
- No credentials required
- No API keys needed
- No external services
- Pure documentation and prompts

**See [SECURITY.md](SECURITY.md) for**:
- Security best practices
- Contributing securely (never commit API keys!)
- Privacy information
- Threat model

## License

MIT License - Use freely, modify as needed, share improvements back.

## Version

**v2.0.0** - Dual-mode universal planning (Current)
- Code Implementation Mode + General Task Planning Mode
- See [ULTRAPLAN_CHANGELOG.md](ULTRAPLAN_CHANGELOG.md) for detailed version comparison
- See [v1.0.0-original.md](v1.0.0-original.md) for code-only version

Last updated: 2025-11-05

## Support

- **Issues**: [GitHub Issues](https://github.com/seisenstein/claude-code-ultraplan/issues)
- **Discussions**: [GitHub Discussions](https://github.com/seisenstein/claude-code-ultraplan/discussions)
- **Original Concept**: [LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/) - [Read the Initiative](https://limitededitionjonathan.substack.com/p/collaborative-prompt-engineering)

---

**Made for the Claude Code community** 🤖

*Original concept and initiative by [LIMITED EDITION JONATHAN](https://limitededitionjonathan.substack.com/) - [Subscribe to his Substack](https://limitededitionjonathan.substack.com/) for more prompt engineering insights.*
