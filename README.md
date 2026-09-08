# agy-help

[English](README.md) | [繁體中文](README.zh-TW.md)

Comprehensive knowledge base and help assistant plugin for the entire Google Antigravity ecosystem and Customization System, providing a dedicated Agent and Skill. Built with the **Positive Affirmative Protocol (Evidence-First & Strict Ternary Output)**, it delivers zero-hallucination technical specifications, architecture guides, and diagnostic support across Antigravity CLI (`agy`), Antigravity IDE, Antigravity 2.0 Desktop Application, Antigravity Python SDK (`google-antigravity`), and customizations (Skills, Rules, Plugins, Hooks, MCP, and Sidecars).

---

## Installation & Management

### Install Plugin

#### Method A: Remote Installation via GitHub (Recommended)
```bash
agy plugin install https://github.com/andyawd/antigravity-help-agent
```

#### Method B: Local Installation
```bash
# From within the project directory:
agy plugin install .

# Or by specifying the path:
agy plugin install /path/to/antigravity-help-agent
```

### List Installed Plugins & Agents
```bash
agy plugin list
agy agents
```

---

## Supported Ecosystem Scope

Authoritative coverage across the entire Google Antigravity product suite:

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

1. **Agent**: [`agents/agy-help/agent.md`](agents/agy-help/agent.md)
   - Operates as both an interactive main agent and a background subagent.
   - Implements the Positive Affirmative Protocol, Premise Verification Protocol, and read-only diagnostic command guardrails.
   - Inherits MCP server capabilities (`inheritMcp: true`).

2. **Skill**: [`skills/agy-help/SKILL.md`](skills/agy-help/SKILL.md)
   - Invoked via `/agy-help` slash command in any conversation session without switching your active agent.
   - Follows the identical Evidence-First and Strict Ternary Output workflow.

---

## Usage Modes

### 1. Switch Agent via Slash Command (`/agents`)

Inside an interactive `agy` CLI session, type `/agents` to view and switch to the `agy-help` agent:

1. Execute `> /agents` to list available agents:
   ```text
   ────────────────────────────────────────────────
   > /agents
   ────────────────────────────────────────────────
   Create New Agents
     Workspace: <workspace-path>
     Global: <global-path>

   Available Agents
   > ● default    Default agent
       agy-help   Google Antigravity Ecosystem Help Assistant
   ```

2. Select and switch to `agy-help`. The terminal will indicate the selection:
   ```text
   > /agents
     ⎿  Prepared selection: agy-help (will fork the current conversation on exit).
   ────────────────────────────────────────────────
   > 
   ────────────────────────────────────────────────
   ```
   Once switched, `agy-help` leads the active session for deep technical auditing and specification lookup.

---

### 2. Instant In-Chat Skill Invocation (`/agy-help`)

Ask targeted questions without switching your main conversation agent:

```text
────────────────────────────────────────────────
> /agy-help How do I configure project-level sandbox permissions in Antigravity 2.0?
────────────────────────────────────────────────
```

Common query examples:
```text
/agy-help How to stream agent Thought Deltas using the Antigravity Python SDK?
/agy-help How does Tab autocomplete and supercomplete work in Antigravity IDE?
/agy-help How to configure custom lifecycle hooks and trusted_hooks.json?
/agy-help What are the available options and definition for the agy CLI --effort flag?
```

---

### 3. Launch Directly from Terminal (`agy --agent`)

Start a new CLI session directly with `agy-help`:

```bash
# Interactive conversation session
agy --agent agy-help

# Non-interactive single-prompt execution
agy --agent agy-help -p "Explain the core differences between Antigravity IDE and standard VS Code extensions"
```

---

### 4. Background Subagent Dispatch via Natural Language

Delegate reference lookup to `agy-help` as a background subagent during coding sessions to prevent context window inflation:

```text
Please dispatch a background task to agy-help to look up how to configure Antigravity IDE code lenses, and report back with a summary.
```

---

## Project Directory Structure

