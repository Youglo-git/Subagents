# Sub-agents Collection

A curated collection of Claude sub-agents for specialized tasks, stored in `.claude/agents/`.

## Overview

Each agent is defined as a Markdown file with YAML frontmatter in `.claude/agents/`. Claude selects the appropriate agent based on context and the agent's `description` field, or you can ask Claude to use a specific agent explicitly.

## Agents

### `code-reviewer`
**Model:** Sonnet | **Color:** Orange

Reviews recently changed or written code for quality, correctness, security, and best practices. Invoked when Claude detects meaningful code changes (new features, refactors, bug fixes).

**Review dimensions:** Correctness, Security, Performance, Code Quality, Test Coverage, API Design

**Output:** Severity-ranked issue list (Critical / Major / Minor / Suggestion) with file/line references, positive highlights, and a merge verdict.

## Usage

Agents are invoked automatically when Claude Code detects a matching context. You can also trigger them explicitly:

```
Use the code-reviewer agent to review my recent changes.
```

## Agent File Structure

```
.claude/agents/<name>.md
```

Frontmatter fields:
- `name` — agent identifier
- `description` — when to invoke (include `<example>` blocks for precision)
- `model` — `sonnet`, `opus`, or `haiku`
- `color` — UI color label

## Agent Memory

Agents can maintain persistent memory across conversations using a file-based system in `.claude/agent-memory/<agent-name>/`. This is a convention implemented in each agent's system prompt — not a native Claude Code feature. The memory path must be resolvable from the project root.

> **Note:** If you move or rename the project directory, verify that memory paths in agent definitions still resolve correctly.

