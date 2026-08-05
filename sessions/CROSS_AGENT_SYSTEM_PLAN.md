# Cross-Agent Communication & Coworking System — Master Plan

> **Created**: 2026-08-04  
> **Author**: OpenClaw (for Jason)  
> **Status**: Phases 1 & 2 complete, pausing for other work  
> **GitHub**: https://github.com/JasonR27/shared-agent-docs  
> **Prior plans referenced**:  
> - `docs/plans/2026-07-31-subplan-openclaw.md`  
> - `docs/plans/2026-07-31-subplan-hermes.md`  
> - `docs/plans/2026-07-31-subplan-cline.md`  
> - `SUBPLAN_ABSORB_OPCODE_SKILLS.md` (superseded by this plan)

---

## Core Objective

Build a cross-agent communication and coworking system for all AI agents in the JasonR27 ecosystem (OpenClaw, OpenCode, Hermes, Cline, Kiro, and future agents) enabling:

1. A shared immutable protocol all agents follow
2. Current status visibility via a shared updates file
3. Coordination via session files in a git-controlled repo
4. Shared memory (NAMS/Neo4j and MemPalace) storing cross-agent context
5. Skill discoverability across agents
6. A future transport layer for direct agent-to-agent messaging

---

## Architecture

```
Layer 1: Document-Based Communication (COMPLETE)
├── shared-agent-docs/ (git repo → GitHub)
│   ├── PROTOCOL.md          (IMMUTABLE — chmod 444)
│   ├── AGENT_UPDATES.md     (all agents append status)
│   ├── sessions/            (per-coworking-session files)
│   │   └── TEMPLATE.md      (coworking session template)
│   └── skills/             (cross-agent skill documentation)
│       └── SKILLS_FULL_REPORT.md (208 skills, 10 categories)
│
├── NAMS/Neo4j (shared memory graph)
│   └── CrossAgentProtocol:v1 entity (well-known identifier)
│
└── MemPalace (shared contextual memory)
    └── CrossAgentProtocol wing (146 drawers, searchable)

Layer 2: Transport Layer (FUTURE — not started)
├── Agent-to-agent direct messaging
├── Prompt injection across agents
└── Data streaming between agents
```

---

## Phase 1: Document-Based Communication ✅ COMPLETE

### 1.1 Shared Docs Repo
- [x] Created `~/Documents/Github/JasonR27/shared-agent-docs/` as a git repo
- [x] Structure: `PROTOCOL.md`, `AGENT_UPDATES.md`, `sessions/`, `skills/`
- [x] GitHub remote created and pushed: https://github.com/JasonR27/shared-agent-docs
- [x] 5 commits on `master` branch:
  - `7561855` — Initial shared-agent-docs repo structure
  - `b817870` — PROTOCOL.md (immutable, chmod 444) + AGENT_UPDATES.md
  - `9fabf34` — Session file + full 206-skills report
  - `3945c38` — Updated skills report with proper frontmatter descriptions
  - `75c7f46` — Phase 2: skills, directives, NAMS+MemPalace storage

### 1.2 Immutable Protocol File
- [x] Written `PROTOCOL.md` (11KB, 9 sections):
  - §1 Purpose — what this protocol governs
  - §2 Agent registry — all 5 agents with config paths
  - §3 Shared infrastructure — docs repo, NAMS, MemPalace
  - §4 Rules — message format (§4.3), task assignment format (§4.4), file editing, shared memory, anti-conflict
  - §5 Mandatory behaviors — before/during/after cross-agent work
  - §6 Memory storage — NAMS entity schema, MemPalace drawer schema
  - §7 Extensibility — adding agents, versioning, future transport layer
  - §8 Violations — revert, report, notify, re-read
  - §9 Quick reference — file paths, identifiers, commands
- [x] `chmod 444` applied — filesystem-enforced read-only
- [x] Committed to git

### 1.3 Agent Updates File
- [x] Written `AGENT_UPDATES.md` with status for all 5 agents:
  - **OpenClaw**: 208 skills, MCP bridge (router mode), NAMS plugin (autoRecall+autoCapture+observational)
  - **OpenCode**: 33 agent definitions, NAMS hooks active
  - **Hermes**: 18 MCPs configured, Phase 0+A done
  - **Cline**: VSCode extension, Plan B pending
  - **Kiro**: Deep-research findings, 18 MCPs, hooks + steering configured
- [x] Cross-agent status matrix (MCP parity, skills parity, NAMS integration)
- [x] Phase status tracking (Phase 1+2 ✅, Phase 3+4 ⏳)
- [x] Protocol directive locations for all 5 agents

### 1.4 Session Infrastructure
- [x] `sessions/TEMPLATE.md` — coworking session template (message format, roles, timeline, decisions, files, NAMS entities, MemPalace drawers)
- [x] `sessions/2026-08-04-skills-and-protocol-setup.md` — this session's plan