```text
antigravity-help-agent/
├── plugin.json               # Plugin manifest
├── LICENSE                   # MIT open-source license
├── README.md                 # Primary documentation (English)
├── README.zh-TW.md           # Documentation (Traditional Chinese)
├── doc/                      # Case study raw transcripts & visual evidence
│   ├── question.md           # Original test prompt & hypothetical mockup
│   ├── with-agy-help/        # Test artifacts with agy-help enabled (Ground truth)
│   │   ├── transcript.txt    # Full terminal log (30.1k tokens, 1 reasoning cycle)
│   │   ├── screenshot_01.png # Evidence retrieval & protocol execution
│   │   └── screenshot_02.png # Architectural exclusion analysis output
│   └── without-agy-help/     # Test artifacts with standard guide (Hallucination)
│       ├── transcript.txt    # Full terminal log (130.8k tokens, 30+ tool calls)
│       ├── screenshot_01.png # Initial tool inspection loop
│       ├── screenshot_02.png # Binary disassembly attempt (objdump/nm)
│       ├── screenshot_03.png # Task loop & process management
│       ├── screenshot_04.png # Temporary plugin creation attempt
│       └── screenshot_05.png # Fabricated namespace & autocomplete response
├── agents/
│   └── agy-help/
│       └── agent.md          # Agent definition (YAML frontmatter, protocol, guardrails)
└── skills/
    └── agy-help/
        └── SKILL.md          # Skill instructions (YAML frontmatter & workflow)
```

---

## Key Protocols & Guardrails

### Positive Affirmative Protocol (Evidence-First Verification)
`agy-help` enforces an evidence-first closed-loop audit protocol before producing any answer:

1. **Mandatory Evidence Anchor**:
   - **Official Verbatim Citation**: Primary search in local built-in manuals (`builtin/skills/antigravity_guide/references/` and `builtin/skills/agy-customizations/docs/`) or official live domains (`antigravity.google` with `domain: antigravity.google` search constraint, and `github.com/google-antigravity`). Strictly rejects unverified third-party blogs or forums.
   - **Local Physical State Inspection**: Validates configurations (`settings.json`), registered `<skills>` structures, and physical plugin directory hierarchies using `view_file` or `list_dir`.

2. **Strict Ternary Output Mapping**:
   Every response strictly maps to one of three mutually exclusive states:
   - **Track 1: Documented Feature (已證實支援)** — Explicitly backed by official verbatim specifications. Quotes exact syntax and standard usage.
   - **Track 2: Architectural Exclusion (架構實質互斥)** — Disproven by underlying data structures (e.g., flat key override collision, absence of prefix namespaces). Explains exact architectural constraints.
   - **Track 3: Unspecified Edge Case (邊界未規範)** — Unrecorded in documentation and unsupported by physical mechanisms. Emits the standard declaration: *"This scenario has no defined behavior in official specification manuals and is considered an Undefined Behavior / Unspecified Edge Case."*

3. **Premise Verification Protocol**:
   When user prompts include hypothetical mockups (e.g., ASCII UI, assumed default option lists, imagined workflows), `agy-help` never assumes their existence. It first verifies the premise against official documentation and rejects ungrounded assumptions outright.

4. **Command Execution Guardrails**:
   Restricts `run_command` strictly to read-only diagnostics (`agy --help`, `agy help <subcommand>`, `agy <subcommand> --help`, `agy --version` / `agy version`, `agy agents`, `agy plugin list`, `agy models`, `agy changelog`, `agy mcp list`, `pip show google-antigravity` / `python3 -m pip show google-antigravity`). Modifying system states is strictly prohibited.

---

## Case Study: Eliminating Hallucinations in Architecture & UI Queries

Here is a concrete test case from plugin development workflows demonstrating the exact hallucination that occurs when relying solely on unconstrained guidance, contrasted with the zero-hallucination precision of `agy-help`.

### Test Scenario & Hypothetical UI Mockup
> Full test prompt available in [`doc/question.md`](doc/question.md).

The test scenario involves having two plugins installed (`antigravity-git-flow` and `antigravity-github-flow`), both providing a skill named `commit`.

