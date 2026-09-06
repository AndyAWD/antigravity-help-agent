# agy_help

[English](README.md) | [繁體中文](README.zh-TW.md)

Google Antigravity 全生態系與客製化體系知識庫說明外掛程式（Plugin），提供專屬的代理（Agent）與技能（Skill），涵蓋命令列介面（CLI，`agy`）、整合開發環境（IDE）、Antigravity 2.0 桌面應用程式（Desktop Application）、Python 軟體開發套件（SDK，`google-antigravity`），以及客製化體系（技能（Skills）、規則（Rules）、外掛程式（Plugins）、掛鉤（Hooks）、模型上下文通訊協定（Model Context Protocol, MCP）、附掛容器（Sidecars）等）的完整指南與架構解答。

---

## 安裝與管理

### 安裝外掛程式

#### 方式 A：透過 GitHub 遠端安裝（推薦）
```bash
agy plugin install https://github.com/andyawd/antigravity-help-agent
```

#### 方式 B：從本機開發路徑安裝
```bash
# 在專案目錄下執行：
agy plugin install .

# 或指定絕對路徑：
agy plugin install /Users/andyawd/Project/agy_help
```

### 檢視已安裝清單
```bash
agy plugin list
agy agents
```

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

## 使用方式

安裝或配置 `agy_help` 外掛程式後，在 Antigravity 命令列介面（`agy`）中有以下幾種實作與啟動方法：

### 1. 使用斜線指令呼叫與切換代理（`/agents`）

在已開啟的 `agy` 互動式交談會話中，輸入 `/agents` 斜線指令即可查看並切換至 `agy_help` 專屬代理：

1. 執行 `> /agents` 會看到可用代理清單：
   ```text
   ────────────────────────────────────────────────
   > /agents
   ────────────────────────────────────────────────
   Create New Agents
     Workspace: 專案路徑
     Global: 全域路徑

   Available Agents
   > ● default    Default agent
       agy_help   Google Antigravity 全生態系說明助手
   ```

2. 移動方向鍵選取並切換至 `agy_help`，終端機將提示已就緒：
   ```text
   > /agents
     ⎿  Prepared selection: agy_help (will fork the current conversation on exit).
   ────────────────────────────────────────────────
   > 
   ────────────────────────────────────────────────
   ```
   切換後，當前的對話工作階段將由 `agy_help` 代理主導，回答所有 Antigravity 生態系產品與客製化體系的疑難雜症。

---

### 2. 使用技能斜線指令即時詢問（`/agy_help`）

若不希望切換當前對話的主代理（保持在 `default` 或專案代理），可隨時在交談框中直接輸入 `/agy_help` 技能斜線指令進行單次或特定提問：

```text
────────────────────────────────────────────────
> /agy_help 如何在 Antigravity 2.0 桌面版設定專案層級的沙盒（Sandbox）權限？
────────────────────────────────────────────────
```

常用查詢範例：
```text
/agy_help 如何使用 Antigravity Python SDK 串流代理（Agent）的思維鏈（Thought）？
/agy_help Antigravity IDE 的 Tab 自動補全（Autocomplete）如何運作？
/agy_help 如何設定自訂的生命週期掛鉤（Lifecycle Hook）？
/agy_help agy CLI 的 --effort 旗標定義與可選值為何？
```

---

### 3. 在終端機啟動時直接指定代理（`agy --agent`）

在系統終端機中，直接以 `agy_help` 代理啟動全新工作階段：

```bash
# 啟動互動式對話會話
agy --agent agy_help

# 或以非互動模式單次提問
agy --agent agy_help -p "請說明 Antigravity IDE 與一般 VS Code 擴充套件的本質差異"
```

---

### 4. 使用自然語言背景派工（Subagent 模式）

若您在日常開發會話（例如編寫專案程式碼）中需要臨時查詢 Antigravity 知識，但又不想讓查詢過程污染主要交談上下文（避免語境視窗 / Context Window 爆滿），可以直接用自然語言命令主代理將任務委派給 `agy_help` 子代理：

```text
請在背景派工給 agy_help 子代理去查閱 Antigravity IDE 的程式碼透鏡（Code Lenses）設定方式，並把總結帶回主對話。
```

主代理將會透過背景子代理獨立完成多層查核，並將精確無幻覺的答案帶回目前工作階段。

---

## 專案目錄結構

```text
agy_help/
├── plugin.json               # 外掛程式資訊清單（Manifest）
├── LICENSE                   # MIT 開源授權條款
├── README.md                 # 主要說明文件（英文）
├── README.zh-TW.md           # 說明文件（繁體中文）
├── agents/
│   └── agy_help/
│       └── agent.md          # 代理定義檔（含 YAML Frontmatter、四層查核防幻覺與命令安全白名單）
└── skills/
    └── agy_help/
        └── SKILL.md          # 技能指示檔（含 YAML Frontmatter 與作業指引）
```

---

## 授權條款

本專案採用 [MIT 授權條款](LICENSE)。