### 1.5 Skills Documentation
- [x] `skills/SKILLS_FULL_REPORT.md` — 208 skills categorized into 10 categories with YAML frontmatter descriptions:
  - 41 NVIDIA/NeMo
  - 31 Neo4j/Graph
  - 30 Thinking/Collaboration
  - 27 Azure
  - 13 Code/Testing
  - 5 Vercel
  - 4 Documentation
  - 3 Memory/Cortex
  - 2 MCP
  - 50 Other
- [x] `~/.openclaw/workspace/SKILLS_SUMMARY.md` — summary table (Name, Category, Description, Trigger)

### 1.6 Shared Memory Storage
- [x] **NAMS**:
  - `CrossAgentProtocol:v1` entity stored (label: `CrossAgentProtocol`)
  - 5 Agent entities stored (OpenClaw, OpenCode, Hermes, Cline, Kiro)
  - Kiro IDE Research observation stored
  - Relationship: OpenClaw `PARTICIPATES_IN` CrossAgentProtocol:v1
  - ⚠️ Known issue: entity store API returns "Unknown" names — properties may not map correctly
- [x] **MemPalace**:
  - `CrossAgentProtocol` wing created (mempalace.yaml + entities.json)
  - 146 drawers filed across 6 files in shared-agent-docs repo
  - Searchable: `search "CrossAgentProtocol"` returns PROTOCOL.md results
  - Rooms: general (PROTOCOL.md), sessions (session files), skills (SKILLS_FULL_REPORT.md)

### 1.7 Skills Registration
- [x] All 107 existing registered skills flipped to `enabled: true` in openclaw.json
- [x] 2 new skills added: `cross-agent-communication`, `cross-agent-onboarding`
- [x] **109 total entries**, all `enabled: true`, 0 disabled
- [x] 208 skills total in `~/.agents/skills/` (auto-discoverable)
- [x] 3 empty skill directories deleted: session-continuity, session-wrap, ship-pipeline

### 1.8 Documentation Updates
- [x] `MEMORY.md` updated with:
  - §2.9 Cross-Agent Communication System
  - §2.10 Kiro IDE Research
  - §2.11 Skills Registration
  - Updated active projects and infrastructure sections
- [x] `memory/2026-08-04.md` daily note written
- [x] Gateway restarted and verified healthy at port 18789

---

## Phase 2: Cross-Agent Skills ✅ COMPLETE

### 2.1 Cross-Agent Communication Skill
- [x] Created `~/.agents/skills/cross-agent-communication/SKILL.md` (4.2KB)
- [x] Content: when to use, agent registry, before/during/after workflow, message format, task format, file locations, NAMS queries, MemPalace queries, hard rules
- [x] Registered in openclaw.json (`enabled: true`)

### 2.2 Cross-Agent Onboarding Skill
- [x] Created `~/.agents/skills/cross-agent-onboarding/SKILL.md` (5.0KB)
- [x] Content: 10-step onboarding checklist (discover protocol → read docs → clone repo → post intro → register in NAMS → create MemPalace drawer → verify MCPs → add directive → commit → verify), existing agent status table
- [x] Registered in openclaw.json (`enabled: true`)

### 2.3 Protocol Directives for All Agents
- [x] **OpenClaw**: `~/.agents/skills/cross-agent-communication/SKILL.md` (auto-discovered)
- [x] **OpenCode**: `~/.config/opencode/skills/cross-agent-communication/SKILL.md`
- [x] **Hermes**: `~/.hermes/skills/cross-agent-communication/SKILL.md`
- [x] **Cline**: `~/.clinerules/agents/cross-agent-communication.md`
- [x] **Kiro**: `~/.kiro/steering/cross-agent-communication.md`

Each directive instructs the agent to:
1. Read PROTOCOL.md before any cross-agent interaction
2. Pull shared docs from GitHub
3. Query NAMS for `CrossAgentProtocol:v1`
4. Use structured message format
5. Update AGENT_UPDATES.md after work
6. Commit and push

---

## Phase 3: Agent-Specific Integration ⏳ PENDING

> Not started — pausing for other work as of 2026-08-04.

### 3.1 OpenCode Integration
- [ ] Add PROTOCOL.md read directive to OpenCode's main AGENTS.md
- [ ] Test: OpenCode can find and follow the protocol

### 3.2 Hermes Integration
- [ ] Implement NAMS MemoryProvider plugin (Python)
- [ ] Add cross-agent steering to Hermes config
- [ ] Test: Hermes can read shared docs, query NAMS

### 3.3 Cline Integration
- [ ] Add 11 MCP servers to Cline's config (currently missing)
- [ ] Convert agent definitions to `.clinerules/agents/` format
- [ ] Test: Cline can read shared docs, query NAMS