**User Prompt & Terminal Mockup:**
```text
Suppose I have installed these two plugins, antigravity-git-flow and antigravity-github-flow, both containing a commit command. When I type /commit, will both /antigravity-git-flow:commit and /antigravity-github-flow:commit appear below for me to choose from?

      ▄▀▀▄        Antigravity CLI 1.1.27
     ▀▀▀▀▀▀       anandydy529@gmail.com (Google AI Pro)
    ▀▀▀▀▀▀▀▀      Gemini 3.8 Flash (High)
   ▄▀▀    ▀▀▄     ~
  ▄▀▀      ▀▀▄

────────────────────────────────────
> /commit
────────────────────────────────────
> /antigravity-git-flow:commit
  /antigravity-github-flow:commit
```

---

### Comparison & Results

| Evaluation Metric | Built-in Guide (`/antigravity-guide`) | `agy-help` Plugin |
| :--- | :--- | :--- |
| **Reasoning Efficiency** | 30+ tool calls, 130.8k tokens consumed (attempted binary reverse-engineering via `strings`/`nm`/`objdump`) | **1 reasoning cycle**, direct answer with minimal token overhead (30.1k tokens) |
| **Premise Verification** | **Failed**: Blindly accepted hypothetical UI mockup as ground truth | **Passed**: Enforced Premise Verification Protocol; audited UI claims first |
| **Output Integrity** | **Sycophantic Hallucination**: Fabricated non-existent "Plugin Namespacing" (`/<plugin>:<skill>`) and "Autocomplete Matching" | **Track 2 (Architectural Exclusion)**: Strictly explained flat unique-key table collision and key overwriting |
| **System Mechanics Explained** | Incorrectly affirmed both candidates would appear in TUI | Accurately proved only one candidate will ever appear based on loading precedence |
| **Raw Artifacts & Logs** | Full log: [`doc/without-agy-help/transcript.txt`](doc/without-agy-help/transcript.txt)<br>Visuals: [`screenshot_01.png`](doc/without-agy-help/screenshot_01.png)–[`05.png`](doc/without-agy-help/screenshot_05.png) | Full log: [`doc/with-agy-help/transcript.txt`](doc/with-agy-help/transcript.txt)<br>Visuals: [`screenshot_01.png`](doc/with-agy-help/screenshot_01.png)–[`02.png`](doc/with-agy-help/screenshot_02.png) |

#### 1. Execution with Built-in `/antigravity-guide` (Hallucination Control Group)
- **Lack of architectural boundary awareness**: The model failed to recognize that Terminal User Interface (TUI) slash commands do not support plugin names as prefix keys.
- **Runaway inspection loops (30+ tool calls & 130.8k tokens)**: The agent entered an extended inspection loop, attempting to reverse-engineer the local `agy` binary using `strings`, `nm`, and `objdump` ([`doc/without-agy-help/transcript.txt`](doc/without-agy-help/transcript.txt)).
- **Sycophantic hallucination fabricating mechanisms**: Returned a confident but fabricated affirmative answer: *"Yes, the display result will be exactly as shown in your mockup."* It fabricated two non-existent features:
  - Fabricated **"Plugin Namespacing"**, claiming the slash command syntax is `/<plugin-name>:<skill-name>`.
  - Fabricated **"Autocomplete Matching"**, claiming the TUI engine matches colons and displays both prefixed commands simultaneously.

#### 2. Execution with `agy-help` (Positive Affirmative Protocol)
- **Immediate precision within 1 reasoning cycle**: Without executing exploratory binary disassemblies, directly answered that only one command will be displayed ([`doc/with-agy-help/transcript.txt`](doc/with-agy-help/transcript.txt)).
- **Strict adherence to architectural invariants**:
  1. The CLI TUI does not support plugin-prefixed slash commands.
  2. Skill registration operates on a flat unique-key dictionary. When duplicate names occur, key overwriting applies based on loading precedence, meaning only one entry remains and only one candidate can ever appear in the autocomplete list.

> [!NOTE]
> While built-in reference documentation is comprehensive, standard models tend to hallucinate to please user assumptions when faced with plausible-looking UI mockups or unrecorded edge cases. `agy-help` establishes negative architectural constraints and strict evidence verification to eliminate this class of hallucinations entirely.

---

## License

This project is licensed under the [MIT License](LICENSE).
