# One-Time Use Guide

Use ultraplan for a single task without permanent installation.

---

## When to Use This Approach

✅ **Perfect for**:
- Testing ultraplan before committing to installation
- One-off planning task
- Want to see how it works first
- Don't need `/ultraplan` in future sessions
- Quick trial run

## When to Install Permanently Instead

If you'll use ultraplan regularly, consider permanent installation:
- Adds `/ultraplan` shorthand to all Claude Code sessions
- No need to re-clone or reference the file
- Faster workflow for repeated use

**See [INSTALL.md](INSTALL.md) for permanent installation.**

---

## Quick Start (One-Time Use)

### Step 1: Get the Repository

```bash
git clone https://github.com/seisenstein/claude-code-ultraplan.git
cd claude-code-ultraplan
```

This downloads the repository and enters the directory containing `ultraplan.md`.

### Step 2: Tell Claude Code to Use the Prompt

In your Claude Code session, give this instruction:

```
Read ultraplan.md from the current directory and apply its planning protocol to this task:

[describe your task here]
```

**Example for code task**:
```
Read ultraplan.md and apply its planning protocol to this task:
add user authentication with OAuth 2.0 to my Express.js app
```

**Example for general task**:
```
Read ultraplan.md and apply its planning protocol to this task:
create an onboarding workflow for new team members
```

### Step 3: Select Mode

Claude Code will read the prompt and ask you to select:
1. **Code Implementation Mode** - For software development tasks
2. **General Task Planning Mode** - For everything else

Choose the appropriate mode for your task.

### Step 4: Wait for Planning Phase

Claude Code will:
1. Classify your task and determine complexity
2. Launch parallel investigation subagents (scaled to complexity)
3. Conduct exhaustive investigation with zero assumptions
4. Generate comprehensive documentation
5. Create implementation plan

This takes 2-25 minutes depending on complexity.

### Step 5: Review Generated Plans

Find your plans in:
- **Code tasks**: `/Scrapbook/[task_type]/[task_name]/`
- **General tasks**: `~/Documents/Plans/[task_name]/`

Files generated:
- `investigation_findings.md` - Complete audit results
- `implementation_plan.md` ⭐ - Your execution blueprint
- `dependencies_map.md` - Execution sequence
- `validation_checklist.md` - Testing procedures
- Plus mode-specific files

### Step 6: Execute the Plan (Separate Session)

**Best practice**: Execute in a fresh Claude Code session

```
Read and execute the implementation plan at /Scrapbook/[task_type]/[task_name]/implementation_plan.md
```

Claude Code will follow the plan step-by-step with zero-assumption clarity.

---

## How One-Time Use Works

**Behind the scenes**:
1. Claude Code reads `ultraplan.md` as instructions
2. Understands it as a planning protocol
3. Applies the 4-phase methodology to your task
4. Uses allowed tools (Read, Write, Glob, Grep, Task, etc.)
5. Generates persistent markdown documentation

**Key difference from permanent installation**:
- You specify the file path each time: `Read ultraplan.md and...`
- With permanent install: Just type `/ultraplan [task]`

---

## Tips for One-Time Use

### Make It Easier

After cloning once, bookmark your terminal session in that directory. Then you can:
```bash
cd ~/claude-code-ultraplan
```

And use ultraplan without re-cloning.

### When to Upgrade to Permanent

If you find yourself using ultraplan more than 2-3 times, consider installing permanently:
```bash
# From the claude-code-ultraplan directory
cp ultraplan.md ~/.claude/commands/
```

Restart Claude Code, and you'll have `/ultraplan` available everywhere.

See [INSTALL.md](INSTALL.md) for detailed installation instructions.

### Reusing Generated Plans

The plans ultraplan generates are reusable:
- Save plans for similar future projects
- Share with team members
- Reference for documentation
- Templates for common patterns

---

## Troubleshooting One-Time Use

### "Claude Code can't find ultraplan.md"

**Solution**: Ensure you're in the repository directory
```bash
pwd  # Should show: /Users/yourname/claude-code-ultraplan (or similar)
ls ultraplan.md  # Should show the file exists
```

### "Claude Code doesn't recognize the prompt"

**Solution**: Be explicit in your instruction
```
Read the file ultraplan.md in the current directory. This file contains a planning protocol. Apply this protocol to plan the following task: [your task]
```

### "Mode selection doesn't appear"

**Solution**: The YAML frontmatter mentions `AskUserQuestion`. If mode selection doesn't appear, manually specify:
```
Read ultraplan.md and apply Code Implementation Mode to this task: [your task]
```

Or:
```
Read ultraplan.md and apply General Task Planning Mode to this task: [your task]
```

### "Investigation phase seems stuck"

This is normal - investigation can take time:
- Low complexity: 2-5 minutes
- Medium complexity: 5-12 minutes
- High complexity: 12-25 minutes

Multiple subagents are working in parallel. Wait for completion.

---

## Comparing One-Time vs Permanent

| Aspect | One-Time Use | Permanent Install |
|--------|-------------|-------------------|
| **Setup** | Git clone only | Git clone + install |
| **Usage** | `Read ultraplan.md and...` | `/ultraplan [task]` |
| **Availability** | When in repo directory | All Claude Code sessions |
| **Updates** | Git pull latest | Re-install after update |
| **Best for** | Testing, one-off tasks | Regular workflow |

---

## Next Steps

### After Trying One-Time

1. **Review the generated plan** - See if it meets your needs
2. **Execute the plan** - Test the implementation approach
3. **Decide**: Install permanently or continue one-time use
4. **Share feedback** - Open issues or discussions on GitHub

### Want to Install Permanently?

See [INSTALL.md](INSTALL.md) for:
- Self-installation via Claude Code
- Manual installation steps
- Platform-specific instructions
- Troubleshooting guide

### Want to Learn More?

- [USAGE.md](USAGE.md) - Complete usage guide
- [EXAMPLES.md](EXAMPLES.md) - Real-world examples
- [CONTRIBUTING.md](CONTRIBUTING.md) - How to improve ultraplan

---

## Support

- **Issues**: [GitHub Issues](https://github.com/seisenstein/claude-code-ultraplan/issues)
- **Discussions**: [GitHub Discussions](https://github.com/seisenstein/claude-code-ultraplan/discussions)
- **Security**: [SECURITY.md](SECURITY.md)

---

**Remember**: One-time use is perfect for testing. If you use it regularly, install permanently for better workflow! 🚀
