# Cross-Agent Communication and Coworking System — Full Plan

> **Date**: 2026-08-04  
> **Author**: OpenClaw for Jason  
> **Status**: Phase 1 in progress  
> **Prior plans referenced**:  
> - `~/Documents/Github/JasonR27/docs/plans/2026-07-31-subplan-openclaw.md` (OpenClaw track)  
> - `~/Documents/Github/JasonR27/docs/plans/2026-07-31-subplan-hermes.md` (Hermes track)  
> - `~/Documents/Github/JasonR27/docs/plans/2026-07-31-subplan-cline.md` (Cline track)

---

## Core Objective

Build a comprehensive cross-agent communication and coworking system that enables all AI agents in the JasonR27 ecosystem (OpenClaw, OpenCode, Hermes, Cline, Kiro, and future agents) to:
1. Share a common communication protocol via an immutable rules file
2. Maintain current status visibility via a shared updates file
3. Coordinate work via shared session files in a git-controlled repo
4. Use shared memory (NAMS/Neo4j and MemPalace) to store and retrieve cross-agent context
5. Discover and use each other's skills and capabilities
6. Safely escalate to a future transport layer (agent-to-agent direct messaging)

## Architecture Overview

```
Layer 1: Document-Based Communication (THIS PLAN)
  ├── shared-agent-docs/ (git repo)
  │   ├── PROTOCOL.md          (IMMUTABLE — chmod 444)
  │   ├── AGENT_UPDATES.md     (all agents append status)
  │   ├── sessions/            (per-coworking-session files)
  │   └── skills/             (cross-agent skill documentation)
  │
  ├── NAMS/Neo4j (shared memory graph)
  │   └── CrossAgentProtocol:v1 entity (well-known identifier)
  │
  └── MemPalace (shared contextual memory)
      └── cross-agent-protocol-v1 drawer

Layer 2: Transport Layer (FUTURE — not in this plan)
  ├── Agent-to-agent direct messaging
  ├── Prompt injection across agents
  └── Data streaming between agents
```

---

## Phase 1: Document-Based Communication Layer (CURRENT)

### 1.1 Shared Docs Repo ✅ DONE
- [x] Created `~/Documents/Github/JasonR27/shared-agent-docs/` as a git repo
- [x] Structure: `PROTOCOL.md`, `AGENT_UPDATES.md`, `sessions/`, `skills/`
- [x] Initial commit made
- [ ] GitHub remote setup (Jason to create on GitHub)

### 1.2 Immutable Protocol File ✅ DONE
- [x] Written `PROTOCOL.md` with:
  - §1 Purpose
  - §2 Agent registry (all 5 agents with config paths)
  - §3 Shared infrastructure (docs repo, NAMS, MemPalace)
  - §4 Rules for cross-agent communication (message format, task format, file editing, shared memory, anti-conflict)
  - §5 Mandatory behaviors (before/during/after cross-agent work)
  - §6 Memory storage protocol (NAMS entity schema, MemPalace drawer schema)
  - §7 Extensibility (adding agents, versioning, future transport)
  - §8 Violations
  - §9 Quick reference
- [x] `chmod 444` applied — file is now read-only
- [x] Committed to git

### 1.3 Agent Updates File ✅ DONE
- [x] Written `AGENT_UPDATES.md` with:
  - OpenClaw status (206 skills, MCP bridge, NAMS plugin)
  - OpenCode status (95 skills, 33 agents, NAMS hooks)
  - Hermes status (18 MCPs, Phase 0+A done, Plan C pending)
  - Cline status (VSCode extension, Plan B pending)
  - Kiro status (full deep-research findings)
  - Cross-agent status matrix (MCP parity, skills parity, NAMS integration status)

### 1.4 Session Files
- [ ] Create template session file in `sessions/TEMPLATE.md`
- [ ] Create first session file: `sessions/2026-08-04-skills-and-protocol-setup.md`

