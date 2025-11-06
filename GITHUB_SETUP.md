# GitHub Setup Instructions

This file contains step-by-step instructions to create your public GitHub repository for the Ultraplan slash command.

## Prerequisites

- GitHub account
- Git installed locally (✅ already done)
- Repository initialized locally (✅ already done at `/Users/sean/claude-code-ultraplan`)

## Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Configure repository:
   - **Repository name**: `claude-code-ultraplan`
   - **Description**: "Universal Implementation Plan Generator for Claude Code - Zero-assumption planning for code and general tasks"
   - **Visibility**: ✅ **Public** (important for community sharing)
   - **Initialize repository**: ❌ **DO NOT** check any boxes (README, .gitignore, license)
     - We already have these files locally

3. Click "Create repository"

## Step 2: Connect Local Repository to GitHub

GitHub will show you commands. Use these (replace `[YOUR_USERNAME]` with your actual GitHub username):

```bash
cd ~/claude-code-ultraplan

# Add GitHub remote
git remote add origin https://github.com/[YOUR_USERNAME]/claude-code-ultraplan.git

# Rename branch to main (modern convention)
git branch -M main

# Push to GitHub
git push -u origin main
```

**Example** (if your username is `jsmith`):
```bash
git remote add origin https://github.com/jsmith/claude-code-ultraplan.git
git branch -M main
git push -u origin main
```

## Step 3: Verify Repository

1. Visit `https://github.com/[YOUR_USERNAME]/claude-code-ultraplan`
2. You should see:
   - ✅ README.md displaying properly
   - ✅ All 9 files present
   - ✅ MIT license badge
   - ✅ Initial commit message

## Step 4: Update README with Your Username

The README contains placeholder `seisenstein`. Update it:

```bash
cd ~/claude-code-ultraplan

# Replace seisenstein with your actual username throughout all files
sed -i '' 's/\[USERNAME\]/YOUR_GITHUB_USERNAME/g' README.md
sed -i '' 's/\[USERNAME\]/YOUR_GITHUB_USERNAME/g' INSTALL.md
sed -i '' 's/\[USERNAME\]/YOUR_GITHUB_USERNAME/g' CONTRIBUTING.md
sed -i '' 's/\[USERNAME\]/YOUR_GITHUB_USERNAME/g' EXAMPLES.md

# Or manually edit files to replace seisenstein with your username

# Commit changes
git add -A
git commit -m "docs: update repository URLs with actual username"
git push
```

## Step 5: Configure Repository Settings

### Enable Discussions (Optional but Recommended)

1. Go to repository Settings
2. Scroll to "Features"
3. Check ✅ "Discussions"
4. This allows community questions and feedback

### Add Topics (Recommended)

1. Click "⚙️" next to "About" on repository homepage
2. Add topics:
   - `claude-code`
   - `prompt-engineering`
   - `ai-tools`
   - `developer-tools`
   - `automation`
   - `planning`
   - `slash-commands`

3. Save changes

### Repository Description

In the same "About" section, ensure description is:
```
Universal Implementation Plan Generator for Claude Code - Zero-assumption planning for code and general tasks
```

### Website (Optional)

If you write a blog post about this, add the URL in the "Website" field.

## Step 6: Verify Self-Installation

Test that Claude Code can self-install from your repository:

### Test with Claude Code

In a fresh Claude Code session:
```
Install the ultraplan slash command from https://github.com/[YOUR_USERNAME]/claude-code-ultraplan to my global Claude Code commands directory
```

Claude Code should:
1. Read the repository
2. Fetch `ultraplan.md`
3. Install to `~/.claude/commands/ultraplan.md`
4. Confirm installation

### Verify manually

```bash
ls -lh ~/.claude/commands/ultraplan.md
# Should show file exists (~20-25 KB)

# Test the command
# In Claude Code: /ultraplan test task
```

## Step 7: Share with Community

### Option 1: Share on Social Media

Example post:
```
🚀 Just released Ultraplan v1.0 - Universal Implementation Plan Generator for Claude Code

Turns vague tasks into bulletproof, executable plans through exhaustive investigation.

✅ Zero assumptions
✅ 60-73% token reduction
✅ Code + general task modes
✅ Persistent documentation

Open source, MIT licensed!
https://github.com/[YOUR_USERNAME]/claude-code-ultraplan

Part of @LimitedEditionJonathan's Collaborative Prompt Engineering #001 initiative.

#ClaudeCode #AI #DeveloperTools #PromptEngineering
```

