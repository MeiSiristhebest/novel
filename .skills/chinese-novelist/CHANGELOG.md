# Changelog

本文件记录 `chinese-novelist` skill 的所有重要更新。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)，
版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

---

## [6.3.8] - 2026-03-01

### 🔒 协议对齐与能力加固（Phase 1/2）

#### 新增
- `tools/novel_agent_runner.py`
  - 新增 Engine 路由：`ENGINE_CONTEXT_MAP`、`detect_engine_types()`、`gate_engine_pack`
  - 新增语言包硬门禁：`gate_language_pack`（guardrails + language-craft + show-dont-tell + style exemplar）
  - 新增 Phase 5 同步门禁：`gate_phase5_sync`
  - 新增 `--strict-schema`、`--audit-protocol` 参数
  - `ROUTING_TRACE.json` 新增 `engine_types/language_pack_status/phase5_sync_status/security_mode/selection_score`
- `tools/runtime_core.py`
  - `extract_last_json_object` 升级为三层解析（fenced json > strict decode > fallback）
  - 新增 `validate_quality_result_data()`
  - `validate_scene_list_data/validate_runtime_state_data` 支持 strict 模式
- `tools/sync_project_views.py`
  - 新增 `03-分章细纲.md` 自动同步区块
  - 新增 `.context/VOLUME_XX.md` 自动同步区块
  - 新增 `.context/PHASE5_SYNC_TRACE.json`（6文件同步证据）
- `schemas/`
  - `scene_list.schema.json`、`runtime_state.schema.json` 新增 `schema_version`
  - 新增 `qa_result.schema.json`、`polisher_result.schema.json`
- `tools/run-novel-automation.ps1/.sh`
  - 新增 `--audit-protocol` 透传（默认开启）
- `data/command-whitelist.txt`：新增 command backend 默认白名单

#### 安全加固
- 默认 `--permission-mode` 调整为 `default`
- `command` 后端新增前缀白名单校验
- `codex-dangerous` 改为双条件启用（CLI + `NOVEL_ALLOW_CODEX_DANGEROUS=true`）

#### 兼容性
- 保持旧流程可运行，`strict-schema` 默认关闭
- 未声明 Engine 项目不阻断（`gate_engine_pack: not applicable`）

## [6.3.7] - 2026-02-22

### 🚫 禁止跳章修复（Chapter Continuity Hard Gate）

#### 修复
- `novels/TheGlitchHunter/.context/scene_list.json` 补齐缺失章节：
  - 新增 `CH10` / `CH11` / `CH12`
  - 章节序列恢复为 `CH01..CH20` 连续编号
- `tools/runtime_core.py` 增强 `validate_scene_list_data()`：
  - 强制 `chapter_num` 唯一且连续（缺号直接报错）
  - 强制 `id` 数字部分与 `chapter_num` 一致
  - 强制 `chapter_file` 数字部分与 `chapter_num` 一致
- `tools/novel_agent_runner.py` 修复 `--max-iterations` 在角色调用失败时的重试越界问题：
  - 当已达到本轮上限且角色调用失败时，立即停机返回失败
- `codex-cli` QA 提示词策略调整为快速结构化审计，避免长时间卡在 QA 调用。

## [6.3.6] - 2026-02-22

### 🔄 状态视图一致性修复（STATE.md 与 07 视图对齐）

#### 修复
- `tools/sync_project_views.py` 新增 `.context/STATE.md` 回写同步：
  - 自动更新 `已完成章节`、`总字数`、`下一章节`、`完成`、`同步时间`
  - 保持 `scene_list.json` 作为进度真值源，避免 `STATE.md` 长期滞后
- 修复阶段字段格式污染：
  - 清洗 `**...**` / `` `...` `` 内联标记，避免 `07-项目状态.md` 出现嵌套样式
- 修复章节标题重复：
  - 当标题已含“第X章”前缀时不再重复拼接（避免 `第7章: 第7章: ...`）

## [6.3.5] - 2026-02-22

### 🌐 多后端 LLM 兼容层（Decouple from Claude Code）

#### 新增
- `tools/novel_agent_runner.py` 新增统一参数：
  - `--llm-backend`：`claude | alma | openai | openai-compatible | gemini | ollama | codex-cli | command`
  - `--llm-base-url`、`--llm-api-key-env`、`--http-retries`、`--http-retry-delay`、`--llm-command`
