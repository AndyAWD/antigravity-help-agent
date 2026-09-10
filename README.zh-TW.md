# antigravity-help

[English](README.md) | [繁體中文](README.zh-TW.md)

Google Antigravity 全生態系與客製化體系知識庫說明外掛程式（Plugin），提供專屬的代理（Agent）與技能（Skill）。內建**「正向實證三軌協議（Positive Affirmative Protocol，證據先行與三態閉環）」**查核機制，為命令列介面（CLI，`agy`）、整合開發環境（IDE）、Antigravity 2.0 桌面應用程式（Desktop Application）、Python 軟體開發套件（SDK，`google-antigravity`）以及客製化體系（技能（Skills）、規則（Rules）、外掛程式（Plugins）、掛鉤（Hooks）、模型上下文通訊協定（Model Context Protocol, MCP）、附掛容器（Sidecars））提供嚴謹無幻覺（Zero-Hallucination）的技術規格審計與架構指引。

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

# 或指定路徑：
agy plugin install /path/to/antigravity-help-agent
```

### 檢視已安裝清單
```bash
agy plugin list
agy agents
```

---

## 支援產品與生態系範圍

本外掛程式提供 Google Antigravity 全產品線之技術指南：

1. **Antigravity 命令列介面（CLI，`agy`）**：終端機互動式介面、啟動旗標參數、斜線指令、設定檔（`settings.json`）與代理生命週期。
2. **Antigravity 整合開發環境（IDE）**：以 VS Code 為基礎的獨立 AI 開發環境、Tab 自動補全與超級補全（Autocomplete & Supercomplete）、行內指令（Inline Commands）、側邊欄對話面板、行內程式碼透鏡（Inline Code Lenses）與診斷自動修復。
3. **Antigravity 2.0 桌面應用程式（Desktop Application）**：平行桌面應用程式、對話畫布（Chat Canvas）、排程背景任務（Scheduled Background Tasks）、HTML 輔助面板（Auxiliary Pane：Subagents、Background Tasks、Artifacts、Files Changed、Terminals）、全域與專案層級安全權限管理。
4. **Antigravity Python 軟體開發套件（SDK，`google-antigravity`）**：程式化代理租賃、編排 API、非同步串流回應、思維鏈增量（Thought Delta）攔截、自訂工具與能力設定（`CapabilitiesConfig`）。
5. **客製化體系（Customization System）**：
   - **技能（Skills）**：程序化工作流程指引（`SKILL.md`）、參考文件與執行腳本。
   - **規則（Rules）**：全域與專案特定工作流程規範（`GEMINI.md`、`AGENTS.md`、`.agents/rules/`）。
   - **外掛程式（Plugins）**：打包與發布代理、技能、掛鉤與 MCP 伺服器的擴充套件。
   - **掛鉤（Hooks）**：生命週期事件自動化腳本與受信任宣告（`hooks.json`、`trusted_hooks.json`）。
   - **模型上下文通訊協定（Model Context Protocol, MCP）**：外部工具與上下文伺服器整合（`mcp_config.json`）。
   - **附掛容器（Sidecars）**：輔助容器與背景執行服務。

---

## 元件架構

本外掛程式包含以下主要元件：

1. **代理（Agent）**：[`agents/agy-help/agent.md`](agents/agy-help/agent.md)
   - 同時支援作為互動式主代理（Main Agent）與背景子代理（Subagent）執行。
   - 實作正向實證三軌協議、提問前提審查機制與唯讀診斷命令安全白名單。
   - 繼承模型上下文通訊協定能力（`inheritMcp: true`）。

2. **技能（Skill）**：[`skills/agy-help/SKILL.md`](skills/agy-help/SKILL.md)
   - 可在任何交談工作階段中以 `/antigravity-help:agy-help`（或簡稱 `/agy-help`）斜線指令直接觸發，無需切換目前主代理。
   - 提供同步對齊代理之證據先行與三態閉環查驗工作流程。

---

## 使用方式

### 1. 使用斜線指令呼叫與切換代理（`/agents`）

在已開啟的 `agy` 互動式交談工作階段中，輸入 `/agents` 斜線指令即可查看並切換至 `agy-help` 專屬代理：

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
       agy-help   Google Antigravity 全生態系說明助手
   ```

