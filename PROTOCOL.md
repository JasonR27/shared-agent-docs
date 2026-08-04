# Cross-Agent Communication and Coworking Protocol

> **⚠️ IMMUTABLE FILE — DO NOT EDIT**
> 
> **Status**: LOCKED — Read-only after finalization on 2026-08-04  
> **Enforcement**: Filesystem `chmod 444` (read-only for all)  
> **Owner**: Jason (jasonr27) — sole human editor  
> **Identifier for MCP Storage**: `CrossAgentProtocol:v1`  
> **Hash**: To be computed upon finalization  
> **Version**: 1.0.0  
> **Date**: 2026-08-04  
> 
> **Any agent found modifying this file must immediately revert changes and report the violation.**
> This file is the single source of truth for cross-agent communications.
> All agents MUST read this file in full before any cross-agent interaction unless they have cached it for the current session.

---

## 1. Purpose

This protocol defines how AI agents in the JasonR27 ecosystem communicate, collaborate, and share work. It establishes rules for:
- Reading and writing shared documents
- Leaving messages and tasks for other agents
- Assigning isolatable tasks to other agents
- Requesting information or continuation from other agents
- Maintaining shared memory (Neo4j/NAMS and MemPalace)
- Preventing conflicts, data loss, and rogue edits

## 2. Agents in the Ecosystem

| Agent | Type | Config Location | Workspace |
|-------|------|----------------|------------|
| **OpenClaw** | AI assistant (local LLM) | `~/.openclaw/openclaw.json` | `~/.openclaw/workspace/` |
| **OpenCode** | AI coding agent | `~/.config/opencode/opencode.jsonc` | `~/.config/opencode/` |
| **Hermes** | Python AI agent | `~/.hermes/config.yaml` | `~/.hermes/` |
| **Cline** | VSCode AI coding agent | VSCode extension settings | Per-project |
| **Kiro** | Agentic IDE (AWS) | `~/.kiro/settings/mcp.json` | `~/.kiro/` |

New agents can be added by Jason only. When added, this file must be updated (by Jason) with their details.

## 3. Shared Infrastructure

### 3.1 Shared Docs Repository

- **Location**: `~/Documents/Github/JasonR27/shared-agent-docs/`
- **Git**: Version-controlled. All agents may `git pull` and `git commit` (except PROTOCOL.md).
- **Structure**:
  - `PROTOCOL.md` — THIS FILE. Immutable. Read-only. Do not edit.
  - `AGENT_UPDATES.md` — Current status of each agent. All agents may append.
  - `sessions/` — Per-session coworking files (e.g., `2026-08-04-skills-absorption.md`).
  - `skills/` — Cross-agent skill documentation.

### 3.2 Shared Memory MCPs

All agents share these memory systems:

| MCP | Endpoint | Workspace ID | Purpose |
|-----|----------|-------------|---------|
| **Neo4j AuraDB** | `neo4j+s://e7619bc7.databases.neo4j.io` | — | Primary graph database |
| **NAMS Memory** | `https://memory.neo4jlabs.com/mcp` | `1495e133-43c3-460b-a1a0-b97eaa45b943` | Conversation memory, entity store |
| **MemPalace** | Local conda (`~/miniconda3/envs/mempalace-mcp/`) | — | Contextual memory palace |
| **Neo4j Memory MCP** | stdio (conda env `neo4j-mcp`) | — | Direct graph CRUD |

**Protocol identifier in NAMS**: Entity label `CrossAgentProtocol`, name `CrossAgentProtocol:v1`. Any agent can query:
```
MATCH (p:CrossAgentProtocol {name: 'CrossAgentProtocol:v1'}) RETURN p
```
to find this protocol's metadata and verify they're talking to the right system.

**Protocol identifier in MemPalace**: Drawer named `cross-agent-protocol-v1`. Any agent can search for this drawer to find protocol metadata.

## 4. Rules for Cross-Agent Communication

### 4.1 The Golden Rule

**ALWAYS read PROTOCOL.md in full before any cross-agent interaction, unless you have cached it for the current session.**

