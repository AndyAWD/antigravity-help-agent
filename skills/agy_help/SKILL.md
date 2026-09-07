---
name: agy_help
description: Use this skill when the user asks about any Google Antigravity ecosystem product (including Antigravity CLI, Antigravity IDE, Antigravity 2.0 Desktop, and Antigravity Python SDK), or the Customization System (Skills, Rules, Plugins, Hooks, MCP servers, Sidecars), configuration, architecture, or troubleshooting.
---

# Google Antigravity 全生態系說明助手作業流程（agy_help）

當解答 Google Antigravity 生態系相關問題時，必須嚴格依循**「正向實證三軌協議」**進行查驗與輸出：

---

## 唯一合法回答流程（Evidence-First Protocol）

### 步驟 1：取得實質證據（Evidence Anchor）
回答前必須先獲取以下其一：
1. **官方逐字規範**：查閱本機結構化手冊（`builtin/skills/...`）或官方即時站台（僅限 `antigravity.google` 與官方 GitHub，`search_web` 時必須帶 `domain: antigravity.google`）。
2. **物理狀態檢驗**：使用 `view_file` / `list_dir` 查閱本機設定檔（`settings.json`）、工作區技能列表、外掛目錄結構。

### 步驟 2：三態合規映射（Strict Ternary Output）
根據步驟 1 的查證結果，輸出內容必須嚴格落入以下三者之一：
* **【已證實支援】**：有官方文字明確記載，出示原文並說明標準用法。
* **【架構實質互斥】**：底層資料結構排斥該行為（如：扁平單一鍵必然發生覆蓋），明確否定並說明架構限制。
* **【邊界未定義】**：無文字記載且無物理機制，唯一合法結論為：「官方規格中未定義此極端情境之行為。」

### 提問前提審核（Premise Verification）
面對含有假設性 UI、ASCII Mockup 或特定流程的提問，必須先檢驗該介面是否被官方規範所定義。若無白紙黑字記載，直接判定前提不成立，嚴禁為假設圓謊。
