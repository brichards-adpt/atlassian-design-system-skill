# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository contains a **Claude Code Skill** for the Atlassian Design System (ADS). The skill teaches Claude how to build pixel-perfect, accessible UIs using ADS components, tokens, and primitives.

## Repository Structure

```
.
├── atlassian-design-system/          # Packaged skill directory
│   ├── SKILL.md                      # Main skill instructions (11KB)
│   ├── references/                   # Reference documentation (250KB+)
│   │   ├── ads-components.md         # ADS component catalog
│   │   ├── ads-icons.md              # Icon reference with import paths
│   │   ├── ads-tokens.md             # Design token reference
│   │   └── ads-api-complete.txt      # Full API documentation (4966 lines)
│   ├── scripts/                      # Executable scripts (currently empty)
│   └── assets/                       # Template files (currently empty)
└── reference for skill building/     # Source materials used to build skill
    ├── ads-rules-lite.md             # Original ADS implementation rules
    ├── ads-components.md             # Original component reference
    ├── ads-icons.md                  # Original icon reference
    ├── ads-tokens.md                 # Original token reference
    └── llms-full.txt                 # Complete ADS documentation from Atlassian
```

## Skill Development Commands

### Validating the Skill

```bash
python3 ~/.claude/skills/skill-creator/scripts/package_skill.py "./atlassian-design-system"
```

This command:
1. Validates skill structure and frontmatter
2. Checks for required fields and proper organization
3. Packages the skill into a distributable `.skill` file

### Packaging After Changes

After modifying SKILL.md or reference files:

```bash
# Validate and package in one step
python3 ~/.claude/skills/skill-creator/scripts/package_skill.py "./atlassian-design-system"

# Output: atlassian-design-system/atlassian-design-system.skill
```

### Installing Locally for Testing

```bash
# Copy the packaged .skill file to Claude's skills directory
cp atlassian-design-system/atlassian-design-system.skill ~/.claude/skills/
```

## Architecture & Design Principles

### Skill Structure Philosophy

This skill follows the **Skill Creator best practices** from `~/.claude/skills/skill-creator/`:

1. **Progressive Disclosure**: Keep SKILL.md concise (<500 lines), move comprehensive details to `references/`
2. **Token Efficiency**: Only essential workflow in SKILL.md; references loaded as needed
3. **Self-Contained**: All documentation bundled; no external dependencies except MCP fallback
4. **Search-Friendly**: References organized for quick grep/search lookups

### Three-Level Loading System

1. **Metadata** (name + description): Always in context (~100 words)
2. **SKILL.md body**: Loaded when skill triggers (~11KB)
3. **Reference files**: Loaded by Claude as needed (~250KB total)

### Key Design Decisions

**Accuracy vs Standards Tradeoff**
- User preference: **Ask user each time** there's a tradeoff between standard ADS components and pixel-perfect accuracy
- SKILL.md includes framework for presenting tradeoffs clearly

**Reference Organization**
- `ads-components.md`: Quick component lookup (10KB)
- `ads-icons.md`: Icon import paths (17KB)
- `ads-tokens.md`: Token validation reference (11KB)
- `ads-api-complete.txt`: Deep API details (215KB) - searched, not read whole

**Framework Support**
- Framework-agnostic guidance
- Special section for Atlassian Forge apps

## Modifying the Skill

### When to Edit SKILL.md

Edit `atlassian-design-system/SKILL.md` when:
- Adding/updating core workflows
- Changing initialization protocol
- Updating project setup requirements
- Modifying the verification checklist
- Adding/removing major sections

**Keep under 500 lines**. If approaching this limit, move content to reference files.

### When to Edit Reference Files

Edit files in `atlassian-design-system/references/` when:
- Updating component APIs or packages
- Adding new icons or deprecating old ones
- Changing design tokens
- Updating detailed API documentation

**DO NOT duplicate** between SKILL.md and references - information should live in one place only.

### Updating from Source Materials

The `reference for skill building/` directory contains original source materials:
- These are NOT part of the packaged skill
- Update reference files in `atlassian-design-system/references/` when Atlassian releases updates
- Maintain the same structure and format for consistency

### Validation Requirements

Before packaging, ensure:
1. **Frontmatter**: Valid YAML with `name` and `description` fields
2. **Description**: Comprehensive "when to use" triggers included
3. **References**: All linked files exist and paths are correct
4. **No Extraneous Files**: No README.md, CHANGELOG.md, or auxiliary docs

## Git Workflow

### Committing Changes

```bash
# Stage skill changes
git add atlassian-design-system/

# Commit with descriptive message
git commit -m "feat: [description of change]

[Optional detailed explanation]

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>"
```

### Branch Strategy

This repository uses `main` branch directly (no feature branches currently configured).

## Skill Metadata

**Name**: `atlassian-design-system`

**Trigger Description**: Deep reference for Atlassian Design System packages, components, foundations, and design tokens. Use when building apps with ADS components, theming, tokens, primitives, icons, or related utilities and tooling.

**Size**: ~70KB packaged (.skill file)

**Reference Files**: 4 files totaling 250KB+ of documentation

## MCP Integration

This skill references the **Atlassian MCP server** as a fallback:
- Primary: Local reference files (ads-components.md, ads-icons.md, ads-tokens.md)
- Fallback: MCP server for real-time validation or missing details
- Search tools should be used before guessing any imports

The skill is designed to work standalone without MCP, with MCP providing supplementary validation.