- 新增统一后端分发 `run_with_backend(...)`，支持在同一门禁流程下切换模型提供方。
- 新增 `codex-cli` 后端：通过 `codex exec` 非交互调用，复用本机 Codex 登录态。

#### 修复
- `claude_run()` 对“返回码=0但空输出”的情况改为显式失败，避免伪成功。
- 引入统一 HTTP 请求重试（429/5xx 等）与明确错误回传，避免静默卡死。
- 新增后端感知默认模型映射（未显式指定模型时）：
  - `codex-cli/openai/openai-compatible` → `gpt-5.2`
  - `gemini` → `gemini-2.5-pro`
  - `ollama` → `qwen2.5:14b`
- `codex-cli` 执行链路稳定性修复：
  - 固定在仓库根目录执行（与 prompt 中 `novels/...` 路径基准一致）
  - 启用 `--ephemeral` 与 `shell_environment_policy.inherit=none`，减少本机 profile/conda 干扰
  - 新增 `--codex-dangerous` 参数并透传到自动化脚本入口
  - 写作角色新增“直出正文”模式：禁止 shell 调用，Runner 直接将模型输出落盘到 `drafts/chapter_XX.md`
  - QA 角色新增结果落盘：`codex-cli` 非结构化输出会被归档为 `.context/qa_result.json`

#### 入口同步
- `tools/run-novel-automation.ps1` / `tools/run-novel-automation.sh` 增加后端参数透传：
  - 可直接在自动循环中指定 backend/model/base_url/command。
- `GETTING-STARTED.md` 增加多后端示例（OpenAI、OpenAI-compatible、Alma、自定义命令）。

## [6.3.4] - 2026-02-22

### 🛠️ Runner 可靠性修复（Strict Loop Reliability）

#### 修复
- `tools/novel_agent_runner.py`：
  - `--max-iterations` 改为“本次运行步数”语义，不再受历史 `RUNNER_STATE.iteration` 影响
  - QA/Polisher 自动写入 `passes=true` 后，立即执行一次 `sync_project_views`，修复 `07-项目状态.md` 滞后一轮问题
  - 每轮结束后强制生成下一角色的 `NEXT_PROMPT.md`，确保可直接继续下一轮

#### 影响
- 自动化循环在“分批执行（每次跑1轮）”场景下行为可预测；
- 视图层与 `.context` 状态一致性提升；
- “拿到下一轮提示词”成为默认行为。

## [6.3.3] - 2026-02-22

### ✅ 按需加载可验证化（Context Pack Enforcement）

#### 新增
- `tools/novel_agent_runner.py` 新增“按需加载技能包”执行层：
  - 基于 `scene_types + genre` 自动解析路由文件集合
  - 生成 `novels/<name>/.context/ROUTING_TRACE.json`（可审计加载清单）
  - 生成 `novels/<name>/.context/ROUTING_CONTEXT.md`（注入提示词的上下文摘录）
  - 自动将路由上下文附加到 `NEXT_PROMPT.md`

#### 门禁
- 新增 `gate_context_pack`（默认阻断）：
  - 缺失 `ROUTING_TRACE.json` → 阻断
  - 路由文件缺失 → 阻断
  - 路由文件加载数为 0 → 阻断

#### 行为变化
- QA/Polisher 自动 `passes=true` 前，必须同时通过 `gate_context_pack`。
- 现在可通过门禁结果 + `ROUTING_TRACE.json` 明确验证“是否按需加载成功”。

## [6.3.2] - 2026-02-21

### 🔁 门禁流转与一致性修复（Anti-Stall + Consistency）

#### 修复
- `tools/novel_agent_runner.py`：
  - Critic 阶段一致性检查改为 `FAIL/INFO`（非阻断），`hard_issues>0` 时不再直接停机，而是进入 Reviser 分支
  - 保留 QA / Polisher 的一致性硬伤阻断，严格门禁语义不变
- `tools/runtime_core.py`：
  - `find_next_scene()` 改为按 `chapter_num` 数值优先排序（其次 `id`），避免 `CH100` / `CH99` 字符串排序异常

