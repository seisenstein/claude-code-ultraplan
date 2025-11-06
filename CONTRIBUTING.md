# Contributing to Ultraplan

Thank you for your interest in improving the Universal Implementation Plan Generator!

This project is part of the **Collaborative Prompt Engineering #001** initiative, where the prompt evolves through community feedback and real-world testing.

## Philosophy

We're building the definitive implementation planning prompt for Claude Code through:
- Real production testing (not toy examples)
- Concrete, measurable improvements
- Community-driven iteration
- Battle-tested refinements

## Types of Contributions

### 1. Bug Reports & Issues

**Found a problem?** Open an issue with:

```markdown
### Issue Type
- [ ] Ultraplan fails to investigate properly
- [ ] Generated plan has errors
- [ ] Documentation unclear
- [ ] Installation problem

### Environment
- OS: macOS / Linux / Windows
- Claude Code version:
- Ultraplan version:

### Task Description
[What you asked ultraplan to do]

### Expected Behavior
[What should have happened]

### Actual Behavior
[What actually happened]

### Investigation Findings
[Attach investigation_findings.md or relevant excerpts]

### Generated Plan Issues
[Specific problems with implementation_plan.md]

### Steps to Reproduce
1. Run `/ultraplan [task]`
2. Select [mode]
3. Observe [problem]
```

### 2. Prompt Improvements

**Found a way to improve the prompt?**

Before submitting:
1. Test on at least 2-3 real projects (not toy examples)
2. Document before/after metrics (token usage, accuracy, completeness)
3. Ensure improvement doesn't break existing functionality

**Submit as PR with**:
- Specific change to `ultraplan.md`
- Rationale for change
- Test results showing improvement
- Any breaking changes noted

### 3. Documentation Improvements

**Found unclear docs?** PRs welcome for:
- Typo fixes
- Clarity improvements
- Additional examples
- Better explanations
- Usage tips

### 4. New Features

**Have an idea?** Open a discussion first:
- Describe the feature
- Explain the use case
- Propose implementation approach
- Discuss with maintainers before coding

## What Makes a Good Contribution

### ✅ Excellent Contributions

**Example 1: Specific Fix**
> "Phase 2 investigation fails when codebase has no tests. Modified line 127 to check for test directory existence first. Tested on 5 projects without tests—works correctly now."

**Example 2: Measured Improvement**
> "Modified complexity classification to include cyclomatic complexity check. Reduces misclassification by 23% (tested on 30 projects). Before: 7 misclassified. After: 2 misclassified."

**Example 3: Documentation Enhancement**
> "Added troubleshooting section for 'plan has open questions' error. Based on 15 user reports in discussions. Includes 3 real examples and fixes."

### ❌ Less Useful Contributions

- "Make it better" (not specific)
- "Seems cool" (no actionable feedback)
- Untested changes
- Generic suggestions without context
- Changes that break existing functionality
- Prompt modifications without testing

## Testing Requirements

All prompt changes must be tested on:

### Minimum Testing (Required)
- ✅ 2+ real projects (not toy examples)
- ✅ Both modes (Code Implementation + General Task Planning)
- ✅ Different complexity levels (Low, Medium, High)
- ✅ Verify all 6 deliverable files generate correctly

### Comprehensive Testing (Recommended)
- ✅ 5+ real projects across different domains
- ✅ Edge cases (empty repos, massive codebases, unclear tasks)
- ✅ Token usage comparison (before/after your change)
- ✅ Plan executability (can Claude Code execute the generated plan?)
- ✅ Cross-session handoff (can a new Claude instance execute the plan?)

## Contribution Process

### 1. Fork and Clone

```bash
git clone https://github.com/YOUR_USERNAME/claude-code-ultraplan.git
cd claude-code-ultraplan
```

### 2. Create Feature Branch

```bash
git checkout -b fix/investigation-timeout
# or
git checkout -b feat/complexity-assessment-improvement
# or
git checkout -b docs/usage-examples
```

