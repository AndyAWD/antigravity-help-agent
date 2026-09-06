# agy_help

Google Antigravity 全生態系與客製化體系知識庫說明外掛程式（Plugin），提供專屬的代理（Agent）與技能（Skill），涵蓋命令列介面（CLI，`agy`）、整合開發環境（IDE）、Antigravity 2.0 桌面應用程式（Desktop Application）、Python 軟體開發套件（SDK，`google-antigravity`），以及客製化體系（技能（Skills）、規則（Rules）、外掛程式（Plugins）、掛鉤（Hooks）、模型上下文通訊協定（Model Context Protocol, MCP）、附掛容器（Sidecars）等）的完整指南與架構解答。

---

## 支援產品與生態系範圍

本外掛程式涵蓋 Google Antigravity 全產品線：

1. **Antigravity 命令列介面（CLI，`agy`）**：終端機互動式介面、啟動旗標參數、斜線指令、設定檔（`settings.json`）與生命週期。
2. **Antigravity 整合開發環境（IDE）**：以 VS Code 為基礎的獨立 AI 開發環境、Tab 自動補全（Autocomplete & Supercomplete）、行內指令（Inline Command）、側邊欄對話面板、行內程式碼透鏡（Inline Code Lenses）與診斷自動修復。
3. **Antigravity 2.0 桌面應用程式（Desktop Application）**：平行桌面應用程式、對話畫布（Chat Canvas）、排程背景任務（Scheduled Tasks）、HTML 輔助面板（Auxiliary Pane：Subagents、Background Tasks、Artifacts、Files Changed、Terminals）、全域與專案層級安全權限控制。
4. **Antigravity Python 軟體開發套件（SDK，`google-antigravity`）**：Python 程式化代理租賃、編排 API、非同步串流回應、思維鏈增量（Thought Delta）攔截、自訂工具與能力設定（`CapabilitiesConfig`）。
5. **客製化體系（Customization System）**：
   - **技能（Skills）**：結構化指引檔（`SKILL.md`）、子手冊與執行腳本。
   - **規則（Rules）**：全域與專案特定工作流程規範（`GEMINI.md`、`AGENTS.md`、`.agents/rules/`）。
   - **外掛程式（Plugins）**：打包與發布代理、技能、掛鉤與 MCP 伺服器的擴充套件。
   - **掛鉤（Hooks）**：生命週期事件自動化腳本與受信任宣告（`hooks.json`、`trusted_hooks.json`）。
   - **模型上下文通訊協定（Model Context Protocol, MCP）**：外部工具與上下文伺服器整合（`mcp_config.json`）。
   - **附掛容器（Sidecars）**：輔助容器與背景執行服務。

---

## 元件架構

本外掛程式包含以下主要元件：

1. **代理（Agent）**：[`agents/agy_help/agent.md`](agents/agy_help/agent.md)
   - **四層降級查核防幻覺機制（Four-tier Fallback Hierarchy）**：
     - **第 1 層（官方結構化技能手冊）**：依提問產品查閱本機結構化手冊實體路徑（`~/.gemini/antigravity-cli/builtin/skills/antigravity_guide/references/` 下之 `cli.md`、`ide.md`、`app.md`、`sdk.md`）與客製化手冊（`~/.gemini/antigravity-cli/builtin/skills/agy-customizations/docs/` 下之 `skills.md`、`rules.md`、`plugins.md`、`hooks.md`、`mcp_servers.md`、`json_configs.md`）。
     - **第 2 層（本機動態診斷、說明與實體配置）**：透過白名單限制的 `run_command` 動態執行 `agy --help`、`agy help <subcmd>`、`agy <subcmd> --help`、`agy --version` / `agy version`、`agy plugin list`、`agy agents`、`agy models`、`agy changelog`、`agy mcp list`、`pip show google-antigravity`、`python3 -m pip show google-antigravity`，或透過 `view_file` 查閱本機設定檔（如 `~/.gemini/antigravity-cli/settings.json`、`.agents/`、`~/.gemini/config/plugins/`）。
     - **第 3 層（官方線上即時文件）**：透過 `read_url_content` / `search_web` 查閱官方最新即時文件完整網址（`https://antigravity.google/docs` 及其子專題站台，包含 CLI、IDE、Permissions、Sandbox、Skills、Rules、Hooks、Plugins、Sidecars、MCP 等）。
     - **第 4 層（嚴格事實錨定與拒絕猜測）**：若全無官方明確紀錄，明確回報已查核途徑並誠實告知查無此功能，嚴禁自行推測虛構指令或參數。
   - **命令執行安全護欄（Command Execution Guardrails）**：嚴格限制 `run_command` 僅能執行唯讀輔助指令，嚴禁執行任何非白名單或狀態修改命令。
   - 支援作為獨立主代理（Main Agent）或子代理（Subagent）執行。

2. **技能（Skill）**：[`skills/agy_help/SKILL.md`](skills/agy_help/SKILL.md)
   - 可在任何交談工作階段中以 `/agy_help` 斜線指令直接觸發。
   - 提供同步對齊代理之全生態系四層查核指引流程。

---

## 安裝與管理

### 驗證外掛程式
在專案根目錄下執行：
```bash
agy plugin validate .
```

### 安裝外掛程式
將外掛程式安裝至全域環境（`~/.gemini/config/plugins/`）：
```bash
agy plugin install /Users/andyawd/Project/agy_help
```

### 檢視已安裝清單
```bash
agy plugin list
agy agents
```

---

## 使用方式

### 方式 1：以代理模式啟動
在終端機中指定使用 `agy_help` 代理：
```bash
agy --agent agy_help
```

### 方式 2：在對話中呼叫技能
在現有交談工作階段中輸入斜線指令，詢問任何生態系產品：
```text
/agy_help 如何在 Antigravity 2.0 桌面版設定專案層級的沙盒（Sandbox）權限？
/agy_help 如何使用 Antigravity Python SDK 串流代理（Agent）的思維鏈（Thought）？
/agy_help Antigravity IDE 的 Tab 自動補全（Autocomplete）如何運作？
/agy_help 如何設定自訂的生命週期掛鉤（Lifecycle Hook）？
```

---

## 專案目錄結構

```text
agy_help/
├── plugin.json               # 外掛程式資訊清單（Manifest）
├── README.md                 # 專案說明文件
├── agents/
│   └── agy_help/
│       └── agent.md          # 代理定義檔（含 YAML Frontmatter 與 System Prompt）
└── skills/
    └── agy_help/
        └── SKILL.md          # 技能指示檔（含 YAML Frontmatter 與 Workflow）
```