#### 一致性优化
- `prompts/qa_prompt.md`：移除“QA 直接写 `passes`”要求，统一为 Runner 门禁通过后自动写入
- `prompts/polisher_prompt.md`：移除“Polisher 直接写 `passes`”要求，明确禁止修改 `scene_list.json`
- `references/quality/protocol-compliance.md`：多场景组合与流派示例改为显式路径（`references/scenes/*`、`references/hooks/*`）
- `references/templates/project-status-template.md`：场景触发器示例改为显式路径
- `SKILL.md`：`infinite-flow`、`quick-transmigration` 示例改为 `style-exemplars/*` 显式路径

## [6.3.1] - 2026-02-21

### 🤖 自动化入口对齐 Demo（Automation Loop Alignment）

本版本参考 `auto-coding-agent-demo` 的循环执行范式，增强了小说自动化入口的可观测性与可恢复性。

#### 新增
- `tools/run-novel-automation.ps1` 新增：
  - 每轮剩余任务统计（`remain:A->B`）
  - 每轮推进增量（`delta`）
  - 读取并记录 `RUNNER_STATE.last_error`
  - 每次运行独立日志：`automation/logs/run-<novel>-<pipeline>-<timestamp>.log`
  - `-DelaySeconds` 参数（轮次间隔）
- `tools/run-novel-automation.sh` 同步以上能力（新增 `delay_seconds` 参数）

#### 修改
- `automation/task-template.json` 增加 `meta`、`priority`、`owner`、`blocked_reason` 字段，便于任务编排与阻塞标注
- `automation/progress-template.md` 明确备注推荐格式：`round/remain/delta/error`
- `GETTING-STARTED.md` 更新 Demo 式入口命令与日志说明

#### 行为变化
- 自动化脚本在“剩余章节=0”时自动早停，不再无效空跑
- 每轮失败都会把阻塞原因落到进度记录，便于快速定位门禁卡点

## [6.3.0] - 2026-02-13

### 🏗️ 全面优化 (Comprehensive Optimization)

本版本对整个 Skill 系统进行了全面优化，SKILL.md 从 717 行精简至 ~420 行（↓41%），消除内容重复，统一术语，建立分层加载机制。

#### Breaking Changes
- **SKILL.md 结构重组**：章节顺序完全重新排列，核心协议移至前部
- **协议 SSOT 化**：Phase 0-5 完整定义仅保留在 `protocol-compliance.md`，其他文件通过指针引用
- **术语标准化**：所有模糊指令（"推荐"/"不可跳过"/"可选"/"强制"）替换为 RFC 2119 风格术语

#### 新增
- **`references/quality/enforcement-levels.md`**：执行强度术语标准（MUST/MUST NOT/SHOULD/MAY）
- **`references/core-20-essential.md`**：核心20文件速通清单，分6层按需加载
- **`references/visual-guide.md`**：Mermaid 流程图（入门决策树、Phase 0-5 流程、场景路由）
- **`data/README.md`**：data/ 与 references/templates/ 的区别说明
- **加载模式**：核心20模式（~20文件）/ 标准模式（~60文件）/ 完整模式（108文件）
- **场景检测兜底机制**：未识别场景默认为"日常/叙事"，加载基础三件套
- **Engine 推断规则**：优先读取策划书"金手指"章节，无描述则跳过 Engine 路由

#### 修改
- **SKILL.md** (717→~420行)：
  - 合并三个重叠的"强制"章节为统一的"AI 核心执行系统"
  - Phase 0-5 协议替换为精简摘要 + 指向 protocol-compliance.md 的指针
  - 原创性警示和读取确认合并为"特殊协议"章节
  - Hook 引用表添加交叉引用注释，指向 hooks/README.md
- **`prompts/writer_prompt.md`** (248→72行)：Phase 1-5 重复内容替换为 SSOT 指针
- **`GETTING-STARTED.md`**：版本更新至 v6.3.0，新增"最简使用"和加载模式说明
- **`references/quality/protocol-compliance.md`** (v2.0→v2.1)：
  - 添加 Phase 0.4 工作流阶段加载
  - 添加场景检测兜底机制（2.1.1）
  - 添加 Engine 推断规则
  - Phase 4 质检层级术语标准化（L1=MUST, L2=SHOULD, L3=MAY）
  - 协议执行优先级术语替换

#### 修复
- **版本号统一**：SKILL.md / GETTING-STARTED.md 全部更新至 v6.3.0
- **`references/hooks/README.md`**：删除 `tournament-arc.md` 重复条目
- **`scripts/check_references.py`** 完全重写：
  - 正则动态解析替代硬编码列表
  - 强制 UTF-8 编码（修复 Windows GBK 崩溃）
  - 自动去重（用 set）
  - 同时扫描 SKILL.md + protocol-compliance.md + writer_prompt.md

