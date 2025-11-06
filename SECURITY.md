# Security Policy

This document outlines security considerations for using and contributing to Claude Code Ultraplan.

---

## Repository Security

### This Repository is Safe to Use

✅ **No credentials required** - This is a pure documentation/prompt repository
✅ **No API keys needed** - The slash command uses only local Claude Code tools
✅ **No external services** - No network calls, no data collection
✅ **Read-only by default** - Users clone and read files only
✅ **MIT Licensed** - Open source, transparent, auditable

### What This Repository Contains

- Markdown documentation files
- Slash command prompt (`ultraplan.md`)
- Usage guides and examples
- No executable code requiring permissions
- No scripts that modify your system

---

## Using Ultraplan Safely

### Allowed Tools in ultraplan.md

The slash command is restricted to these safe tools only:

```yaml
allowed-tools: Task, Read, Write, Glob, Grep, Bash(mkdir:*), Bash(ls:*), Bash(test:*), AskUserQuestion
```

**What each tool does**:
- `Task` - Launches subagents for investigation (scoped to repository)
- `Read` - Reads files in your codebase (read-only)
- `Write` - Creates documentation files only (in `/Scrapbook/` or `~/Documents/Plans/`)
- `Glob` - Searches for files by pattern (read-only)
- `Grep` - Searches file contents (read-only)
- `Bash(mkdir:*)` - Creates directories only (limited scope)
- `Bash(ls:*)` - Lists directory contents (read-only)
- `Bash(test:*)` - Tests file existence (read-only)
- `AskUserQuestion` - Prompts user for input (interactive)

**Notably excluded** (for safety):
- ❌ Unrestricted `Bash` commands
- ❌ Network access tools (no data exfiltration)
- ❌ Code execution tools
- ❌ File deletion tools
- ❌ System modification tools

### What Ultraplan Does NOT Do

- ❌ Does not execute code (planning phase only)
- ❌ Does not connect to external services
- ❌ Does not access your credentials
- ❌ Does not modify existing code (only creates documentation)
- ❌ Does not send data to third parties
- ❌ Does not require any API keys or tokens

### Safe Usage Practices

**Do**:
- ✅ Review generated plans before executing them
- ✅ Use ultraplan for planning only (separate from execution)
- ✅ Keep credentials in `.env` files (already in `.gitignore`)
- ✅ Review output documentation before sharing
- ✅ Use on private repositories (nothing leaves your machine)

**Don't**:
- ❌ Include API keys in task descriptions
- ❌ Share generated plans containing sensitive data
- ❌ Execute plans without reviewing them first
- ❌ Assume documentation is safe to share publicly (review first)

---

## Contributing Securely

### ⚠️ CRITICAL: Never Commit Credentials

**Before submitting any contribution** (issue, PR, example):

#### Check for Credentials
```bash
# Search for potential API keys in your contribution
git grep -i "api[_-]key"
git grep -i "token"
git grep -i "secret"
git grep -i "password"
git grep "sk-" # OpenAI keys
git grep "ghp_" # GitHub tokens
git grep "gho_" # GitHub OAuth tokens
```

#### Common Credential Patterns to Avoid

❌ **Never commit**:
- API keys: `api_key = "sk-abc123xyz"`
- Access tokens: `token: "ghp_abc123xyz"`
- OAuth secrets: `client_secret: "abc123"`
- Database URLs: `DATABASE_URL=postgres://user:password@host/db`
- Private keys: `-----BEGIN PRIVATE KEY-----`
- Environment files: `.env`, `.env.local`, `config/secrets.yml`
- Authentication headers: `Authorization: Bearer xxx`
- Session tokens or cookies
- AWS credentials: `aws_access_key_id`, `aws_secret_access_key`
- Cloud service credentials (Azure, GCP, etc.)

#### Use Placeholders Instead

✅ **Safe examples**:
```bash
# Good - uses placeholders
api_key = "YOUR_API_KEY"
token = "xxx-xxx-xxx"
DATABASE_URL = "postgres://user:password@localhost/db"

# Good - explains without exposing
# To use this: Set OPENAI_API_KEY in your .env file

# Good - redacted screenshots
Authorization: Bearer [REDACTED]
```

### Sensitive Information in Examples

When contributing examples or screenshots:

❌ **Never include**:
- Your actual project names (use generic names)
- Real file paths that reveal personal info (`/Users/yourname/...`)
- Real API endpoints (use `https://api.example.com`)
- Real organization names in examples
- Personal email addresses
- Internal system names or IPs
- Production URLs or staging URLs

✅ **Safe alternatives**:
- Generic paths: `/path/to/project/`
- Example domains: `https://api.example.com`
- Placeholder names: `myapp`, `myproject`, `example-service`
- Mock emails: `user@example.com`
- Example IPs: `192.0.2.1` (TEST-NET-1)

