# Changelog

All notable changes to the Claude Code Ultraplan project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Future Enhancements Under Consideration
- Automatic complexity detection improvements based on file count
- Integration with other Claude Code tools and workflows
- Templates for common task patterns
- Metrics dashboard for tracking planning efficiency
- Community-contributed prompt improvements
- Multi-language support for documentation

## [2.0.2] - 2025-11-06

### Changed
- **Major documentation restructure**: Consolidated all documentation into single README.md
- Merged INSTALL.md, ONE_TIME_USE.md, USAGE.md, and EXAMPLES.md into comprehensive README
- Deleted 7 redundant documentation files (START_HERE.md, GITHUB_SETUP.md, SECURITY.md, ULTRAPLAN_CHANGELOG.md, INSTALL.md, ONE_TIME_USE.md, USAGE.md, EXAMPLES.md)
- Created `archived/` directory for old version files
- Moved v1.0.0-original.md and v2.0.0-slashcommand.md to `archived/`

### Fixed
- Eliminated documentation redundancy and maintenance burden
- Established single source of truth for all user documentation
- Simplified repository structure from 14 files to 6 core files

### Improved
- Much easier to maintain - one change, one file update
- Better user experience - all info in one place
- Reduced confusion from conflicting information across multiple files

**Impact**: Patch release - no functional changes to ultraplan.md, only repository structure and documentation organization improvements

## [2.0.1] - 2025-11-06

### Fixed
- Corrected all branch references in INSTALL.md from '/main/' to '/master/' (4 instances)
- Reformatted "Automated Installation" section in INSTALL.md as a single, clear prompt for users to copy and paste to Claude Code, eliminating ambiguity about execution responsibility

## [2.0.0] - 2025-11-05

### Added
- **Dual-mode operation** - Code Implementation Mode + General Task Planning Mode (MAJOR FEATURE)
- Mode selection system using AskUserQuestion tool
- General Task Planning Mode for non-code tasks (workflows, research, projects, content, resources, learning)
- Mode-specific output locations (`/Scrapbook/` for code, `~/Documents/Plans/` for general)
- General mode deliverables: `resources_list.md` and `alternatives_analysis.md`
- Mode-aware documentation structures throughout all 4 phases
- YAML frontmatter with slash command metadata
- Section 7 "Context for Executor" in implementation plans
- Comprehensive version history documentation ([ULTRAPLAN_CHANGELOG.md](ULTRAPLAN_CHANGELOG.md))
- Original v1.0.0 archived in `v1.0.0-original.md`

### Changed
- **BREAKING**: Now requires mode selection at invocation (but Code mode maintains v1.0.0 compatibility)
- Task classification now branches by mode (code vs. general task types)
- Complexity classification made universal (works for both code and non-code tasks)
- Investigation phase explicitly branches based on selected mode
- Requirements inventory expanded with mode-specific elements
- Plan structure adapts to mode context
- Success criteria now universal with mode-aware guidance

### Enhanced
- More detailed specifications for both code and general tasks
- Clearer investigation execution instructions
- Expanded risk management strategies
- Better context preservation for executors

## [1.0.0] - 2025-11-05

### Added
- Initial private release of Universal Implementation Plan Generator (code-only)
- Four-phase planning protocol (Classification, Investigation, Documentation, Plan Creation)
- Complexity-aware scaling (1-2 agents for simple tasks, 5+ for complex)
- Zero-assumption investigation methodology
- Persistent markdown documentation for cross-session handoffs
- Four core deliverable files (investigation findings, implementation plan, dependencies map, testing checklist)
- Code-specific files (testing_strategy.md, rollback_plan.md)
- Token economics model (upfront investment, long-term recovery)
- Session-independent execution capabilities

### Features
- **Code Implementation Only**: Bug fixes, features, refactoring, API integrations, infrastructure
- Task types: New Feature, Bug Fix, Refactoring, Integration, Infrastructure
- **Complexity Classification**: Low/Medium/High based on files affected
- **Scaled Investigation**: Launches appropriate number of parallel subagents for code analysis
- **Gap Analysis**: Re-investigates until zero assumptions remain
- **Validation Framework**: Testing checkpoints and rollback procedures
- **Context Preservation**: Complete state saved in `/Scrapbook/` for future sessions

### Limitations
- **Code tasks only** - Could not plan non-development tasks
- Single output location (`/Scrapbook/` only)
- No mode selection (assumed all tasks were code-related)

### Origin
- Created as part of LIMITED EDITION JONATHAN's Collaborative Prompt Engineering #001 initiative
- Based on production testing across code implementation projects
- Foundation for v2.0.0 universal planning expansion

---

## Version History

| Version | Date | Description | Status |
|---------|------|-------------|--------|
| **v2.0.2** | 2025-11-06 | Documentation consolidation (current) | ✅ Active |
| v2.0.1 | 2025-11-06 | Documentation fixes | 📦 Previous |
| v2.0.0 | 2025-11-05 | Dual-mode universal planning | 📦 Previous |
| v1.0.0 | 2025-11-05 | Original code-only version | 📦 Archived |

**Current Version**: v2.0.2 (ultraplan.md)
**Archived Versions**: v1.0.0, v2.0.0 (see `archived/` directory)

## How to Install/Upgrade

### First-Time Installation
```bash
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/master/ultraplan.md
```

### Upgrading from v1.0.0 to v2.0.0
```bash
# Same command - just overwrites the old version
curl -o ~/.claude/commands/ultraplan.md https://raw.githubusercontent.com/seisenstein/claude-code-ultraplan/master/ultraplan.md
```

**Restart Claude Code** to load the new version.

**No breaking changes for code tasks** - Select "Code Implementation Mode" for v1.0.0-compatible behavior.

---

## Contributing to Changelog

When submitting PRs, please add an entry under `[Unreleased]` in the appropriate category:
- `Added` for new features
- `Changed` for changes in existing functionality
- `Deprecated` for soon-to-be removed features
- `Removed` for now removed features
- `Fixed` for any bug fixes
- `Security` for vulnerability fixes

Example:
```markdown
### Added
- New complexity detection algorithm for monorepos
```

---

**Note**: This project follows [Semantic Versioning](https://semver.org/):
- MAJOR version (X.0.0) - Incompatible API changes
- MINOR version (0.X.0) - Backwards-compatible functionality additions
- PATCH version (0.0.X) - Backwards-compatible bug fixes
