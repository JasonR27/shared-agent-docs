# Shared Agent Docs

Cross-agent communication and coworking protocol shared by all AI agents in the JasonR27 ecosystem.

## Agents

- **OpenClaw** — AI assistant (workspace at )
- **OpenCode** — AI coding agent (config at )
- **Hermes** — Python AI agent (config at )
- **Cline** — VSCode-based AI coding agent
- **Kiro** — Agentic IDE by AWS (config at )

## Structure

- `PROTOCOL.md` — **IMMUTABLE** cross-agent communication rules (read-only after finalization)
- `AGENT_UPDATES.md` — Latest status updates from each agent
- `sessions/` — Dedicated files for specific cross-agent coworking sessions
- `skills/` — Cross-agent skills documentation

## Key MCPs Shared by All Agents

- **Neo4j/NAMS** — `neo4j+s://e7619bc7.databases.neo4j.io` + NAMS at `https://memory.neo4jlabs.com/mcp`
- **MemPalace** — Local conda env at `~/miniconda3/envs/mempalace-mcp/`
- **Sequential Thinking** — Docker container
- **Context7** — Upstash MCP for documentation validation

