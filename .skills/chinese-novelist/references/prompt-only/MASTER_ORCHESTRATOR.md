# MASTER_ORCHESTRATOR（Prompt-Only）

> 目标：在不运行脚本的前提下，手工完成与 `novel_agent_runner.py` 等价、但增加战略层、发布性控制和高阶创作能力的单轮或多轮写作闭环。

## 先读两份协议
1. `PROGRESSIVE_DISCLOSURE_PROTOCOL.md`
2. `FILE_RELATION_MAP.md`

## 输入（每轮）
必须按渐进式披露顺序粘贴，而不是一次性全贴：

### L0 运行态层
1. `.context/scene_list.json`
2. `.context/STATE.md`
3. `.context/RUNNER_STATE.json`

### L1 当前章骨架层
4. 当前章节相关素材（`03-分章细纲.md`、`00-全局设定/04-伏笔追踪表.md`、`00-全局设定/05-时间线.md`、`00-全局设定/06-细节追踪表.md`）
5. `.context/VOLUME_XX.md` 或当前卷锚点

### L2 战略与高阶层（按路由追加）
6. `.context/STRATEGIC_CONTROL.md`
7. `.context/VOICE_BIBLE.md`
8. `.context/PUBLISHABILITY_POLICY.md`
9. `.context/MARKET_BET.md`
10. `.context/READER_PSYCHOLOGY_MODEL.md`
11. `.context/NOVELTY_LAB.md`
12. `.context/CHARACTER_AUTONOMY.md`
13. `.context/DANGEROUS_BET_REGISTER.md`
14. `.context/AESTHETIC_LADDER.md`
15. `.context/READER_STATE_MACHINE.md`
16. `.context/CHARACTER_PRESSURE_INDEX.md`
17. `.context/SACRIFICE_LEDGER.md`
18. `.context/MIRACLE_CANDIDATES.md`

### L3 外部信号层（最晚追加）
19. `.context/LIVE_SIGNAL_POLICY.md`
20. `.context/LIVE_SIGNAL_SOURCES.md`
21. `.context/ARCHAEOLOGY_PROTOCOL.md`
22. `.context/SIGNAL_VALUE_GATE.md`
23. `.context/LIVE_SIGNAL_DECAY_RULE.md`
24. `.context/LIVE_SIGNAL_SNAPSHOT.md`
25. `.context/LIVE_SIGNAL_INGESTION.md`
26. `.context/ARCHAEOLOGY_LOG.md`
27. `.context/CONTENTANY_ALIGNMENT.md`
28. `.context/PLATFORM_STRATEGY_CARD.md`
29. `.context/PLATFORM_SNAPSHOT.md`
30. `.context/PLATFORM_POLICY_SNAPSHOT.md`

## Phase 0：运行态确认与双层触发检测
1. 识别 `next_role`、`current_chapter`、`pipeline`。
2. 识别当前待写章节（`scene_list` 第一条 `passes=false`）。
3. 执行一致性预检（阻断级）。
4. 按 `PROGRESSIVE_DISCLOSURE_PROTOCOL.md` 确认本轮只读取必要层级。
5. 执行信号入口预检：
   - 一切外部信号先过 `.context/SIGNAL_VALUE_GATE.md`
   - 一切信息采集先遵守 `.context/LIVE_SIGNAL_SOURCES.md`
   - 一切考古先遵守 `.context/ARCHAEOLOGY_PROTOCOL.md`
   - 一切实时信号先过 `.context/LIVE_SIGNAL_DECAY_RULE.md`
   - 若本轮要引入新信号，先执行 `signal_curator`
6. 生成 `STRATEGIC_PLAN`。
7. 生成 `HIGH_ORDER_PLAN`。
8. 生成 `AESTHETIC_DELTA_PLAN`。
9. 若提供 `LIVE_SIGNAL_SNAPSHOT.md`，只能作为 `signal_curator` 与高阶角色输入，不允许直接入正文。

## Phase 1：自动路由
1. 调用 `references/prompt-only/ROUTER_PROMPT.md`。
2. 产出 `.context/ROUTING_TRACE.json` 草案。
3. 若 required 文件缺失，直接阻断。
4. 每个 required/selected 文件都必须说明其上游、下游、服务的决策。

## Phase 2：上下文打包
1. 调用 `references/prompt-only/CONTEXT_PACKER_PROMPT.md`。
2. 严格按 L0 -> L1 -> L2 -> L3 顺序打包。
3. `ROUTING_CONTEXT.md` 仅保留清单、层级、证据、引用关系，不落盘全文正文。

## Phase 3：角色执行
### 3.1 前置战略角色（按需）
- `market_bet`
- `story_director`
- `dangerous_bet_lab`
- `aesthetic_upgrade_director`

### 3.2 前置信号角色（按需）
- `signal_curator`

### 3.3 前置高阶角色（按需）
- `novelty_lab`
- `reader_psychology_director`
- `reader_behavior_modeler`
- `ruthless_cut_review`
- `character_pressure_test`
- `character_gravity_director`

### 3.4 核心写作角色
- five-role：initializer -> planner -> drafter -> critic -> reviser -> polisher
- writer-qa：initializer -> writer

### 3.5 后置高阶强化角色
- `miracle_moment_lab`

### 3.6 后置战略与质检角色
- `voice_auditor`
- `qa`
- `chief_editor`
- `feedback_triage`

## Phase 4：门禁执行（严格阻断）
按顺序调用 `GATES_PROMPTS/`：
1. gate_scene_schema
2. gate_context_pack
3. gate_platform_snapshots
4. gate_chapter_wordcount
5. gate_chapter_title
6. gate_l1
7. gate_consistency
8. gate_layout_compliance
9. gate_detail_specificity
10. gate_voice_uniqueness
11. gate_homogeneity_risk
12. gate_strategic_packet
13. gate_high_order_packet
14. gate_aesthetic_delta
15. gate_quality_bar
16. gate_memorable_line_or_action
17. gate_publishability
18. gate_state_sync

## Phase 5：状态更新与下一轮
通过后输出五块：
1. `.context/STRATEGIC_PACKET.json`
2. `.context/HIGH_ORDER_PACKET.json`
3. `.context/RUNNER_STATE.json` 更新建议
4. `scene_list` 更新建议
5. `.context/NEXT_PROMPT.md`

## 强制禁止
1. 不得跳章推进。
2. 不得采集不能改变决策的信息。
3. 不得把实时热词直接写进正文冒充新鲜感。
4. 不得让实时信号推翻主赌注与人物弧线。
5. 不得在缺少 `voice_audit` 时放行章节。
6. 不得使用异常排版、故意错字、伪口语断句作为“反检测手段”。
7. 不得让实时信号越过抽象层直接影响 `writer` 的语言表层。
8. 不得因为局部精彩而保留会拖死全书上限的内容。
9. 不得把“稳妥合格”当成审美升级的替代品。
10. 不得一次性把所有文件全文注入；必须遵守渐进式披露与文件关系图。