2. 選取並切換至 `agy-help`，終端機將提示就緒：
   ```text
   > /agents
     ⎿  Prepared selection: agy-help (will fork the current conversation on exit).
   ────────────────────────────────────────────────
   > 
   ────────────────────────────────────────────────
   ```
   切換後，當前的對話工作階段將由 `agy-help` 代理主導，進行深度技術審計與規格查詢。

---

### 2. 使用技能斜線指令即時詢問（`/antigravity-help:agy-help`）

若不希望切換當前對話的主代理（保持在 `default` 或專案代理），可隨時在交談框中直接輸入 `/antigravity-help:agy-help`（或 `/agy-help`）技能斜線指令進行單次或特定提問：

```text
────────────────────────────────────────────────
> /antigravity-help:agy-help 如何在 Antigravity 2.0 桌面版設定專案層級的沙盒（Sandbox）權限？
────────────────────────────────────────────────
```

常用查詢範例：
```text
/antigravity-help:agy-help 如何使用 Antigravity Python SDK 串流代理（Agent）的思維鏈增量（Thought Delta）？
/antigravity-help:agy-help Antigravity IDE 的 Tab 自動補全與超級補全（Autocomplete & Supercomplete）如何運作？
/antigravity-help:agy-help 如何設定自訂的生命週期掛鉤（Lifecycle Hook）與 trusted_hooks.json？
/antigravity-help:agy-help agy CLI 的 --effort 旗標定義與可選值為何？
```

---

### 3. 在終端機啟動時直接指定代理（`agy --agent`）

在系統終端機中，直接以 `agy-help` 代理啟動全新工作階段：

```bash
# 啟動互動式交談工作階段
agy --agent agy-help

# 或以非互動模式單次提問
agy --agent agy-help -p "請說明 Antigravity IDE 與一般 VS Code 擴充套件的本質差異"
```

---

### 4. 使用自然語言背景派工（Subagent 模式）

若您在日常開發工作階段（例如編寫專案程式碼）中需要臨時查詢 Antigravity 規格，但又不想讓查詢過程污染主要交談上下文（避免脈絡視窗 / Context Window 爆滿），可以直接用自然語言命令主代理將任務委派給 `agy-help` 子代理：

```text
請在背景派工給 agy-help 子代理去查閱 Antigravity IDE 的程式碼透鏡（Code Lenses）設定方式，並把總結帶回主對話。
```

主代理將會透過背景子代理獨立完成多層查核，並將精確無幻覺的答案帶回目前工作階段。

---

## 專案目錄結構

```text
antigravity-help-agent/
├── plugin.json               # 外掛程式資訊清單（Manifest）
├── LICENSE                   # MIT 開源授權條款
├── README.md                 # 主要說明文件（英文）
├── README.zh-TW.md           # 說明文件（繁體中文）
├── doc/                      # 實施案例原始紀錄與截圖佐證
│   ├── question.md           # 測試提問原文與假想終端機模擬畫面
│   ├── with-agy-help/        # 啟用 agy-help 之正確實證紀錄（Ground Truth）
│   │   ├── transcript.txt    # 完整終端機日誌（30.1k Tokens，1 個推理週期）
│   │   ├── screenshot_01.png # 證據檢索與協議啟動截圖
│   │   └── screenshot_02.png # 架構實質互斥分析與結論截圖
│   └── without-agy-help/     # 未啟用 agy-help 之幻覺對照組（Hallucination）
│       ├── transcript.txt    # 完整終端機日誌（130.8k Tokens，30+ 次工具呼叫）
│       ├── screenshot_01.png # 工具探索死循環起始截圖
│       ├── screenshot_02.png # 反組譯二進位檔探索截圖（objdump/nm）
│       ├── screenshot_03.png # 背景任務與程序管理死循環截圖
│       ├── screenshot_04.png # 試圖動態建立假外掛截圖
│       └── screenshot_05.png # 虛構命名空間與自動補全之幻覺回答截圖
├── agents/
│   └── agy-help/
│       └── agent.md          # 代理定義檔（含 YAML Frontmatter、正向實證協議與命令安全白名單）
└── skills/
    └── agy-help/
        └── SKILL.md          # 技能指示檔（含 YAML Frontmatter 與作業流程）
```

