# Agent Monorepo / Personal IP Guide

## 目的

這份指南整理目前對話中形成的核心方向，幫助建立一份屬於個人品牌的 agent-oriented monorepo。  
這個 monorepo 不只是放程式碼，而是用來承載：

- agent 學習
- agent 演化
- 技能提煉
- 工具開發
- playbooks / patterns / labs 的積累
- public knowledge repo 與 private runtime repo 的分工

---

## 核心定位

這份 monorepo 應該被理解為：

> 一個把 agent 的想法、工具、模板、實驗、正式包裝，逐步演化成可用能力的系統。

也就是說，它不是單純「很多 repo 放一起」，而是：

- labs 產生想法與驗證
- tools 提供 agent 可直接使用的能力
- patterns / playbooks 提煉方法
- docs 記錄演化歷程
- skills 成為可重用資產

---

## 建議的總體架構

```text
monorepo/
  labs/         # 實驗、demo、prototype、research
  tools/        # agent 可直接呼叫或組合的工具
  skills/       # 可安裝、可複用的 skill packs
  playbooks/    # 可人工閱讀與執行的方法手冊
  patterns/     # 可抽象化、可複製的模式
  docs/         # 架構、決策、演化紀錄
```

---

## 各資料夾角色定義

### `labs/`
用於保存：
- prototype
- demo app
- RAG 實驗
- 失敗案例
- 創意來源
- architecture exploration

特徵：
- 不一定可發佈
- 可以較自由
- 重點是探索與驗證

### `tools/`
用於保存：
- CLI tool
- MCP tool
- repo transformers
- extractors
- utilities for agent usage

特徵：
- 給 agent 或人直接使用
- 有清楚輸入/輸出
- 能被自動化呼叫
- 是能力接口

### `skills/`
用於保存：
- 可直接安裝或複用的 skill packs
- agent skill definitions
- reusable execution knowledge

特徵：
- 不是心得文
- 應有明確用途
- 有使用時機與結果導向

### `playbooks/`
用於保存：
- 作戰手冊
- step-by-step methods
- agent/human hybrid workflows

特徵：
- 偏流程
- 偏操作方法
- 偏可落地執行

### `patterns/`
用於保存：
- 可重用模式
- 結構設計
- 解法框架
- repo-to-skill / lab-to-skill 類方法

特徵：
- 比 templates 更不易混淆
- 適合 agentic learning
- 強調可抽象、可套用

### `docs/`
用於保存：
- architecture notes
- evolution log
- design decisions
- roadmap
- naming system
- publishing model

---

## 建議的演化路徑

一個內容項目在 monorepo 中，應該有以下提升路徑：

```text
labs/idea
  -> patterns/prototype
  -> tools/usable tool
  -> skills/reusable knowledge
  -> playbooks/documented execution
```

或者簡化成：

```text
lab -> distilled pattern -> tool/skill -> reusable system
```

---

## 不是所有內容都要 publish

需要先分清楚三種內容：

### 1. 可發佈的
例如：
- npm package
- pip package
- MCP tool
- CLI tool

### 2. 可參考但不發佈的
例如：
- demo
- 實驗
- 原型
- 研究筆記
- architecture exploration

### 3. 可轉化的
例如：
- 現在還只是 lab
- 未來可抽成 tools / skills / package

---

## 一般 package 如何 public 到 npm / pip / bun

### npm / bun
通常流程：
- 在 package 目錄內開發
- 有 `package.json`
- build（若需要）
- `npm publish`
- bun 通常也可直接安裝 npm package

### pip / Python
通常流程：
- 有 `pyproject.toml`
- `python -m build`
- `twine upload dist/*`

### 關鍵理解
不是 monorepo 內所有子項目都要被 package 化。  
只有那些：
- 有穩定 API
- 可重用
- 有清楚用途
- 能維護版本

的內容才適合發佈。

---

## Public / Private Repo 分工建議

### Public repo
用來做：
- learning notes
- labs
- patterns
- playbooks
- skills
- 開放式工具
- 演化紀錄

### Private repo
用來做：
- runtime
- actions
- secrets
- orchestration
- 真正生產系統
- internal MCP integration

### 可選第三層：shared MCP/tool repo
若 MCP 能力真的會跨多專案共用，可再獨立：
- `mcp-tools`
- `mcp-adapters`
- `agent-runtime-connectors`

---

## MCP 中的 tools 該如何理解

在 GitHub 官方 MCP 的語境中：

- MCP server = 一個獨立程序 / service
- tools = 此 server 對外暴露的可呼叫能力
- client config = 決定啟用哪些 tools