Caching is per-session: if you start a new session, re-read. If your session is interrupted or context is compacted, re-read. When in doubt, re-read.

### 4.2 What Constitutes a Cross-Agent Interaction

Any of the following triggers the read requirement:
- Leaving a message for another agent
- Reading a message from another agent
- Assigning a task to another agent
- Accepting a task from another agent
- Requesting data, code review, or continuation from another agent
- Writing to a shared file that another agent may read
- Writing to shared memory (NAMS/MemPalace) about another agent
- Creating or modifying shared docs

### 4.3 Message Format

Messages between agents MUST use the following format in shared docs:

```markdown
## Message: [from-agent] → [to-agent]
**Date**: YYYY-MM-DD HH:MM TZ
**Subject**: Brief subject line
**Priority**: low | normal | high | urgent
**Status**: pending | accepted | in-progress | completed | blocked

### Body
Message content here.

### Action Items
- [ ] Action item 1
- [ ] Action item 2

### References
- File: path/to/relevant/file
- NAMS entity: entity name or ID
- MemPalace drawer: drawer name
```

### 4.4 Task Assignment Format

When assigning a task to another agent:

```markdown
## Task Assignment: [from-agent] → [to-agent]
**Date**: YYYY-MM-DD HH:MM TZ
**Task ID**: [ YYYYMMDD-HHMM-<short-slug> ]
**Priority**: low | normal | high | urgent
**Isolatable**: yes | no (can this run in isolation without context from assigner?)

### Objective
Clear statement of what needs to be accomplished.

### Scope
- What files/resources to touch
- What NOT to touch
- Expected output

### Verification
How the assigner will verify completion.

### Dependencies
- Any blockers or prerequisites
- Files to read first
```

### 4.5 Shared File Editing Rules

1. **No concurrent edits**: Before editing a shared file, check if another agent is working on it (look for a `.lock` file or a "WIP" marker in the file).
2. **Atomic writes**: Write complete content, not partial edits, to shared files. Use git commits for traceability.
3. **Never edit PROTOCOL.md**: This file is immutable. Any proposed changes must go through Jason.
4. **Commit messages**: Use the format `[agent-name] action description`.
5. **Conflicts**: If two agents commit to the same file, the second committer must resolve the conflict and notify the first.

### 4.6 Shared Memory Rules

1. **NAMS**: Each agent uses its own `conversation_id` per session. Entities merge by name. No agent should delete another agent's entities.
2. **MemPalace**: Each agent may create drawers. Never delete another agent's drawers.
3. **Neo4j Memory MCP**: Use `CREATE` sparingly. Prefer `MERGE` to avoid duplicates. Never run `DROP` or `DELETE` on entities you didn't create.
4. **Cross-agent entities**: Tag with `:AgentWork` label and include the originating agent's name in properties.

### 4.7 Anti-Conflict Rules

1. Before starting work, `git pull` the shared docs repo.
2. After finishing work, `git add`, `git commit`, and `git push` (if remote is configured).
3. If working on the same file as another agent, coordinate via a session file in `sessions/`.
4. Never force-push (`git push --force`) the shared docs repo.
5. Never delete another agent's commit or work.
6. If you encounter a conflict, stop and notify the other agent via a message in AGENT_UPDATES.md.

## 5. Mandatory Behaviors

### 5.1 Before Starting Cross-Agent Work

1. **Read PROTOCOL.md** (this file) in full — or use your session cache.
2. **Read AGENT_UPDATES.md** to know the current state of all agents.
3. **Check for messages addressed to you** in AGENT_UPDATES.md and `sessions/`.
4. **`git pull`** the shared docs repo.
5. **Query NAMS** for any existing context: `memory_search` with relevant keywords.
6. **Query MemPalace** for any relevant drawers.

### 5.2 During Cross-Agent Work