### 3. Make Changes

Edit `ultraplan.md` or documentation files.

### 4. Test Thoroughly

Install your modified version:
```bash
cp ultraplan.md ~/.claude/commands/ultraplan.md
```

Test on real projects:
```
/ultraplan [real task from real project]
```

Document results:
- What improved?
- What broke (if anything)?
- Token usage before/after
- Time to completion
- Plan quality assessment

### 5. Commit with Descriptive Message

```bash
git add ultraplan.md
git commit -m "fix: handle codebases with no test directory

- Check for test directory existence before analyzing tests
- Prevents investigation phase failure on projects without tests
- Tested on 5 projects (3 without tests, 2 with tests)
- No breaking changes to existing functionality"
```

### 6. Push and Open PR

```bash
git push origin fix/investigation-timeout
```

Open PR on GitHub with:

```markdown
## Summary
[What does this PR do?]

## Motivation
[Why is this change needed?]

## Changes
- [Specific change 1]
- [Specific change 2]

## Testing
Tested on:
- Project 1: [type], [complexity], [result]
- Project 2: [type], [complexity], [result]
- Project 3: [type], [complexity], [result]

### Metrics
- Token usage: [before] → [after] ([% change])
- Plan quality: [before score] → [after score]
- Investigation time: [before] → [after]

## Breaking Changes
- [ ] None
- [ ] Yes (describe below)

[If breaking changes, explain migration path]

## Checklist
- [ ] Tested on 2+ real projects
- [ ] Both modes tested
- [ ] Documentation updated
- [ ] No breaking changes (or migration guide provided)
- [ ] Commit messages are clear
```

## Code Review Process

Maintainers will:
1. Review code changes (usually within 3-5 days)
2. Ask questions or request changes
3. Test changes independently
4. Merge if approved

### Review Criteria

- ✅ Solves real problem (not theoretical)
- ✅ Tested on multiple projects
- ✅ Doesn't break existing functionality
- ✅ Documentation updated
- ✅ Clear commit messages
- ✅ Rationale explained

## Community Standards

### Be Specific

❌ "This doesn't work"
✅ "Phase 2 investigation fails with error 'cannot read property' when codebase has no package.json"

### Show Your Work

❌ "Tried this, seems better"
✅ "Modified line 127, tested on 5 projects, token usage reduced by 15%"

### Focus on Real Use Cases

❌ "What if someone wants to plan a Mars mission?"
✅ "In my production app with 50k LOC, investigation phase times out"

### Be Constructive

❌ "This prompt is terrible"
✅ "Found issue with X, here's how to fix it, tested successfully"

## Prompt Engineering Best Practices

When modifying `ultraplan.md`:

### 1. Maintain Structure
Don't break the 4-phase protocol structure. Modifications should fit within existing phases.

### 2. Keep Zero-Assumption Philosophy
Any changes must maintain the zero-assumption investigation approach.

### 3. Preserve Token Economics
Changes should improve or maintain token efficiency (upfront investment, long-term recovery).

### 4. Ensure Session Independence
Generated plans must work in fresh Claude Code sessions without context from planning session.

### 5. Test Cross-Complexity
Ensure changes work for Low, Medium, and High complexity tasks.

## Recognition

Contributors are recognized in:
- `CHANGELOG.md` for each release
- GitHub contributors page
- Special callouts for significant improvements

Significant contributors may be invited to:
- Maintainer discussions
- Early testing of major changes
- Community leadership roles

## Questions?

- **General questions**: [GitHub Discussions](https://github.com/[USERNAME]/claude-code-ultraplan/discussions)
- **Bug reports**: [GitHub Issues](https://github.com/[USERNAME]/claude-code-ultraplan/issues)
- **Security issues**: Email [maintainer email]

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

## Thank You!

Every contribution makes ultraplan better for the entire Claude Code community. Whether it's a typo fix, a major improvement, or a bug report—thank you for helping build better tools together.

---

**Let's build the definitive planning prompt for Claude Code** 🤖