### 1.5 Skills Documentation
- [ ] Full skills report (206 skills) — IN PROGRESS (subagent generating)
- [ ] Write to `skills/SKILLS_FULL_REPORT.md`
- [ ] Write summary to workspace `SKILLS_SUMMARY.md`

### 1.6 Store Protocol in Shared Memory
- [ ] Store `CrossAgentProtocol:v1` entity in NAMS via REST API
- [ ] Store `Agent` entities for all 5 agents in NAMS
- [ ] Store `CrossAgentProtocol` drawer in MemPalace
- [ ] Store agent status drawers in MemPalace
- [ ] Verify any agent can query and find the protocol

### 1.7 Skills Registration
- [x] All 107 registered skills set to `enabled: true` in openclaw.json
- [x] All 206 skills in `~/.agents/skills/` auto-discoverable
- [ ] Verify gateway picks up all skills after restart
- [ ] Generate skill-by-skill report with purpose and usage

### 1.8 Memory Update
- [ ] Update `MEMORY.md` with:
  - Cross-agent protocol details
  - Kiro research findings
  - Shared docs repo location
  - Skills registration status
- [ ] Write daily note `memory/2026-08-04.md`
- [ ] Store key findings in NAMS

---

## Phase 2: Cross-Agent Skills Development (NEXT)

### 2.1 Cross-Agent Communication Skill
- [ ] Create `cross-agent-communication` skill in `~/.agents/skills/`
- [ ] SKILL.md content:
  - How to read PROTOCOL.md
  - How to write messages to other agents
  - How to assign tasks to other agents
  - How to update AGENT_UPDATES.md
  - How to query NAMS for cross-agent context
  - How to use MemPalace for cross-agent memory
- [ ] Register in openclaw.json

### 2.2 Cross-Agent Onboarding Skill
- [ ] Create `cross-agent-onboarding` skill in `~/.agents/skills/`
- [ ] SKILL.md content:
  - What a new agent needs to do to join the ecosystem
  - Read PROTOCOL.md first
  - Query NAMS for CrossAgentProtocol:v1
  - Post introduction to AGENT_UPDATES.md
  - Create Agent entity in NAMS
  - Create MemPalace drawer
- [ ] Register in openclaw.json

### 2.3 Install Skills for Other Agents
- [ ] Symlink skills into Kiro's `~/.kiro/skills/` (if not already)
- [ ] Copy to OpenCode's `~/.config/opencode/skills/`
- [ ] Copy to Hermes's `~/.hermes/skills/`
- [ ] Document in AGENT_UPDATES.md

---

## Phase 3: Agent-Specific Integration

### 3.1 OpenCode Integration
- [ ] Add PROTOCOL.md read directive to OpenCode's AGENTS.md
- [ ] Add NAMS query directive for CrossAgentProtocol:v1
- [ ] Test: OpenCode can read shared docs, query NAMS, find protocol

### 3.2 Hermes Integration
- [ ] Add PROTOCOL.md read directive to Hermes steering/config
- [ ] Plan C from hermes subplan: Implement NAMS MemoryProvider plugin
- [ ] Plan C: Implement Cortex-CS MemoryProvider plugin
- [ ] Test: Hermes can read shared docs, query NAMS, find protocol

### 3.3 Cline Integration
- [ ] Add PROTOCOL.md read directive to Cline's `.clinerules/`
- [ ] Plan B from cline subplan: Add 11 MCP servers
- [ ] Plan B: Convert 33 agents to `.clinerules/agents/`
- [ ] Test: Cline can read shared docs, query NAMS, find protocol

### 3.4 Kiro Integration
- [ ] Add PROTOCOL.md read directive to Kiro's steering file
- [ ] Configure custom agents in Kiro for cross-agent work
- [ ] Populate Powers registry with cross-agent power
- [ ] Test: Kiro can read shared docs, query NAMS, find protocol

---

## Phase 4: Transport Layer (FUTURE — Not Started)