---

## 核心機制與協議

### 正向實證三軌協議（Positive Affirmative Protocol）
`agy-help` 在產生任何解答前，必須嚴格依循「證據先行（Evidence-First）」的閉環查驗流程：

1. **強制證據錨定（Mandatory Evidence Anchor）**：
   - **官方原典逐字引述**：優先檢索本機結構化手冊（`builtin/skills/antigravity_guide/references/` 與 `builtin/skills/agy-customizations/docs/`）；線上來源嚴格限定官方網域（`antigravity.google`，搜尋時強制帶入 `domain: antigravity.google` 條件，以及 `github.com/google-antigravity`），嚴禁採信非官方第三方論壇與部落格。
   - **本機物理狀態檢驗**：透過 `view_file` 或 `list_dir` 檢視本機設定檔（`settings.json`）、目前掛載之 `<skills>` 註冊結構與外掛實體目錄，以實體資料結構為憑。

2. **三態閉環輸出（Strict Ternary Output）**：
   所有回答結論只能且必須歸屬於以下三態之一，杜絕模稜兩可或臆測：
   - **軌道 1【已證實支援（Documented Feature）】**：官方文件有白紙黑字逐字規範，貼出原文引述並說明官方標準語法與操作規範。
   - **軌道 2【架構實質互斥（Architectural Exclusion）】**：底層資料結構不支持該推論（如本機技能註冊表為扁平唯一鍵，同名鍵值必然覆蓋），明確否定並出示底層物理架構說明限制原因。
   - **軌道 3【邊界未規範（Unspecified Edge Case）】**：查無官方逐字規範亦無物理機制支援，唯一合法表述為：*「此情境在官方規格手冊中未定義具體行為，屬於未規範之邊界情境（Undefined Behavior）。」*

3. **使用者提問前提審核（Premise Verification Protocol）**：
   當提問包含假設性介面（如 ASCII 模擬畫面（Mockup）、預設選項清單或假想流程）時，預設前提為待驗證。優先審查前提是否符合官方白紙黑字規範，若無直接佐證則宣告前提不成立，嚴禁為假設圓謊。

4. **命令執行安全白名單（Command Execution Guardrails）**：
   `run_command` 工具權限嚴格限制於唯讀診斷指令（如 `agy --help`、`agy help <subcommand>`、`agy <subcommand> --help`、`agy --version` / `agy version`、`agy agents`、`agy plugin list`、`agy models`、`agy changelog`、`agy mcp list`、`pip show google-antigravity` / `python3 -m pip show google-antigravity`），嚴格禁止執行任何可能變更系統狀態或非診斷性的命令。

---

## 實施案例：以正向實證協議根除架構與介面幻覺

以下為外掛程式（Plugin）開發流程中的真實測試案例，清楚展示了缺乏負向架構約束時所產生的諂媚型幻覺（Sycophantic Hallucination），以及 `agy-help` 如何透過正向實證協議精準判定。

### 測試情境與假想介面模擬畫面（Mockup）
> 完整提問原文請參閱 [`doc/question.md`](doc/question.md)。

情境為同時安裝了兩個外掛程式（`antigravity-git-flow` 與 `antigravity-github-flow`），兩者皆包含名為 `commit` 的技能（Skill）。

