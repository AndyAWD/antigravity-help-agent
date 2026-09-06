# agy_help

[English](README.md) | [繁體中文](README.zh-TW.md)

Comprehensive knowledge base and help plugin for the entire Google Antigravity ecosystem, providing a dedicated Agent and Skill. It covers Antigravity CLI (`agy`), Antigravity IDE, Antigravity 2.0 Desktop Application, Antigravity Python SDK (`google-antigravity`), and the Customization System (Skills, Rules, Plugins, Hooks, Model Context Protocol (MCP), and Sidecars).

---

## Supported Products & Ecosystem Scope

This plugin provides authoritative guidance across the entire Google Antigravity product suite:

1. **Antigravity CLI (`agy`)**: Interactive terminal interface, CLI flags, slash commands, configuration schemas (`settings.json`), and agent lifecycle.
2. **Antigravity IDE**: Standalone AI-first development environment built on VS Code, Tab autocomplete & supercomplete, inline commands, sidebar chat panel, inline code lenses, and automated diagnostic fixing.
3. **Antigravity 2.0 Desktop Application**: Parallel desktop app, Chat Canvas, scheduled background tasks, HTML Auxiliary Pane (Subagents, Background Tasks, Artifacts, Files Changed, Terminals), and global/project-level permission management.
4. **Antigravity Python SDK (`google-antigravity`)**: Programmatic agent leasing, orchestration APIs, asynchronous streaming responses, Thought Delta interception, custom tools, and capability configurations (`CapabilitiesConfig`).
5. **Customization System**:
   - **Skills**: Procedural workflows (`SKILL.md`), reference documentation, and execution scripts.
   - **Rules**: Global and project-specific instructions (`GEMINI.md`, `AGENTS.md`, `.agents/rules/`).
   - **Plugins**: Packaging and distribution for agents, skills, hooks, and MCP servers.
   - **Hooks**: Lifecycle event automation scripts and trust manifests (`hooks.json`, `trusted_hooks.json`).
   - **Model Context Protocol (MCP)**: External tools and context server integrations (`mcp_config.json`).
   - **Sidecars**: Auxiliary containers and background support services.

---

## Component Architecture

This plugin consists of two primary components:

1. **Agent**: [`agents/agy_help/agent.md`](agents/agy_help/agent.md)
   - **Four-tier Fallback Zero-Hallucination Hierarchy**:
     - **Tier 1 (Structured Offline Reference)**: Primary lookup in local builtin guide references (`references/cli.md`, `references/ide.md`, `references/app.md`, `references/sdk.md`) and customization documentation (`docs/skills.md`, `docs/rules.md`, `docs/plugins.md`, `docs/hooks.md`, `docs/mcp_servers.md`, `docs/json_configs.md`).
     - **Tier 2 (Local Runtime & Environment Introspection)**: Safe command execution (`agy --help`, `agy help <subcmd>`, `agy <subcmd> --help`, `agy --version`, `agy plugin list`, `agy agents`, `agy models`, `agy changelog`, `agy mcp list`, `pip show google-antigravity`, `python3 -m pip show google-antigravity`), plus local configuration inspections (`~/.gemini/antigravity-cli/settings.json`, `.agents/`, `~/.gemini/config/plugins/`).
     - **Tier 3 (Live Official Documentation Fetching)**: Real-time queries to official documentation portals (`https://antigravity.google/docs` and related sub-documentation).
     - **Tier 4 (Strict Fact-Grounding & Honest Refusal)**: If unrecorded across all preceding tiers, explicitly state all verified channels and refuse to guess or fabricate commands.
   - **Command Execution Guardrails**: Strict whitelist for read-only diagnostic commands. Arbitrary shell commands or state-modifying actions are strictly prohibited.
   - Operates both as a standalone main agent and as a background subagent.

2. **Skill**: [`skills/agy_help/SKILL.md`](skills/agy_help/SKILL.md)
   - Activated via `/agy_help` slash command in any conversation session.
   - Provides step-by-step guidance aligned with the four-tier verification protocol.

---

## Installation & Management

### Validate Plugin
Run validation from the project root directory:
```bash
agy plugin validate .
```

### Install Plugin

#### Method A: Remote Installation via GitHub (Recommended)
```bash
agy plugin install https://github.com/AndyAWD/antigravity-help-agent
```

#### Method B: Local Installation
```bash
# From within the project directory:
agy plugin install .

# Or by absolute path:
agy plugin install /path/to/agy_help
```

### List Installed Plugins & Agents
```bash
agy plugin list
agy agents
```

---

## Usage

After installing or configuring `agy_help`, you can use it in several ways:

### 1. Switch Agent via Slash Command (`/agents`)

Inside an active interactive `agy` CLI session, type `/agents` to view and switch to the `agy_help` agent:

1. Run `> /agents` to see available agents:
   ```text
   ────────────────────────────────────────────────
   > /agents
   ────────────────────────────────────────────────
   Create New Agents
     Workspace: <workspace-path>
     Global: <global-path>

   Available Agents
   > ● default    Default agent
       agy_help   Google Antigravity Ecosystem Help Assistant
   ```

2. Select and switch to `agy_help`. The terminal will indicate the selection:
   ```text
   > /agents
     ⎿  Prepared selection: agy_help (will fork the current conversation on exit).
   ────────────────────────────────────────────────
   > 
   ────────────────────────────────────────────────
   ```
   Once switched, the current conversation will be managed by `agy_help`.

---

### 2. Instant In-Chat Skill Invocation (`/agy_help`)

To ask questions without switching your main conversation agent, use the `/agy_help` slash command directly:

```text
────────────────────────────────────────────────
> /agy_help How do I configure project-level sandbox permissions in Antigravity 2.0?
────────────────────────────────────────────────
```

Common query examples:
```text
/agy_help How to stream agent Thought Deltas using the Antigravity Python SDK?
/agy_help How does Tab autocomplete and supercomplete work in Antigravity IDE?
/agy_help How to configure custom lifecycle hooks?
/agy_help What are the available options and definition for the agy CLI --effort flag?
```

---

### 3. Launch Directly from Terminal (`agy --agent`)

Start a new CLI session using `agy_help` as the primary agent:

```bash
# Interactive conversation session
agy --agent agy_help

# Non-interactive single-prompt execution
agy --agent agy_help -p "Explain the core differences between Antigravity IDE and standard VS Code extensions"
```

---

### 4. Background Subagent Dispatch via Natural Language

When developing code in a main conversation, you can avoid context window pollution by delegating reference queries to `agy_help` as a background subagent:

```text
Please dispatch a background task to agy_help to look up how to configure Antigravity IDE code lenses, and report back with a summary.
```

The primary agent will run `agy_help` in the background, conduct the multi-tier lookup, and return grounded results without inflating your active context window.

---

## Project Directory Structure

```text
agy_help/
├── plugin.json               # Plugin manifest
├── LICENSE                   # MIT open-source license
├── README.md                 # Primary documentation (English)
├── README.zh-TW.md           # Documentation (Traditional Chinese)
├── agents/
│   └── agy_help/
│       └── agent.md          # Agent definition (YAML frontmatter, 4-tier fallback, guardrails)
└── skills/
    └── agy_help/
        └── SKILL.md          # Skill instructions (YAML frontmatter & workflow)
```

---

## License

This project is licensed under the [MIT License](LICENSE).