### 3.4 Kiro Integration
- [ ] Populate Kiro powers registry with cross-agent power
- [ ] Configure custom agents in Kiro for cross-agent work
- [ ] Test: Kiro can read shared docs, query NAMS

---

## Phase 4: Transport Layer 🔮 FUTURE

> Not started — design phase only. Will be built on top of Layer 1 and must comply with all rules in PROTOCOL.md.

### 4.1 Design
- [ ] Agent-to-agent messaging transport (likely HTTP-based)
- [ ] Prompt injection protocol (agent as user to another agent)
- [ ] Data streaming protocol
- [ ] Security model: authentication, authorization, scope

### 4.2 Implementation
- [ ] Build transport server
- [ ] Agent registration and discovery
- [ ] Message routing and queuing
- [ ] Audit logging to NAMS

### 4.3 Integration
- [ ] Comply with all Layer 1 rules
- [ ] Version bump to protocol v2.0.0
- [ ] Update all agent directives

---

## Known Issues

| Issue | Impact | Status |
|-------|--------|--------|
| NAMS entity store returns "Unknown" names | Entities stored but properties may not map correctly | ⚠️ Needs investigation |
| NAMS stats unchanged at 200 nodes | autoCapture may not be firing hooks | ⚠️ Needs investigation |
| MemPalace MCP can't be invoked directly | Can only use CLI, not MCP tool calls | ⚠️ Workaround: use CLI |
| `openclaw.json` skill entries don't accept `source` key | Gateway rejects config with `source` field | ✅ Fixed (removed key) |

---

## Key Identifiers (How Any Agent Finds the Protocol)

| System | Identifier | Query |
|--------|-----------|-------|
| **NAMS** | `CrossAgentProtocol:v1` | `MATCH (p:CrossAgentProtocol {name: 'CrossAgentProtocol:v1'}) RETURN p` |
| **MemPalace** | `CrossAgentProtocol` wing | `search "CrossAgentProtocol"` |
| **File** | `PROTOCOL.md` | `~/Documents/Github/JasonR27/shared-agent-docs/PROTOCOL.md` |
| **GitHub** | Remote repo | https://github.com/JasonR27/shared-agent-docs |

---

## Task Status Summary

| Task | Status | Owner |
|------|--------|-------|
| Skills enabled (109 → all enabled:true) | ✅ DONE | OpenClaw |
| Shared docs repo created + pushed to GitHub | ✅ DONE | OpenClaw |
| PROTOCOL.md written + locked (chmod 444) | ✅ DONE | OpenClaw |
| AGENT_UPDATES.md written with all 5 agents | ✅ DONE | OpenClaw |
| Kiro deep research | ✅ DONE | OpenClaw |
| Full skills report (208 skills) | ✅ DONE | OpenClaw |
| Session template (TEMPLATE.md) | ✅ DONE | OpenClaw |
| Store protocol in NAMS | ✅ DONE | OpenClaw |
| Store protocol in MemPalace | ✅ DONE | OpenClaw |
| Gateway restart + verify skills | ✅ DONE | OpenClaw |
| Update MEMORY.md | ✅ DONE | OpenClaw |
| Daily note (2026-08-04.md) | ✅ DONE | OpenClaw |
| Cross-agent communication skill | ✅ DONE | OpenClaw |
| Cross-agent onboarding skill | ✅ DONE | OpenClaw |
| Protocol directives for all 5 agents | ✅ DONE | OpenClaw |
| Agent-specific integration (Phase 3) | ⏳ PENDING | Per-agent |
| NAMS entity name fix | ⏳ PENDING | OpenClaw |
| Transport layer (Phase 4) | 🔮 FUTURE | TBD |

---

## Rationale

### Why a shared git repo?
- All agents can clone/pull/push without coupling to a specific project
- Git provides version control — audit trail of who changed what
- GitHub remote enables backup and collaboration
- Clean separation from project-specific work

### Why chmod 444?
- Filesystem-level enforcement — even if an agent tries to write, it fails
- Only Jason can `chmod 644` to edit, then `chmod 444` to re-lock
- Defense in depth: convention (agents refuse) + enforcement (filesystem refuses)

### Why NAMS/MemPalace identifiers?
- Any agent can query `CrossAgentProtocol:v1` in NAMS and discover the protocol
- MemPalace wing `CrossAgentProtocol` serves the same purpose for the palace
- New agents can be pointed to these identifiers and find everything they need

### Why document-based communication first?
- Transport layer requires significantly more infrastructure (servers, auth, routing)
- Document-based layer provides immediate value with minimal setup
- All agents already have filesystem and MCP access
- Git provides version control and conflict resolution for free
