# MASTER_ORCHESTRATOR（Prompt-Only）

> 目标：在不运行脚本的前提下，手工完成与 `novel_agent_runner.py` 等价的单轮或多轮写作闭环。

## 输入（每轮）
必须粘贴以下内容（建议按顺序）：
1. `.context/scene_list.json`
2. `.context/STATE.md`
3. `.context/RUNNER_STATE.json`
4. 当前章节相关素材（`03-分章细纲.md`、`04-伏笔追踪表.md`、`05-时间线.md`、`06-细节追踪表.md`）
5. （可选/推荐）`.context/PLATFORM_SNAPSHOT.md`（仅当本轮要生成/更新《平台策略卡》或讨论“最新榜单/当前风向/总榜Top”时必须提供）
6. （可选/推荐）`.context/PLATFORM_POLICY_SNAPSHOT.md`（仅当本轮要生成/更新《平台策略卡》或讨论“平台是否反AI/如何审核/合规口径”时必须提供）
7. （可选/推荐）`.context/PLATFORM_STRATEGY_CARD.md`（若目标平台已明确则必须提供）

## 平台对齐（Prompt-Only 的硬门槛）
- 若你已明确目标平台（起点/番茄/晋江/飞卢），每轮都必须提供 `.context/PLATFORM_STRATEGY_CARD.md`。
- 若缺失：本轮直接停机，先根据 `references/guides/platform-playbook-cn.md` 生成策略卡（模板见 `references/prompt-only/MANUAL_TEMPLATES/PLATFORM_STRATEGY_CARD.template.md`）。

## Phase 0：运行态确认
1. 识别 `next_role`、`current_chapter`、`pipeline`。
2. 识别当前待写章节（`scene_list` 第一条 `passes=false`）。
3. 输出 `ROUND_CONTEXT`（仅摘要，不改状态）。

## Phase 1：自动路由
1. 调用 `references/prompt-only/ROUTER_PROMPT.md`。
2. 产出 `.context/ROUTING_TRACE.json` 草案（含 required/selected/deferred/batches/selection_reason，格式见 `references/prompt-only/MANUAL_TEMPLATES/ROUTING_TRACE.template.json`）。
3. 若 required 文件缺失，直接阻断。

## Phase 2：上下文打包
1. 调用 `references/prompt-only/CONTEXT_PACKER_PROMPT.md`。
2. 对 selected 文件做全文注入。
3. 超限则进入 batch_2 / batch_3，直到：
   - required 文件全部完成注入；且
   - 当前轮可执行角色。

## Phase 3：角色执行
- five-role：initializer → planner → drafter → critic → reviser → polisher
- writer-qa：initializer → writer → qa

角色输出必须遵循 `references/prompt-only/OUTPUT_CONTRACTS.md`。

## Phase 4：门禁执行（严格阻断）
按顺序调用 `GATES_PROMPTS/`：
1. gate_scene_schema
2. gate_context_pack
3. gate_platform_snapshots
4. gate_chapter_wordcount
5. gate_chapter_title
6. gate_l1
7. gate_consistency
8. gate_state_sync

规则：任一 `blocking=true && passed=false` 立即停机。

## Phase 5：状态更新与下一轮
通过后输出三块：
1. `.context/RUNNER_STATE.json` 更新建议
2. `scene_list` 更新建议（仅 QA/Polisher 且门禁全通过时设置当前章 `passes=true`）
3. `.context/NEXT_PROMPT.md`（下一角色，格式见 `references/prompt-only/MANUAL_TEMPLATES/NEXT_PROMPT.template.md`）

## 输出要求
每轮最终输出四个区块：
1. `.context/ROUTING_TRACE.json`
2. `.context/GATE_REPORT.json`（格式见 `references/prompt-only/MANUAL_TEMPLATES/GATE_REPORT.template.json`）
3. `STATE_PATCH`
4. `.context/NEXT_PROMPT.md`

## 强制禁止
1. 不得跳章推进。
2. 不得在门禁失败时给 PASS。
3. 不得输出非结构化“口头结论”替代 JSON。