1. **Log all decisions** to NAMS with appropriate entity labels.
2. **Update AGENT_UPDATES.md** with your current status (what you're doing, ETA).
3. **Write messages in the correct format** (§4.3, §4.4).
4. **Commit work frequently** — small, atomic commits.
5. **Never assume another agent's state** — verify via AGENT_UPDATES.md or direct query.

### 5.3 After Completing Cross-Agent Work

1. **Update AGENT_UPDATES.md** with completion status.
2. **Log results to NAMS and MemPalace.**
3. **Leave a completion message** for the requesting agent if applicable.
4. **`git commit and push`** all changes.
5. **Remove any lock files** you created.

## 6. Memory Storage Protocol

### 6.1 NAMS Entity Schema for Cross-Agent Work

```
(:CrossAgentProtocol {name: 'CrossAgentProtocol:v1', version: '1.0.0', file: 'PROTOCOL.md'})

(:Agent {name: 'OpenClaw', type: 'assistant', config: '~/.openclaw/openclaw.json'})
(:Agent {name: 'OpenCode', type: 'coding', config: '~/.config/opencode/opencode.jsonc'})
(:Agent {name: 'Hermes', type: 'python-ai', config: '~/.hermes/config.yaml'})
(:Agent {name: 'Cline', type: 'vscode-agent', config: 'vscode-settings'})
(:Agent {name: 'Kiro', type: 'agentic-ide', config: '~/.kiro/settings/mcp.json'})

(:AgentWork {agent: 'agent-name', task: 'task-description', date: 'YYYY-MM-DD', status: 'completed|in-progress|blocked'})
```

Relationships:
```
(:Agent)-[:PARTICIPATES_IN]->(:CrossAgentProtocol)
(:Agent)-[:ASSIGNED]->(:AgentWork)
(:Agent)-[:COMPLETED]->(:AgentWork)
(:Agent)-[:LEFT_MESSAGE]->(:Message)
```

### 6.2 MemPalace Drawer Schema

- `cross-agent-protocol-v1` — Protocol metadata
- `agent-status-{agent-name}` — Per-agent status and capabilities
- `coworking-session-{date}-{slug}` — Per-session coworking context
- `task-{task-id}` — Per-task context and results

## 7. Extensibility

### 7.1 Adding New Agents

1. Jason adds the agent to §2 of this file.
2. Jason updates the NAMS `Agent` entity and MemPalace drawer.
3. The new agent reads PROTOCOL.md on first interaction.
4. The new agent posts an introduction to AGENT_UPDATES.md.

### 7.2 Protocol Versioning

- Version 1.0.0 is the initial locked version.
- Any changes require Jason's approval and a version bump.
- Old versions are archived, never deleted.
- The NAMS `CrossAgentProtocol` entity carries the version number.

### 7.3 Future Transport Layer

This protocol defines the **document-based communication layer** (Layer 1). A future **transport layer** (Layer 2) will enable agents to send prompts and data directly to each other. Layer 2 will be built on top of Layer 1 and must comply with all rules in this file.

## 8. Violations

If an agent violates this protocol:
1. **Revert** any unauthorized changes to PROTOCOL.md immediately.
2. **Report** the violation to AGENT_UPDATES.md.
3. **Notify** Jason directly if possible.
4. The violating agent must re-read PROTOCOL.md before any further cross-agent work.

## 9. Quick Reference

```
BEFORE cross-agent work:
  1. Read PROTOCOL.md (this file) or use session cache
  2. Read AGENT_UPDATES.md
  3. git pull shared-agent-docs/
  4. Query NAMS for context
  5. Query MemPalace for context

DURING cross-agent work:
  1. Use correct message/task format
  2. Commit frequently
  3. Log decisions to NAMS + MemPalace

AFTER cross-agent work:
  1. Update AGENT_UPDATES.md
  2. Log results to NAMS + MemPalace
  3. git commit + push
  4. Remove lock files
```

---

**Protocol Version**: 1.0.0  
**Created**: 2026-08-04  
**Author**: Jason (jasonr27) with OpenClaw  
**License**: Private — JasonR27 ecosystem only  
**Immutability**: Enforced via `chmod 444` and git-protected history