### 4.1 Design
- [ ] Design agent-to-agent messaging transport
- [ ] Define prompt injection protocol (agent as user to another agent)
- [ ] Define data streaming protocol
- [ ] Security model: authentication, authorization, scope

### 4.2 Implementation
- [ ] Build transport server (likely HTTP-based)
- [ ] Agent registration and discovery
- [ ] Message routing
- [ ] Audit logging to NAMS

### 4.3 Integration
- [ ] Integrate with Layer 1 (this plan) — must comply with PROTOCOL.md
- [ ] All existing rules apply to transport layer
- [ ] Transport version bump to protocol v2.0.0

---

## Tasks Status (Current)

| Task | Status | Owner |
|------|--------|-------|
| Skills enabled (107 → enabled:true) | ✅ DONE | OpenClaw |
| Shared docs repo created | ✅ DONE | OpenClaw |
| PROTOCOL.md written + locked | ✅ DONE | OpenClaw |
| AGENT_UPDATES.md written | ✅ DONE | OpenClaw |
| Kiro deep research | ✅ DONE | OpenClaw |
| Full skills report (206 skills) | 🔄 IN PROGRESS | Subagent |
| Template session file | ⏳ PENDING | OpenClaw |
| Store protocol in NAMS | ⏳ PENDING | OpenClaw |
| Store protocol in MemPalace | ⏳ PENDING | OpenClaw |
| Gateway restart + verify skills | ⏳ PENDING | OpenClaw |
| Update MEMORY.md | ⏳ PENDING | OpenClaw |
| Daily note | ⏳ PENDING | OpenClaw |
| Cross-agent communication skill | ⏳ PENDING (Phase 2) | OpenClaw |
| Cross-agent onboarding skill | ⏳ PENDING (Phase 2) | OpenClaw |
| Install skills for other agents | ⏳ PENDING (Phase 2) | OpenClaw |
| Agent-specific integration | ⏳ PENDING (Phase 3) | Per-agent |
| Transport layer | ⏳ FUTURE (Phase 4) | TBD |

---

## Rationale

### Why a shared git repo instead of a file in an existing project?
- All agents can clone/pull/push without coupling to a specific project
- Git provides version control — audit trail of who changed what
- Future GitHub remote enables backup and collaboration
- Clean separation from project-specific work

### Why chmod 444 instead of convention?
- Filesystem-level enforcement — even if an agent tries to write, it fails
- Only Jason (root/owner) can `chmod 644` to edit, then `chmod 444` to re-lock
- Prevents rogue/hallucinated edits from any agent
- Defense in depth: convention (agents refuse to edit) + enforcement (filesystem refuses)

### Why NAMS/MemPalace identifiers?
- `CrossAgentProtocol:v1` is a well-known entity name any agent can query
- `MATCH (p:CrossAgentProtocol {name: 'CrossAgentProtocol:v1'}) RETURN p` returns the protocol metadata
- MemPalace drawer `cross-agent-protocol-v1` serves the same purpose for the palace
- Any new agent can be pointed to these identifiers and discover the full protocol

### Why per-session caching of PROTOCOL.md?
- Reading the same file on every interaction wastes tokens
- A session is a continuous work period — the protocol won't change mid-session
- If context is compacted or the session restarts, the cache is invalidated and must be re-read
- This balances token economy with protocol compliance

### Why document-based communication first?
- Transport layer (direct agent-to-agent messaging) requires:
  - A running server/process for each agent
  - Authentication between agents
  - Message routing and queuing
  - Error handling and retry logic
  - Significantly more infrastructure
- The document-based layer provides immediate value with minimal setup
- All agents already have file system access and MCP access
- Git provides version control and conflict resolution for free
- The protocol file ensures all agents behave correctly regardless of transport

### Why symlink Kiro's skills instead of copying?
- Kiro already symlinks from `~/.agents/skills/` (verified)
- All agents share the same skill pool — no duplication
- Updates to `~/.agents/skills/` propagate everywhere automatically
- This is the correct design — single source of truth for skills
