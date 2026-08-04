# Agent Updates — Current Status of All Agents

> **Last Updated**: 2026-08-04 15:10 CST  
> **Maintained by**: All agents (append your status, don't overwrite others)

---

## OpenClaw

**Status**: Active  
**Model**: nvidia/z-ai/glm-5.2 (current session)  
**Default Model**: nvidia/stepfun-ai/step-3.7-flash  
**Config**: `~/.openclaw/openclaw.json`  
**Workspace**: `~/.openclaw/workspace/`

### Current Capabilities
- **206 skills** in `~/.agents/skills/` (all 107 registered entries now `enabled: true`)
- **MCP Bridge**: `openclaw-mcp-bridge` v0.14.1 in router mode, 18 servers
- **NAMS Memory Plugin**: `openclaw-nams-memory` — autoRecall enabled, autoCapture enabled, observational enabled
- **Gateway**: Local mode, port 18789
- **Skills auto-discover** from `~/.agents/skills/` (personal agent skills, visible to all agents on this machine)

### Current Work
- Enabling all 107 registered skills (COMPLETED — all set to `enabled: true`)
- Deep-researching Kiro IDE for NAMS/MemPalace storage
- Creating shared-agent-docs repo and cross-agent protocol
- Full skills report generation in progress

### References
- Skills config: `~/.openclaw/openclaw.json` → `skills.entries`
- MCP config: `~/.openclaw/openclaw.json` → `plugins.entries."openclaw-mcp-bridge".config.servers`
- NAMS plugin: `~/.openclaw/extensions/nams-memory/`
- Memory: `~/.openclaw/workspace/MEMORY.md`

---

## OpenCode

**Status**: Active  
**Config**: `~/.config/opencode/opencode.jsonc`  
**Workspace**: `~/.config/opencode/`

### Current Capabilities
- **95 skills** in `~/.config/opencode/skills/`
- **33 agent definitions** in `~/.config/opencode/agents/`
- **18 MCP servers** (direct stdio connections — no router plugin)
- NAMS hooks active (nams-hooks.ts)
- Cortex-CS plugin active

### Current Work
- Skills absorption complete (7 skills absorbed from OpenCode into OpenClaw)
- Agent definitions fully synced (33 each in OpenCode and OpenClaw)

### References
- Agents: `~/.config/opencode/agents/`
- Skills: `~/.config/opencode/skills/`
- MCP: `~/.config/opencode/opencode.jsonc` → `mcp` section

---

## Hermes

**Status**: Active  
**Config**: `~/.hermes/config.yaml`  
**Workspace**: `~/.hermes/`

### Current Capabilities
- Python-based AI agent with personality modes (helpful, concise, technical, creative, etc.)
- **18 MCP servers** matching OpenCode's set
- **33 agent definitions** synced
- Default model: `tencent/hy3:free` via nous provider
- NAMS integration via hooks (planned — Python MemoryProvider plugin)
- Cortex-CS plugin port (planned — Plan C in hermes subplan)

### Current Work
- Phase 0 + Plan A complete (import + full capabilities)
- Plan C (NAMS + Cortex-CS Python plugin ports) NOT STARTED
- Needs `pip install agent-memory` for NAMS provider

### References
- Config: `~/.hermes/config.yaml`
- Skills: `~/.hermes/skills/`
- Agents: `~/.hermes/workspace/agents/`
- Subplan: `~/Documents/Github/JasonR27/docs/plans/2026-07-31-subplan-hermes.md`

---

## Cline

**Status**: Active (VSCode extension)  
**Config**: VSCode extension settings  
**Workspace**: Per-project `.clinerules/`

### Current Capabilities
- VSCode-based AI coding agent
- Agent conversion from OpenCode format to `.clinerules/agents/*.md` (planned)
- MCP support via VSCode MCP config
- GDS capabilities (cortex-cs, sm-engine) — planned for addition

### Current Work
- Plan B (add 11 MCP servers, convert 33 agents, verify GDS) — NOT STARTED
- Waiting for Phase 0 completion (done)

### References
- Subplan: `~/Documents/Github/JasonR27/docs/plans/2026-07-31-subplan-cline.md`

---

## Kiro

**Status**: Active  
**Config**: `~/.kiro/settings/mcp.json`  
**Workspace**: `~/.kiro/`

### Current Capabilities
- **Agentic IDE** by AWS (fork of VS Code, similar to Cursor)
- **18 MCP servers** configured in `~/.kiro/settings/mcp.json` (all enabled, all matching OpenCode's set)
- **Skills**: Symlinked from `~/.agents/skills/` (shared with OpenClaw and all other agents)
- **Hooks**: NAMS session-start, tool-call, and user-prompt hooks configured (JSON-based, similar to OpenCode but simpler)
- **Hook scripts**: `nams_session_manager.py` in `~/.kiro/hooks/scripts/`
- **Steering**: Custom rules via `~/.kiro/steering/core-guidelines.md` (mirrors OpenClaw's core-guidelines.md)
- **Powers**: Registry directory exists but empty (`~/.kiro/powers/registries/`)
- **Sessions**: Stored in `~/.kiro/sessions/<workspace-hash>/sess_<uuid>/`
- **Permissions**: MCP tool-level allowlist in `~/.kiro/settings/permissions.yaml`
- **Extensions**: VS Code-compatible extensions (github, gemini, neo4j, playwright, jupyter, etc.)
- **Models**: Claude Opus 4.8 or Auto (mix of frontier models)
- **Agent Modes**: "vibe" (freeform), spec-driven (structured requirements → architecture → tasks)
- **Autopilot**: Autonomous large task execution
- **Specs**: Structured specifications that break down requirements into implementation plans
- **Custom Agents**: Supported (see Kiro docs at kiro.dev/docs/custom-agents/)
- **Trust Migration**: Completed — MCP permissions migrated

### Architecture Details

**Kiro is a VS Code fork** by AWS (Amazon). Key architectural points:
- **Based on VS Code**: Full VS Code extension compatibility, imports VS Code settings during setup
- **Agent System**: Built-in agent with "vibe" mode (freeform coding) and spec-driven mode (structured)
- **Hooks System**: JSON-based hooks in `~/.kiro/hooks/` — triggers: `SessionStart`, `PreToolUse`, `UserPromptSubmit`
- **Steering System**: Markdown files in `~/.kiro/steering/` that guide agent behavior (equivalent to OpenClaw's AGENTS.md)
- **MCP Integration**: Native MCP support via `~/.kiro/settings/mcp.json` — both local (stdio) and remote (HTTP) servers
- **Skills System**: Symlinks to `~/.agents/skills/` (shared pool — same skills as OpenClaw, OpenCode, etc.)
- **Powers System**: On-demand domain-specific context and tools (registry currently empty — needs population)
- **Session Management**: Session-based with workspace hashing, per-session message logs (JSONL format)
- **Snapshots**: File snapshots stored per-session for rollback capability
- **Permissions**: YAML-based tool-level permission system

### NAMS Integration
- **Hook files**: 3 JSON hooks (session-start, tool-call, user-prompt) — all return "allow" permission decisions
- **Hook script**: `nams_session_manager.py` — handles session mapping and NAMS MCP calls
- **Workspace ID**: Same as all agents: `1495e133-43c3-460b-a1a0-b97eaa45b943`
- **Session map**: `~/.kiro/hooks/session-map.json` and per-workspace session maps

### MCP Server List (18 servers, all enabled)
1. neo4j-memory (AuraDB) 2. neo4j-official (AuraDB) 3. neo4j-cypher (AuraDB)
4. neo4j-memory-local 5. neo4j-official-local 6. neo4j-cypher-local
7. sequentialthinking 8. mempalace 9. playwright
10. brave-search 11. context7 12. video-transcriber-mcp
13. github 14. pixelrag 15. youtube_transcript
16. nams-memory 17. cortex-cs 18. sm-engine

### Current Work
- Skills symlinked from shared `~/.agents/skills/` pool
- NAMS hooks configured and active
- Steering file mirrors core-guidelines
- Powers registry empty — needs population
- Custom agents not yet configured

### References
- Config: `~/.kiro/settings/mcp.json`
- Permissions: `~/.kiro/settings/permissions.yaml`
- Steering: `~/.kiro/steering/core-guidelines.md`
- Hooks: `~/.kiro/hooks/`
- Skills: `~/.kiro/skills/` (symlinks to `~/.agents/skills/`)
- Sessions: `~/.kiro/sessions/`
- GitHub: https://github.com/kirodotdev/Kiro
- Docs: https://kiro.dev/docs/

---

## Cross-Agent Status

### MCP Parity
All 5 agents have access to the same 18 MCP servers. ✅ COMPLETE

### Skills Parity
- `~/.agents/skills/` shared pool: **206 skills** (symlinked by Kiro, auto-discovered by OpenClaw)
- OpenCode: 95 skills in its own directory (7 absorbed into OpenClaw)
- All agents can access the shared pool via symlinks or auto-discovery

### Agent Definitions
33 agent definitions synced across OpenCode, OpenClaw, and Hermes. ✅ COMPLETE

### NAMS Integration
- OpenClaw: ✅ Plugin active (autoRecall + autoCapture + observational)
- OpenCode: ✅ Hooks active (nams-hooks.ts)
- Kiro: ✅ Hooks active (JSON-based, nams_session_manager.py)
- Hermes: ⚠️ Hooks planned (Python MemoryProvider — not yet implemented)
- Cline: ⚠️ Not yet configured

### Shared Docs
- ✅ Repo created at `~/Documents/Github/JasonR27/shared-agent-docs/`
- ✅ PROTOCOL.md (immutable) written
- ✅ AGENT_UPDATES.md (this file) written
- `sessions/` directory ready for coworking session files
- `skills/` directory ready for cross-agent skill documentation