**使用者提問與終端機模擬畫面：**
```text
假設我安裝了 antigravity-git-flow 和 antigravity-github-flow 這兩個外掛程式，且兩者都包含 commit 指令。當我輸入 /commit 時，下方是否會同時顯示 /antigravity-git-flow:commit 與 /antigravity-github-flow:commit 供我選擇？

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

### 執行對比與成果

| 評估指標 | 內建一般指引（`/antigravity-guide`） | `agy-help` 外掛程式（Plugin） |
| :--- | :--- | :--- |
| **推理效率** | 耗費 30+ 次工具呼叫、消耗 130.8k 權杖（Tokens），甚至試圖以 `strings`/`nm`/`objdump` 反組譯二進位執行檔 | **單一推理週期（1 reasoning cycle）**立即精準解答，無多餘權杖消耗（僅 30.1k Tokens） |
| **提問前提審查** | **失敗**：直接採信提問中的假想介面與模擬畫面 | **通過**：依循提問前提審核協議（Premise Verification Protocol）優先查核介面真實性 |
| **輸出真實性** | **諂媚型幻覺**：虛構「外掛命名空間（Plugin Namespacing）語法 `/<plugin>:<skill>`」與「自動補全多選匹配」 | **軌道 2（架構實質互斥）**：依底層扁平唯一鍵字典結構，明確指出鍵值覆蓋機制 |
| **架構機制解釋** | 錯誤回答兩者都會出現在終端機使用者介面（TUI）供選取 | 正確指出同名技能僅會保留載入優先級最高者，補全選單**只會出現單一項目** |
| **原始紀錄與截圖** | 完整歷程：[`doc/without-agy-help/transcript.txt`](doc/without-agy-help/transcript.txt)<br>截圖佐證：[`screenshot_01.png`](doc/without-agy-help/screenshot_01.png)–[`05.png`](doc/without-agy-help/screenshot_05.png) | 完整歷程：[`doc/with-agy-help/transcript.txt`](doc/with-agy-help/transcript.txt)<br>截圖佐證：[`screenshot_01.png`](doc/with-agy-help/screenshot_01.png)–[`02.png`](doc/with-agy-help/screenshot_02.png) |

#### 1. 使用內建一般指引（`/antigravity-guide`）的執行現象（幻覺對照組）
- **缺乏架構邊界認知**：未能識別終端機使用者介面（TUI）的斜線指令並不支援以外掛名稱作為前綴鍵（Prefix Key）。
- **失控的工具探索循環（30+ 次工具呼叫、130.8k 權杖）**：代理進入死循環，試圖反組譯本機 `agy` 執行檔來推測行為（詳見 [`doc/without-agy-help/transcript.txt`](doc/without-agy-help/transcript.txt)）。
- **迎合提問虛構不存在的機制**：給出自信但完全錯誤的肯定回答（*「會的，顯示結果就如同您示意圖所呈現的樣子。」*），並憑空捏造「外掛命名空間」與「自動補全冒號匹配」兩大虛構功能。

#### 2. 使用 `agy-help`（正向實證三軌協議）的執行現象
- **單一推理週期直擊核心**：無需執行盲目的反組譯或探索性指令（詳見 [`doc/with-agy-help/transcript.txt`](doc/with-agy-help/transcript.txt)）。
- **嚴謹遵循系統架構不變性（Architectural Invariants）**：
  1. 終端機使用者介面（TUI）不支援外掛前綴斜線指令。
  2. 技能註冊表在底層運作於扁平唯一鍵字典（Flat Unique-Key Table）；當出現同名技能時，註冊機制會依載入優先權直接覆蓋（Key Overwriting），因此記憶體中只會存在單一實體，自動補全清單中也**永遠只會出現一個候選項目**。

> [!NOTE]
> 內建手冊雖然詳盡，但在面對逼真的假想介面（UI Mockup）或邊界情境時，一般模型往往會為了迎合使用者預設立場而串接內部符號虛構事實。`agy-help` 專門藉由正向實證三軌協議與負向架構約束，徹底杜絕此類架構性幻覺。

---

## 授權條款

本專案採用 [MIT 授權條款](LICENSE)。