所以 `tools/` 不只是「工具目錄」，而是：

> 一組 agent 可發現、可授權、可調用的能力介面

### MCP tool naming 原則
應該像：
- `fetch_repo_tree`
- `select_high_value_files`
- `build_skill_context`
- `generate_skill_card`

避免：
- `do_magic`
- `run_pipeline`
- `process_data`

---

## 現有 repo 的理解方式

### `biu1-ragme-github`
應視為：
- lab
- demo app
- multi-service RAG application prototype

角色：
- 展示完整 app 與架構
- 驗證產品方向
- 不是單純小工具

適合放：
```text
labs/ragme-github/
```

### `biu1-gh-rag2skill`
應視為：
- tool
- pipeline
- repo-to-skill generator

角色：
- 把 repo 萃取成 `SKILL.md`
- 比較接近 skill factory / extraction tool

適合放：
```text
tools/gh-rag2skill/
```

### 關係總結
- `ragme-github` = 實驗場 / lab
- `rag2skill` = 從實驗與 repo 中提煉可複用知識的工具

---

## 可學習的熱門 repo 模式

### `mattpocock/skills`
可學：
- 把個人 workflow 產品化
- skill pack 化
- setup 簡潔
- 個人品牌感強

### `free-claude-code`
可學：
- 命中痛點
- proxy / adapter / provider abstraction
- CLI/API/config/module boundary 清楚
- 工程產品感強

### `ai-engineering-from-scratch`
可學：
- phase-based curriculum
- 學習路徑產品化
- lesson 產出 artifact
- docs / site / outputs 結合

### `addyosmani/agent-skills`
可學：
- skills / commands / references 分層清晰
- 工程 best practices agent 化
- skill anatomy 明確
- 最接近可複用 framework

---

## 你的 monorepo 應如何建立 impact

不要只追求內容多，而要追求：

> 把一個 agentic pain，壓縮成最容易被使用、fork、改造的資產。

可以參考以下 impact 路徑：

### 路徑 A：個人 workflow 產品化
- 把自己的 agent 工作法封裝成 skill / tool

### 路徑 B：解決協議層 / routing / integration bottleneck
- 做 MCP bridge / adapters / orchestration glue

### 路徑 C：學習與演化系統化
- 每個 lab 都能產出 artifact
- artifact 會回流成 skill / tool / pattern

### 路徑 D：把 best practices 變成 agent 行為
- 將抽象觀念寫成可執行流程

---

## 你最適合的 impact 方向

最適合你的可能是：

### 1. Repo-to-Skill / Lab-to-Skill 工廠
把：
- repo
- lab
- experiment
- architecture note

逐步轉成：
- skill
- pattern
- playbook
- reusable tool

### 2. Agent Evolution Log
做成一個清楚展示：
- agent 如何學習
- agent 如何成長
- skill 如何被蒸餾
- workflow 如何被組裝

的 monorepo

### 3. MCP-native Skill System
讓 skill 不只是 markdown，還能：
- 被 tools 使用
- 被 runtime 組合
- 被 CI 檢查
- 被 agent 調用

---

## 命名建議（個人 agent IP）

以下是目前較適合成為個人 monorepo 名稱的方向：

### 推薦名稱
- `swlok-agent-lab`
- `swlok-agent-forge`
- `swlok-skill-forge`
- `swlok-agent-foundry`
- `swlok-agent-playground`
- `swlok-agent-workbench`
- `swlok-agent-atlas`
- `swlok-agent-archive`
- `swlok-agent-patterns`
- `swlok-agent-evolution`

### 最推薦前三名
1. `swlok-agent-forge`
2. `swlok-agent-lab`
3. `swlok-agent-foundry`

### 各名稱傾向
- `lab`：最清楚、最穩
- `forge`：最有個人 IP 感、最有打造能力的意味
- `foundry`：最平台化、最工程化
- `evolution`：最符合學習/演化敘事

---

## 最終建議

如果這份 monorepo 的核心是：

- agent 學習
- skill 蒸餾
- tool 生產
- MCP / RAG / runtime ideas
- 長期演化紀錄

那最佳理解方式是：

> 這不是單純的 code monorepo，  
> 而是一個 lab-driven, tool-producing, skill-distilling monorepo。

而在實作上，最推薦的主結構是：

```text
monorepo/
  labs/
  tools/
  skills/
  playbooks/
  patterns/
  docs/
```

---

## 一句話版總結

這份 monorepo 應該承載的不是「很多程式」，而是：

> agent 的學習、演化、提煉、組裝與可重用能力的形成過程。