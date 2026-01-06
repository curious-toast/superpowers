# Superpowers for Codex

Complete guide for using Superpowers with OpenAI Codex.

## Installation

### Prerequisites

- OpenAI Codex access
- Shell access to install files
- This repo cloned locally

### Installation Steps

#### 1. Symlink Superpowers

```bash
ln -s ~/development/repos/superpowers ~/.codex/superpowers
```

#### 2. Install Bootstrap

The bootstrap file is included in the repository at `.codex/superpowers-bootstrap.md`. Codex will automatically use it from the cloned location.

#### 3. Verify Installation

Tell Codex:

```
Run ~/.codex/superpowers/.codex/superpowers-codex find-skills to show available skills
```

You should see a list of available skills with descriptions.

## Usage

### Finding Skills

```
Run ~/.codex/superpowers/.codex/superpowers-codex find-skills
```

### Loading a Skill

```
Run ~/.codex/superpowers/.codex/superpowers-codex use-skill superpowers:brainstorming
```

### Bootstrap All Skills

```
Run ~/.codex/superpowers/.codex/superpowers-codex bootstrap
```

This loads the complete bootstrap with all skill information.

### Personal Skills

Create your own skills in `~/.codex/skills/`:

```bash
mkdir -p ~/.codex/skills/my-skill
```

Create `~/.codex/skills/my-skill/SKILL.md`:

```markdown
---
name: my-skill
description: Use when [condition] - [what it does]
---

# My Skill

[Your skill content here]
```

Personal skills override superpowers skills with the same name.

## Architecture

### Codex CLI Tool

**Location:** `~/.codex/superpowers/.codex/superpowers-codex`

A Node.js CLI script that provides three commands:
- `bootstrap` - Load complete bootstrap with all skills
- `use-skill <name>` - Load a specific skill
- `find-skills` - List all available skills

### Shared Core Module

**Location:** `~/.codex/superpowers/lib/skills-core.js`

The Codex implementation uses the shared `skills-core` module (ES module format) for skill discovery and parsing. This is the same module used by the OpenCode plugin, ensuring consistent behavior across platforms.

### Tool Mapping

Skills written for Claude Code are adapted for Codex with these mappings:

- `TodoWrite` → `update_plan`
- `Task` with subagents → Tell user subagents aren't available, do work directly
- `Skill` tool → `~/.codex/superpowers/.codex/superpowers-codex use-skill`
- File operations → Native Codex tools

## Updating

Pull the latest changes in your local clone of the repo.

## Troubleshooting

### Skills not found

1. Verify installation: `ls ~/.codex/superpowers/skills`
2. Check CLI works: `~/.codex/superpowers/.codex/superpowers-codex find-skills`
3. Verify skills have SKILL.md files

### CLI script not executable

```bash
chmod +x ~/.codex/superpowers/.codex/superpowers-codex
```

### Node.js errors

The CLI script requires Node.js. Verify:

```bash
node --version
```

Should show v14 or higher (v18+ recommended for ES module support).