### Tool Calls in Contributions

If your contribution includes example tool calls or command outputs:

⚠️ **Review for**:
- API tokens in command arguments
- Authentication headers in curl examples
- Credentials in configuration files
- Private repository URLs
- Internal system paths or hostnames

**Safe example**:
```markdown
❌ Unsafe:
curl -H "Authorization: Bearer sk-abc123" https://api.openai.com/v1/models

✅ Safe:
curl -H "Authorization: Bearer YOUR_API_KEY" https://api.openai.com/v1/models
```

### Accidentally Committed Credentials?

**Immediate Actions**:

1. **Revoke/Rotate the credential immediately**
   - Don't wait to "fix the commit first"
   - Assume the credential is compromised
   - Generate new credentials

2. **Contact repository maintainers**
   - Open a security issue (mark as private if GitHub supports it)
   - Email maintainers directly
   - Explain what was exposed

3. **Remove from git history** (if you have permissions):
   ```bash
   # WARNING: This rewrites history - coordinate with maintainers
   git filter-branch --force --index-filter \
     "git rm --cached --ignore-unmatch path/to/file" \
     --prune-empty --tag-name-filter cat -- --all

   # Force push (coordinate with team first)
   git push origin --force --all
   ```

4. **Understand the scope**:
   - Git history is permanent on GitHub
   - Forks may retain the credential
   - Cached pages/search engines may have indexed it
   - **Assume the credential is public forever**

---

## What to Do If You Find a Security Issue

### Reporting Security Vulnerabilities

**Do NOT open a public issue** for security vulnerabilities.

Instead:

1. **Email the maintainers** (if contact info available in repository)
2. **Use GitHub Security Advisories** (if enabled for this repo)
3. **Include in your report**:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if you have one)

### What Constitutes a Security Issue?

**Security issues** include:
- Exposed credentials in repository
- Malicious code in prompts
- Unsafe tool usage that could harm systems
- Data exfiltration vectors
- Prompt injection vulnerabilities

**Not security issues** (open normal issues):
- Documentation errors
- Feature requests
- Usability improvements
- Performance problems

---

## Security Best Practices for Claude Code

### General Claude Code Security

When using ultraplan or any Claude Code tools:

1. **Review all generated plans before executing**
   - Check for unexpected file modifications
   - Verify command safety
   - Ensure no credential exposure

2. **Use separate sessions for planning vs. execution**
   - Planning session: Read-only investigation
   - Execution session: Controlled changes
   - Never mix the two

3. **Keep credentials in environment variables**
   - Use `.env` files (in `.gitignore`)
   - Never hardcode in source files
   - Use secret management tools

4. **Review documentation before sharing**
   - Generated plans may contain sensitive paths
   - Investigation findings may reveal architecture
   - Redact before publishing publicly

5. **Be cautious with generated code**
   - Review before committing
   - Test in isolated environments
   - Verify no security vulnerabilities introduced

---

## Threat Model

### What This Repository Protects Against

✅ **Credential exposure**: No secrets in repository
✅ **Code execution risks**: No executable code
✅ **Supply chain attacks**: Simple, auditable prompts
✅ **Data exfiltration**: No network access in slash command
✅ **Malicious modifications**: Open source, community reviewed

### What Users Must Protect

⚠️ **Your responsibility**:
- Your own API keys and credentials
- Your codebase contents (when using ultraplan on private repos)
- Generated documentation (may contain sensitive info)
- Execution of generated plans (review before running)

---

## Privacy

### Data Collection

This repository:
- ❌ Does not collect any user data
- ❌ Does not send telemetry
- ❌ Does not track usage
- ❌ Does not require accounts or registration

### What Stays Local

When using ultraplan:
- ✅ All investigation stays on your machine
- ✅ Generated documentation saved locally only
- ✅ No data sent to external services
- ✅ Your codebase never leaves your system

---

## Compliance

### License Compliance

- MIT License - permissive, commercial use allowed
- No warranty or liability
- Attribution required (see LICENSE file)

### Use in Regulated Environments

If you work with:
- Healthcare data (HIPAA)
- Financial data (PCI-DSS, SOX)
- Personal data (GDPR, CCPA)
- Government data (FedRAMP, etc.)

**Additional considerations**:
- Review your organization's policies on AI tool usage
- Ensure generated documentation doesn't contain regulated data
- Use on appropriately secured systems
- Follow your organization's code review processes

---

## Updates

This security policy may be updated as:
- New security considerations are identified
- Community feedback is received
- Best practices evolve

**Last Updated**: 2025-11-05

---

## Questions?

For security-related questions:
- Open a discussion on GitHub (for general questions)
- Email maintainers directly (for sensitive issues)
- Follow security best practices above

**Remember**: When in doubt, redact or ask before sharing!
