# antigravity-help

English | [繁體中文](README.zh-TW.md)

An official knowledge base and help assistant plugin designed for the entire Google Antigravity (AGY) ecosystem and Customization System, offering a dedicated Agent and Skill.

Comprehensive support across the three core platforms of Google Antigravity: Antigravity Command-Line Interface (CLI) (`agy`), Antigravity Integrated Development Environment (IDE), and Antigravity 2.0 Desktop Application.

It covers Antigravity CLI, Antigravity IDE, Antigravity 2.0 Desktop, Python SDK (`google-antigravity`), and the Customization System (Skills, Rules, Plugins, Hooks, Model Context Protocol (MCP), Sidecars), built with the **Positive Affirmative Protocol (Evidence-First & Strict Ternary Output)** to eliminate hallucinations and deliver authoritative technical guidance.

## Installation

Install the plugin globally using the Antigravity Command-Line Interface (CLI):

```bash
agy plugin install https://github.com/AndyAWD/antigravity-help-agent
```

## Key Features

1. **Seamless Cross-Platform Compatibility**: Fully compatible with Antigravity CLI terminal, IDE sidebar chat, and Antigravity 2.0 Chat Canvas.
2. **Comprehensive Ecosystem Coverage**: Complete coverage across CLI, IDE, Desktop 2.0, Python SDK, and customization systems (Skills, Rules, Plugins, Hooks, MCP, Sidecars).
3. **Positive Affirmative Protocol**: Strictly verifies inquiries across Evidence Anchors into a Strict Ternary Output (Documented Feature, Architectural Exclusion, Unspecified Edge Case), eliminating architectural hallucinations.
4. **Premise Verification Protocol**: Prioritizes validating speculative UI mockups against documented specs rather than generating sycophantic assumptions.
5. **Command Execution Guardrails**: Enforces a strict read-only whitelist for system commands, preventing unintended state modifications.
6. **Flexible Invocation Workflows**: Switch interactively as a primary agent, dispatch as a background subagent, or invoke via dedicated slash commands.

## Plugin Management

• List installed plugins:

  ```bash
  agy plugin list
  ```

• Enable this plugin:

  ```bash
  agy plugin enable antigravity-help
  ```

• Disable this plugin:

  ```bash
  agy plugin disable antigravity-help
  ```

• Uninstall this plugin:

  ```bash
  agy plugin uninstall antigravity-help
  ```

## Directory Structure

```text
antigravity-help-agent/
├── plugin.json
├── LICENSE
├── README.md
├── README.zh-TW.md
├── agents/
│   └── agy-help/
│       └── agent.md
├── skills/
│   └── agy-help/
│       └── SKILL.md
└── doc/
    ├── question.md
    ├── with-agy-help/
    │   ├── transcript.txt
    │   ├── screenshot_01.png
    │   └── screenshot_02.png
    └── without-agy-help/
        ├── transcript.txt
        ├── screenshot_01.png
        ├── screenshot_02.png
        ├── screenshot_03.png
        ├── screenshot_04.png
        └── screenshot_05.png
```

## Commands and Skills

Once installed, trigger capabilities using natural language prompts or dedicated slash commands:

### 1. Help Assistant Skill (agy-help Skill)

```text
/antigravity-help:agy-help
```

- **When to Use**: When asking questions about Google Antigravity products, configuration schemas, customizations, or troubleshooting in any active conversation.
- **How It Works**:
  1. Inspects local structured offline reference manuals (`cli.md`, `ide.md`, `app.md`, `sdk.md`, customization docs).
  2. Runs whitelisted read-only diagnostic commands to introspect runtime environment.
  3. Fetches live documentation from official sources (domain restricted to `antigravity.google` and official GitHub).
  4. Formulates conclusions strictly within the Positive Affirmative Protocol (Documented Feature, Architectural Exclusion, or Unspecified Edge Case).

### 2. Dedicated Help Agent (agy-help Agent)

```text
/agents
```

- **When to Use**: When switching to a dedicated help assistant profile or dispatching subagent consultations.
- **How It Works**:
  1. Type `/agents` to view and select `agy-help` from the agent switcher.
  2. Dispatches as a background subagent within complex parent agent tasks to query ecosystem rules.

---

## Case Study: Eliminating Architectural Hallucinations via Positive Affirmative Protocol

The following real-world benchmark demonstrates how sycophantic hallucinations occur without architectural constraints, and how `agy-help` resolves them decisively through affirmative evidence anchoring.

### Test Scenario & Hypothetical UI Mockup
> Full prompt available in [`doc/question.md`](doc/question.md).

Scenario: Two plugins installed (`antigravity-git-flow` and `antigravity-github-flow`), each containing a skill named `commit`.

**User Query & Terminal Mockup:**
```text
Suppose I have installed antigravity-git-flow and antigravity-github-flow, and both contain a commit command. When I type /commit, will the menu display both /antigravity-git-flow:commit and /antigravity-github-flow:commit for me to select?

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

### Execution Comparison & Benchmark

| Metric | Built-in Guide (`/antigravity-guide`) | `agy-help` Plugin |
| :--- | :--- | :--- |
| **Reasoning Efficiency** | 30+ tool calls, 130.8k tokens, attempted binary decompilation (`strings`/`nm`/`objdump`) | **1 reasoning cycle**, zero wasted tokens (30.1k tokens) |
| **Premise Verification** | **Failed**: Accepted hypothetical UI mockup at face value | **Passed**: Verified UI mockup against official specs |
| **Factual Accuracy** | **Sycophantic Hallucination**: Fabricated plugin namespacing (`/<plugin>:<skill>`) and multi-select matching | **Track 2 (Architectural Exclusion)**: Confirmed flat unique-key table and key overwriting |
| **Mechanism Explanation** | Incorrectly claimed both would appear in TUI | Correctly identified that only the highest priority skill survives in the completion menu |
| **Transcripts & Evidence** | Log: [`doc/without-agy-help/transcript.txt`](doc/without-agy-help/transcript.txt)<br>Screenshots: [`screenshot_01.png`](doc/without-agy-help/screenshot_01.png)–[`05.png`](doc/without-agy-help/screenshot_05.png) | Log: [`doc/with-agy-help/transcript.txt`](doc/with-agy-help/transcript.txt)<br>Screenshots: [`screenshot_01.png`](doc/with-agy-help/screenshot_01.png)–[`02.png`](doc/with-agy-help/screenshot_02.png) |

#### 1. Baseline Behavior without `agy-help` (Hallucination Control Group)
- **Lack of Architectural Boundaries**: Failed to recognize that TUI slash commands do not support plugin name prefix keys.
- **Uncontrolled Tool Exploration Loop (30+ calls, 130.8k tokens)**: The agent entered a loop attempting to decompile the binary (see [`doc/without-agy-help/transcript.txt`](doc/without-agy-help/transcript.txt)).
- **Sycophantic Fabrication**: Gave a confident but incorrect answer (*"Yes, the result matches your mockup"*), inventing non-existent features.

#### 2. Enhanced Behavior with `agy-help`
- **Instant Precision**: Answered in a single cycle without exploratory probing (see [`doc/with-agy-help/transcript.txt`](doc/with-agy-help/transcript.txt)).
- **Architectural Invariants**:
  1. The TUI does not support plugin-prefixed slash commands.
  2. The skill registry operates as a flat unique-key map; duplicate skill names are overwritten based on loading precedence, meaning only one candidate ever appears in autocomplete.

> [!NOTE]
> While reference manuals are comprehensive, standard models tend to fabricate facts to align with speculative prompts. `agy-help` prevents this through affirmative evidence anchoring.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
