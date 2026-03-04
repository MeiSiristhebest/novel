# 新手入门指南 (Getting Started)

> **欢迎使用 Chinese Novelist Pro v6.3.0！**
> 全能网文助手：支持混搭流派、多平台风格适配，覆盖 95% 主流网文类型。

---

## ⚡ 最简使用 — 一句话开始

**直接在对话中说：**
> "我是新手，带我入门"

AI 会自动进入引导模式，5 轮访谈后帮你生成完整项目。无需任何配置！

**或者更直接：**
> "帮我写一个玄幻流的小说，书名叫《道天》"

AI 会自动调用合适的工具和模板。

---

## 📊 加载模式（v6.3.0 新增）

根据你的需求选择合适的模式：

| 模式 | 文件数 | 适用场景 | 说明 |
|:-----|:-------|:---------|:-----|
| **核心20模式** | ~20 | 新手、快速验证 | 最小化上下文，快速启动 |
| **标准模式** | ~60 | 日常写作 | 核心20 + 流派Hook + 常用技法 |
| **完整模式** | 108 | 专业创作 | 全部引用文件 |

> 详见 `references/core-20-essential.md`

---

## 🆕 v6.3.0 核心升级

### 1. 分层加载机制
不再需要一次性加载 108 个文件。核心20模式让 AI 以最小上下文快速启动，按需扩展。

### 2. 统一执行术语
所有指令使用 RFC 2119 风格的标准术语（必须/禁止/应当/可以），消除歧义。

### 3. 协议单一真相源 (SSOT)
Phase 0-5 全流程协议只在 `references/quality/protocol-compliance.md` 中完整定义，其他文件通过指针引用。

### 4. 混搭引擎启动 (Mix-and-Match)
自由组合 **"基础流派"** 和 **"金手指引擎"**！

**示例：**
- "我要写一个 **凡人流** + **直播系统** 的小说"
- "我想写 **年代文** 但主角有 **位面聊天群**"

### 5. 智能质检系统
三级质检：L1 基础扫描（每章必做）→ L2 完整质检（建议做）→ L3 高级分析（按需）

---

## 📁 支持流派速查 (35种)

| 分类 | 包含流派 |
| :--- | :--- |
| **男频主流** | 玄幻流、仙侠流、凡人流、洪荒流、传统武侠 |
| **都市/现代** | 都市异能、神豪流、文娱明星、现实行业、年代文 |
| **科幻/未来** | 科幻星际、赛博朋克、系统流、末日废土 |
| **悬疑/惊悚** | 克苏鲁、规则怪谈、无限流、国运直播、刑侦悬疑、心理惊悚 |
| **女频** | 古言/女频、现代言情、古代宫斗、快穿攻略、团宠萌宝、耽美/BL |
| **特殊/垂直** | 历史穿越、轻小说、游戏电竞、体育竞技、短篇/微小说、喜剧/讽刺、军事/谍战、诸天流、种田/领主 |

---

## 🚀 快速启动

### 方式 1: 对话启动（推荐）
直接在对话中说出你的需求：
- "我要写一个玄幻流 + 系统流的小说，书名叫《道天》"
- "帮我生成一个都市异能的小说策划"

AI 会自动调用合适的工具和模板。

### 方式 2: 使用快速启动脚本
```bash
# 交互式选择流派和引擎
python tools/quick_start.py

# 查看所有支持的流派和引擎
python tools/quick_start.py --list-templates
```

### 方式 3: 长程写作 Harness
```bash
# 自动多轮推进
python tools/novel_agent_runner.py --novel "你的书名" --chapters 10

# 指定流程（默认 five-role，可选 writer-qa）
python tools/novel_agent_runner.py --novel "你的书名" --pipeline writer-qa --chapters 10

# 指定 LLM 后端（claude/alma/openai/openai-compatible/gemini/ollama/codex-cli/command）
python tools/novel_agent_runner.py --novel "你的书名" --llm-backend openai --model gpt-5-mini

# 严格门禁（默认 true）
python tools/novel_agent_runner.py --novel "你的书名" --strict-gates true --sync-views true

# Alma 自动执行（兼容旧参数 --alma）
python tools/novel_agent_runner.py --novel "你的书名" --chapters 10 --llm-backend alma --thread-id "<线程ID>"

# OpenAI 兼容网关（LM Studio/vLLM/LiteLLM/本地代理）
python tools/novel_agent_runner.py --novel "你的书名" --llm-backend openai-compatible --llm-base-url "http://localhost:4000/v1" --model "gpt-4o-mini"

# 自定义命令后端（把 prompt 从 stdin 传给你的脚本/CLI）
python tools/novel_agent_runner.py --novel "你的书名" --llm-backend command --llm-command "python [你的LLM桥接脚本].py --model {model}" --model "qwen2.5"

# 复用 Codex CLI 本地登录态（无需单独 OpenAI API Key）
python tools/novel_agent_runner.py --novel "你的书名" --llm-backend codex-cli --model gpt-5

# 若 Codex 在本机审批/沙箱链路较慢，可显式开启危险直通模式（仅在可信本地环境使用）
python tools/novel_agent_runner.py --novel "你的书名" --llm-backend codex-cli --model gpt-5.2 --codex-dangerous true
```