---

## [6.2.0] - 2026-02-13

### 🔧 系统修复 (System Fixes)

#### 修复
- **统一版本号**：SKILL.md 版本从 4.0.0 更新至 6.2.0
- **修复依赖声明**：移除不存在的 `chinese-humanizer` skill 依赖
- **目录英文化**：workflows/ 目录从中文命名（1-选题定位/）改为英文命名（1-positioning/）
- **增强验证脚本**：validate_integrity.py 现在检查 workflows/ 目录
- **代码风格优化**：统一 novel_agent_runner.py 中的变量命名

#### 新增
- **修复摘要文档**：FIXES_APPLIED.md 记录所有修复内容

---

## [6.1.0] - 2026-02-08

### 🧠 顶级作家思维链协议 (Top-Novelist Thinking Chain)

#### 新增
- **思维链协议**：AI 写作前必须完成 7 步内部推理（场景目的/读者期待/情绪曲线/伏笔检查/技法选择等）
- **写作前强制读取清单**：STATE.md → VOLUME_XX.md → 细纲 → 伏笔表 → 技法文件 → 语言规范
- **写作后强制检查清单**：主线推进/人物成长/伏笔埋设/章末钩子/AI去痕/状态更新

#### 修复
- 修复 5 个 workflow 文件中的 13 处断链引用
- 统一 `golden-three-chapters.md` 路径 (guides/ 而非 hooks/)
- 修正 `genre_registry_v3.json` 路径 (templates/ 而非 root)

---

## [6.0.0] - 2026-02-08

### 🔄 7 阶段创作工作流 (7-Stage Workflow)

本版本引入基于顶级作家调研的 7 阶段创作系统，支持多卷状态跟踪。

#### Breaking Changes
- **新增 `.context/` 目录**：项目级状态跟踪
- **7 阶段替代 4 阶段**：选题定位 → 梗概人设 → 粗纲细纲 → 存稿准备 → 正文连载 → 修改打磨 → 反馈迭代

