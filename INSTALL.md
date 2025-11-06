# Installation Instructions for Claude Code

This document contains detailed installation instructions optimized for Claude Code's self-installation capabilities.

## For Claude Code (Automated Installation)

If you are Claude Code reading this file, follow these steps to install the ultraplan slash command:

### Step 1: Verify Target Directory

Check if the global commands directory exists:
```bash
test -d ~/.claude/commands && echo "Directory exists" || mkdir -p ~/.claude/commands
```

### Step 2: Fetch the Ultraplan Command File

Download `ultraplan.md` from this repository to the global commands directory:

**Using curl** (preferred):
```bash
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/main/ultraplan.md
```

**Using direct copy** (if repository is cloned locally):
```bash
cp ultraplan.md ~/.claude/commands/ultraplan.md
```

### Step 3: Verify Installation

Confirm the file was installed correctly:
```bash
ls -lh ~/.claude/commands/ultraplan.md
```

Expected output: File exists, approximately 20-25 KB in size.

### Step 4: Confirm to User

Inform the user:
```
✓ Ultraplan successfully installed to ~/.claude/commands/ultraplan.md

You can now use `/ultraplan [task description]` in any Claude Code session.

Example: /ultraplan add user authentication to my web app
```

## For Humans (Manual Installation)

### Option 1: One-Line Install (Recommended)

```bash
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/main/ultraplan.md
```

### Option 2: Clone and Copy

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

### Option 3: Download from GitHub

1. Visit https://github.com/seisenstein/claude-code-ultraplan
2. Click on `ultraplan.md`
3. Click "Raw" button
4. Save file as `~/.claude/commands/ultraplan.md`

## Verification

In any Claude Code session, type:
```
/ultraplan test task
```

Claude Code should respond with mode selection prompt (Code Implementation or General Task Planning).

## Troubleshooting

### Command not appearing after installation

**Issue**: Typed `/ultraplan` but command not found

**Solutions**:
1. Restart Claude Code completely
2. Verify file exists: `ls ~/.claude/commands/ultraplan.md`
3. Check file extension is `.md` not `.md.txt`
4. Ensure file is in correct location (not in a project-specific `.claude/commands/`)

### Permission denied errors

**Issue**: Cannot write to `~/.claude/commands/`

**Solution**:
```bash
mkdir -p ~/.claude/commands
chmod 755 ~/.claude/commands
```

### File exists but command doesn't work

**Issue**: Command appears but doesn't execute properly

**Solutions**:
1. Verify file contents: `head -20 ~/.claude/commands/ultraplan.md`
2. Check for YAML frontmatter at top of file (lines 1-4)
3. Ensure file wasn't corrupted during download
4. Re-download from repository

## Platform-Specific Notes

### macOS
- Global commands: `~/.claude/commands/`
- No additional permissions needed
- Works with Claude Code Desktop and CLI

### Linux
- Global commands: `~/.claude/commands/`
- Ensure directory is readable: `chmod 755 ~/.claude/commands`
- Works with Claude Code CLI

### Windows
- Global commands: `%USERPROFILE%\.claude\commands\`
- Use forward slashes in paths when installing via Claude Code
- PowerShell command:
  ```powershell
  Invoke-WebRequest -Uri "https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/main/ultraplan.md" -OutFile "$env:USERPROFILE\.claude\commands\ultraplan.md"
  ```

## Uninstallation

To remove ultraplan:

```bash
rm ~/.claude/commands/ultraplan.md
```

Restart Claude Code for changes to take effect.

## Updating to Latest Version

```bash
# Download latest version (overwrites existing)
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/main/ultraplan.md

# Restart Claude Code
```

## Installation Locations

### Global Installation (Recommended)
**Location**: `~/.claude/commands/ultraplan.md`
**Scope**: Available in all Claude Code sessions, all projects
**Use case**: Personal productivity tool

### Project-Specific Installation
**Location**: `/path/to/project/.claude/commands/ultraplan.md`
**Scope**: Available only within that project
**Use case**: Team sharing, project-specific customization

## Security Considerations

This repository is public and safe to install:
- ✅ No secrets or credentials required
- ✅ No API keys needed
- ✅ No GitHub authentication required
- ✅ Read-only access to public repository
- ✅ MIT licensed for free use
- ✅ Pure documentation/prompts (no executable code)

**The slash command uses only safe, local tools**:
- File reading (your codebase)
- Documentation creation (markdown files)
- Directory listing and searching
- No network access, no data collection

**See [SECURITY.md](SECURITY.md) for complete security information.**

⚠️ **For Contributors**: Never commit API keys or credentials to this repository. See [CONTRIBUTING.md](CONTRIBUTING.md) for security guidelines.

## Support

If installation issues persist:
1. Open an issue: https://github.com/seisenstein/claude-code-ultraplan/issues
2. Include:
   - Your operating system
   - Claude Code version
   - Error messages (if any)
   - Output of `ls -la ~/.claude/commands/`