### Option 2: Submit to Awesome Lists

Consider submitting to:
- Awesome Claude Code repositories
- Awesome AI Tools lists
- Prompt Engineering communities

### Option 3: Create Blog Post

Write about:
- Why you created this
- How it improves your workflow
- Real-world examples from your usage
- Token savings and efficiency gains
- Link to the GitHub repository

### Option 4: Forum Posts

Share in:
- Claude community forums
- Reddit (r/ClaudeAI, r/programming, r/coding)
- Hacker News
- Dev.to
- Hashnode

## Step 8: Community Maintenance

### Enable Issue Templates

Create `.github/ISSUE_TEMPLATE/bug_report.md` and `feature_request.md`:

```bash
cd ~/claude-code-ultraplan
mkdir -p .github/ISSUE_TEMPLATE

# Bug report template
cat > .github/ISSUE_TEMPLATE/bug_report.md << 'EOF'
---
name: Bug Report
about: Report a problem with ultraplan
title: "[BUG] "
labels: bug
assignees: ''
---

**Describe the bug**
A clear description of what the bug is.

**Task you ran**
```
/ultraplan [your task description]
```

**Expected behavior**
What you expected to happen.

**Actual behavior**
What actually happened.

**Environment**
- OS: [e.g., macOS 14.0]
- Claude Code version: [e.g., 1.2.0]

**Additional context**
Attach investigation_findings.md if relevant.
EOF

# Feature request template
cat > .github/ISSUE_TEMPLATE/feature_request.md << 'EOF'
---
name: Feature Request
about: Suggest an improvement
title: "[FEATURE] "
labels: enhancement
assignees: ''
---

**Is your feature request related to a problem?**
A clear description of what the problem is.

**Describe the solution you'd like**
What you want to happen.

**Describe alternatives you've considered**
Other approaches you've thought about.

**Additional context**
Any other context about the feature request.
EOF

git add .github/
git commit -m "chore: add issue templates"
git push
```

### Monitor and Respond

- Check issues and discussions regularly
- Respond to bug reports within 3-5 days
- Consider PRs for improvements
- Update CHANGELOG.md for each release

### Version Releases

When making improvements:

```bash
# Update CHANGELOG.md
# Update version in README.md

git add -A
git commit -m "chore: release v1.1.0"
git tag v1.1.0
git push origin main --tags
```

Create GitHub release:
1. Go to repository → Releases → "Create a new release"
2. Select tag v1.1.0
3. Title: "v1.1.0 - [Brief description]"
4. Copy relevant CHANGELOG section into description
5. Publish release

## Security Considerations

### Your GitHub Account is Secure

✅ **This repository is public but safe**:
- No credentials or secrets in code
- No API keys required
- No authentication needed
- Read-only access for users
- Pure markdown and documentation

✅ **Open source benefits**:
- Community can inspect code
- Contributions improve quality
- Transparency builds trust
- MIT license allows free use

✅ **Your account remains protected**:
- Users only read public files
- No write access to your repository
- Standard GitHub security applies

### What NOT to Add

❌ Never commit:
- Personal API keys
- Credentials or passwords
- Private information
- `.env` files with secrets

## Troubleshooting

### "Permission denied" when pushing

**Solution**: Setup SSH key or use GitHub CLI
```bash
# Option 1: GitHub CLI (easiest)
brew install gh
gh auth login
# Follow prompts

# Option 2: HTTPS with token
# Use personal access token instead of password
```

### "Branch 'main' doesn't exist"

**Solution**: You're on 'master', rename to 'main':
```bash
git branch -M main
git push -u origin main
```

### "Remote already exists"

**Solution**: Update remote URL:
```bash
git remote set-url origin https://github.com/[YOUR_USERNAME]/claude-code-ultraplan.git
```

## Next Steps

1. ✅ Create GitHub repository (public)
2. ✅ Push local code to GitHub
3. ✅ Update README with your username
4. ✅ Configure repository settings
5. ✅ Test self-installation
6. ✅ Share with community
7. ✅ Setup issue templates
8. ✅ Monitor and maintain

## Support

If you encounter issues:
1. Check this guide again
2. Review GitHub's documentation: https://docs.github.com
3. Ask in GitHub Discussions (after repository is created)

---

**Ready?** Follow steps 1-7 above to publish your ultraplan repository! 🚀