#### 新增
- **workflows/** 目录：7 个阶段的工作流定义 (`workflow.md`)
- **data/** 目录：状态模板 (`state-template.md`, `volume-template.md`, `session-log-template.md`)
- **多卷支持**：每卷独立 `VOLUME_XX.md` 状态文件
- **会话日志**：`SESSION_LOG.md` 记录每次会话进度

#### 修改
- SKILL.md 新增 v6.0 状态跟踪协议
- quick_start.py 新增 `_gen_context_dir()` 生成状态目录

---

## [5.0.0] - 2026-02-08

### 🔄 可复现性重构 (Reproducibility Overhaul)

本版本彻底解决了"AI 遵从度不一致"的核心问题，引入唯一事实来源 (SSOT) 和渐进式披露协议。

#### Breaking Changes
- **模式简化**：4 种模式 → 2 种模式 (引导式 Guided / 专家式 Expert)
- **文件编号**：标准项目文件从 `00-06 + 07-语言指南` 改为 `00-07` (8件套)

#### 新增
- **SSOT 文件**: `references/project-structure.md` 定义唯一标准项目结构
- **模式检查清单**: `references/modes/guided-mode-checklist.md` / `expert-mode-checklist.md`
- **渐进式披露协议**: AI 每次只生成 1 个文件，生成后请求用户确认
- **8 件套文件**: 新增 `04-伏笔追踪表`, `05-时间线`, `06-细节追踪表`, `07-项目状态`
- **可选补充**: `08-素材碎片`（灵感池/金句库）

#### 修复
- `quick_start.py` 现在生成完整 8 个文件（原 5 个）
- SKILL.md 中的 Hook 引用与实际文件路径对齐

---

## [4.1.1] - 2026-02-08

### 📈 可用性增强 (Usability Improvements)

- **读取确认协议**: 在 SKILL.md 中新增强制性协议，要求 AI 在策划书/章节/质检报告末尾显式列出参考文件来源
- **Theory 目录强化**: 为 5 个理论文件增加"实战转化"章节，将抽象概念转化为可执行行为
  - `writers-philosophy.md` - 增加触发场景和检查点
  - `commercial-success.md` - 增加商业化辅助模板
  - `author-career-survival.md` - 增加职业困境应对指引
  - `learning-from-reading.md` - 增加阅读拆解报告模板
  - `deconstructing-masterpieces.md` - 增加解构任务输出格式

## [4.1.0] - 2026-02-08

### 🐛 质量修复 (Quality Fixes)

本次更新专注于修复 `chinese-novelist` skill 的完整性问题，确保所有引用文件真实存在且路径正确。

- **修复断链**: 修正了 `genre_registry_v3.json` 中引用的 21 个缺失 Hook 文件。
- **路径修正**: 修复了 `SKILL.md` 中 9 处指向错误的 Hook 路径（如 `theory/` -> `guides/`）。
- **脚本增强**: 重写了 `scripts/validate_integrity.py`，支持更严格的路径检查和 UTF-8 编码。

### ✨ 新增 Hook (21个)

补全了所有流派所需的配套技法文件：
- **核心技法**: `action-scene-guide.md` (战斗), `sensory-library.md` (五感), `emotional-beats.md` (情感)
- **世界构建**: `kingdom-building.md`, `resource-management.md`, `world-hopping.md`, `urban-setting.md`
- **流派特色**: `romance-scene-guide.md`, `team-dynamics.md`, `political-intrigue.md`, `golden-three-chapters.md` 等。

## [4.0.0] - 2026-02-07

### 🌟 全能网文助手 (All-Rounder)

本版本完成了“技能补全路线图”的核心阶段，将技能覆盖率从 60% 提升至 95% 以上，并实现了“流派+引擎”的混搭模式和“多平台风格”的质检适配。

### 核心功能升级 (2项)

1.  **混搭引擎启动器 (Mix-and-Match)** (`tools/quick_start.py` v2.0)
    -   支持 **“基础流派 + 金手指引擎”** 的组合启动（例如：凡人流 + 直播系统）。
    -   新增 7 种通用引擎：系统面板、签到、直播、重生、老爷爷、聊天群、无引擎。
    -   新增 `--list-templates` 命令查看所有支持的流派和引擎。

2.  **智能质检系统** (Prompt-Based QA)
    -   提供专业的质检 Prompt 来评估章节质量。
    -   可用 Prompt：`references/prompts/scene-critic.md`（场景质检）、`chief-editor.md`（主编审稿）。
    -   支持在对话中直接调用："请用场景质检标准审查这一章"。

### 实现架构说明

本技能采用 **Prompt 工程 + 少量机械工具** 的混合架构：

**✅ 已实现的机械工具**：
- `tools/quick_start.py` - 项目脚手架生成器（自动创建目录结构和模板文件）
- `tools/loop_manager.py` - 循环管理工具
- `tools/fanfic_helper.py` - 同人辅助工具

**✅ 基于 Prompt 的智能功能**：
所有涉及内容分析、质量评估、风格检测的功能均通过 **Prompt 工程**实现，利用 LLM 的理解能力：
- 场景质量检测 → `references/prompts/scene-critic.md`
- 主编级审稿 → `references/prompts/chief-editor.md`
- 人物一致性检查 → `references/prompts/fanfic-ooc.md`
- 语言质量分析 → `references/prompts/language-analyzer.md` ✨NEW
- 风格漂移检测 → `references/prompts/style-drift-detector.md` ✨NEW

> **设计理念**: 发挥 LLM 在语义理解、创意评估方面的优势，避免硬编码规则的局限性。

### 新增流派范文 (6个 - 补全高频缺口)

- `references/style-exemplars/shenhao.md` - **神豪流**（消费暴击、阶级反转）
- `references/style-exemplars/quick-transmigration.md` - **快穿攻略**（位面节奏、好感度系统）
- `references/style-exemplars/group-pet.md` - **团宠萌宝**（全员宠爱、治愈系）
- `references/style-exemplars/entertainment.md` - **文娱明星**（文抄公、舆论打脸）
- `references/style-exemplars/period-drama.md` - **年代文**（时代红利、极品亲戚）
- `references/style-exemplars/national-fate.md` - **国运直播**（国家绑定、弹幕互动）

### 数据更新 (1个)

- `references/templates/genre_registry_v3.json` - 升级至 v3.0.0
  - 新增 **潇湘、17K、红袖、纵横** 平台映射。
  - 新增 **战神、赘婿、奶爸、神医、马甲** 等下沉市场热门标签。

---

## [3.4.0] - 2026-02-07
...