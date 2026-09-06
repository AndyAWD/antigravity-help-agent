---
name: agy_help
description: Use this skill when the user asks about any Google Antigravity ecosystem product (including Antigravity CLI, Antigravity IDE, Antigravity 2.0 Desktop, and Antigravity Python SDK), or the Customization System (Skills, Rules, Plugins, Hooks, MCP servers, Sidecars), configuration, architecture, or troubleshooting.
---

# Google Antigravity 全生態系說明助手作業流程（agy_help）

當需要回答 Google Antigravity 生態系任何產品（包括命令列介面（CLI，`agy`）、整合開發環境（IDE）、Antigravity 2.0 桌面應用程式（Desktop Application）、Python 軟體開發套件（SDK，`google-antigravity`））或客製化體系的相關問題時，**嚴格禁止憑空猜測或腦補虛構**。必須依循以下四層降級查核防幻覺架構（Four-tier Fallback Hierarchy）逐步驗證：

---

## 四層降級查核防幻覺架構

### 第 1 層：官方結構化技能手冊（Primary Offline Reference）
依據使用者詢問的具體產品或客製化面向，優先查閱本機結構化手冊。
本機內建手冊實體路徑位於 `~/.gemini/antigravity-cli/builtin/skills/antigravity_guide/references/`（或 IDE 對應之 `~/.gemini/antigravity-ide/builtin/skills/antigravity_guide/references/`、桌面版之 `~/.gemini/antigravity/builtin/skills/antigravity_guide/references/`，Windows 環境對應為 `%USERPROFILE%\.gemini\...`）：
- **Antigravity 命令列介面（CLI，`agy`）**：查閱 `references/cli.md`（CLI 斜線指令、啟動旗標參數、設定檔結構）。
- **Antigravity 整合開發環境（IDE）**：查閱 `references/ide.md`（Tab 自動補全（Autocomplete & Supercomplete）、行內指令（Inline Command）、側邊欄對話面板、行內程式碼透鏡（Inline Code Lenses）、診斷自動修復）。
- **Antigravity 2.0 桌面應用程式（Desktop Application）**：查閱 `references/app.md`（對話畫布（Chat Canvas）、排程任務（Scheduled Tasks）、輔助面板（Auxiliary Pane）、全域與專案層級安全權限）。
- **Antigravity Python 軟體開發套件（SDK，`google-antigravity`）**：查閱 `references/sdk.md`（`Agent` 類別、非同步串流回應、思維鏈增量（Thought Delta）、自訂工具與能力設定 `CapabilitiesConfig`）。
- **客製化架構體系（Customization System）**：查閱內建手冊目錄（實體路徑位於 `~/.gemini/antigravity-cli/builtin/skills/agy-customizations/docs/`）：
  - 技能（Skills）：`docs/skills.md`
  - 規則（Rules）：`docs/rules.md`
  - 外掛程式（Plugins）：`docs/plugins.md`
  - 掛鉤（Hooks）：`docs/hooks.md`
  - 模型上下文通訊協定（Model Context Protocol, MCP）：`docs/mcp_servers.md`
  - 設定檔格式（JSON Configs）：`docs/json_configs.md`

### 第 2 層：本機動態診斷、說明與實體配置（Local Runtime & Environment Introspection）
若第 1 層手冊未記載或需確認本機安裝版本的具體細節：
- **CLI 與外掛程式診斷**：呼叫 `run_command` 執行 `agy --help`、`agy help <subcommand>`、`agy <subcommand> --help`、`agy --version` / `agy version`、`agy plugin list`、`agy agents`、`agy models`、`agy changelog` 或 `agy mcp list`，獲取執行檔的第一手官方資訊。
- **本機設定檔案驗證**：透過 `view_file` 或 `list_dir` 查閱本機設定與結構：
  - CLI 設定：`~/.gemini/antigravity-cli/settings.json`
  - IDE 與專案層級配置：專案目錄下之 `.agents/`、`~/.gemini/antigravity-ide/`
  - 2.0 桌面版設定：`~/.gemini/antigravity/`
  - 外掛程式全域目錄：`~/.gemini/config/plugins/`
- **Python SDK 環境查核**：透過 `run_command` 執行 `pip show google-antigravity` 或 `python3 -m pip show google-antigravity` 檢查已安裝版本與中繼資料。

### 第 3 層：官方線上即時文件（Live Official Docs Fetching）
若前兩層皆無明確紀錄，使用 `read_url_content` 或 `search_web` 查閱官方最新即時站台（所有路徑均需使用完整 URL）：
- 官方主文件首頁：`https://antigravity.google/docs`
- 命令列介面（CLI）文件：
  - `https://antigravity.google/docs/cli/reference`
  - `https://antigravity.google/docs/cli/features`
  - `https://antigravity.google/docs/cli/best-practices`
- 整合開發環境（IDE）與瀏覽器自動化：`https://antigravity.google/docs/ide/browser`
- 安全權限與終端機沙盒（Sandbox）：
  - `https://antigravity.google/docs/permissions`
  - `https://antigravity.google/docs/sandbox`
- 客製化體系指南：
  - 技能（Skills）：`https://antigravity.google/docs/skills`
  - 規則與工作流程（Rules & Workflows）：`https://antigravity.google/docs/rules-workflows`
  - 掛鉤（Hooks）：`https://antigravity.google/docs/hooks`
  - 外掛程式（Plugins）：`https://antigravity.google/docs/plugins`
  - 附掛容器（Sidecars）：`https://antigravity.google/docs/sidecars`
  - 模型上下文通訊協定（MCP）：`https://antigravity.google/docs/mcp`
- Python SDK 開源儲存庫：`https://github.com/google-antigravity/antigravity-sdk-python`
- 更新日誌（Changelog）與疑難排解：
  - `https://antigravity.google/changelog`
  - `https://antigravity.google/support`

### 第 4 層：嚴格事實錨定與拒絕猜測（Strict Fact-Grounding & Honest Refusal）
- 若歷經前三層查核後，**依然查無該產品功能、指令、旗標或應用程式介面（API）之明確官方紀錄**：
  - **嚴格禁止自行推測、擴充或虛構功能與參數**。
  - 明確列出已查核之途徑（結構化技能手冊、本機動態環境、官方線上即時文件）。
  - 誠實明確地告知使用者「官方手冊、本機環境與線上文件中均無此項記載」，並提供官方文件站台連結或指引至官方社群諮詢，落實零幻覺（Zero-Hallucination）原則。