也可以直接说："自动写10章"。

### 方式 3.1: 迁移旧项目到新状态模型
```bash
# 预演（不落盘）
python tools/migrate_novel_state.py --novel "你的书名"

# 正式迁移（自动备份）
python tools/migrate_novel_state.py --novel "你的书名" --apply

# 运行时校验
python tools/validate_runtime.py --novel "你的书名"
```

### 方式 3.2: Demo 式自动循环入口
```bash
# Windows
powershell -File tools/run-novel-automation.ps1 -Novel "你的书名" -Pipeline "five-role" -LlmBackend "openai" -Model "gpt-5-mini" -Rounds 3 -DelaySeconds 1

# Bash
bash tools/run-novel-automation.sh "你的书名" "writer-qa" 3 true true 1 "ollama" "qwen2.5:14b"
```

说明：
- 脚本会自动记录每轮 `remain:A->B`、`delta` 和 `last_error` 到 `automation/progress.md`
- 每次运行会生成独立日志：`automation/logs/run-<novel>-<pipeline>-<timestamp>.log`
- 若剩余章节为 0，会自动早停

### 方式 4: 非脚本 Prompt-Only 闭环（通用LLM对话框）
适用：你不想运行任何脚本，但仍希望按 `.context` 真相源执行完整流程。

入口文件：
- `references/prompt-only/MASTER_ORCHESTRATOR.md`
- `references/prompt-only/SOP_MANUAL_RUN.md`
- `references/prompt-only/ROUTER_PROMPT.md`
- `references/prompt-only/CONTEXT_PACKER_PROMPT.md`

#### 一章手工示例（最小可运行）
1. 在对话框粘贴：
   - `.context/scene_list.json`
   - `.context/STATE.md`
   - `.context/RUNNER_STATE.json`
   - 当前章素材（03/04/05/06）
2. 发送 `references/prompt-only/ROUTER_PROMPT.md`，拿到 `.context/ROUTING_TRACE.json` 草案（格式参照 `references/prompt-only/MANUAL_TEMPLATES/ROUTING_TRACE.template.json`）。
3. 发送 `CONTEXT_PACKER_PROMPT.md`，执行全文注入与分批（如超限）。
4. 按 `next_role` 发送角色 Prompt（目录 `references/prompt-only/ROLE_PROMPTS/` 下对应文件）。
5. 顺序发送门禁 Prompt（目录 `references/prompt-only/GATES_PROMPTS/` 下全部文件）。
6. 若门禁全通过，要求模型输出：
   - `.context/RUNNER_STATE.json` 更新建议
   - `scene_list.passes` 更新建议（仅 QA/Polisher）
   - `.context/NEXT_PROMPT.md`
7. 人工落盘并记录到 `automation/progress.md`。

关键约束：
- 不再“前800字截断”；命中文件默认全文注入。
- 不再“前4文件限制”；按相关性自动选集 + 分批多轮。
- 任一 blocking gate 失败立即停机，不推进 `passes`。

### 方式 5: 使用质检 Prompt
写完章节后，在对话中说：
- "用场景质检标准审查这一章" → 调用 `scene-critic.md`
- "帮我做主编级审稿" → 调用 `chief-editor.md`
- "检查人物是否OOC" → 调用 `fanfic-ooc.md`

---

## 📖 进阶阅读

- **核心20文件清单** → `references/core-20-essential.md`
- **视觉流程图** → `references/visual-guide.md`
- **执行术语标准** → `references/quality/enforcement-levels.md`
- **完整写作协议** → `references/quality/protocol-compliance.md`
- **所有流派范文** → `references/style-exemplars/` 目录
- **写作技巧指南** → `references/guides/` 目录
- **系统架构** → `SKILL.md` 和 `INTEGRATION-ARCHITECTURE.md`
- **非脚本闭环协议** → `references/prompt-only/` 目录

---

## 🔁 Auto-Coding Demo 对照学习路径

如果你在参考 `auto-coding-agent-demo`，可按下列映射理解：

1. `task.json` ↔ `.context/scene_list.json`（任务真相源）
2. `CLAUDE.md` ↔ `references/quality/protocol-compliance.md`（执行协议）
3. `run-automation.sh` ↔ `tools/run-novel-automation.ps1/.sh`（自动循环入口）
4. `progress.txt` ↔ `.context/PROGRESS.md`（过程审计日志）
