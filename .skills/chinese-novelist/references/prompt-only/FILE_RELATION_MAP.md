# FILE_RELATION_MAP（文件关系图）

## 目标
为 `prompt-only` 体系提供统一的“谁依赖谁、谁产出给谁、谁回写到哪”的关系图。

## 核心依赖链
### 运行链
`STATE.md` -> `scene_list.json` -> `ROUTER_PROMPT.md` -> `CONTEXT_PACKER_PROMPT.md` -> `MASTER_ORCHESTRATOR.md`

### 执行链
当前章骨架层 -> `writer` -> `miracle_moment_lab` -> `voice_auditor` -> `qa`

### 战略链
`MARKET_BET.md` -> `DANGEROUS_BET_REGISTER.md` -> `STRATEGIC_CONTROL.md` -> `story_director/chief_editor`

### 审美链
`TOP_AUTHOR_SCORECARD.md` -> `AESTHETIC_LADDER.md` -> `aesthetic_upgrade_director` -> `gate_aesthetic_delta`

### 读者链
`READER_PSYCHOLOGY_MODEL.md` -> `READER_STATE_MACHINE.md` -> `reader_behavior_modeler` -> `feedback_triage`

### 人物链
`VOICE_BIBLE.md` -> `CHARACTER_AUTONOMY.md` -> `CHARACTER_PRESSURE_INDEX.md` -> `character_gravity_director/voice_auditor`

### 删改链
`STRATEGIC_CONTROL.md` -> `SACRIFICE_LEDGER.md` -> `ruthless_cut_review` -> `story_director`

### 记忆点链
当前章正文 -> `MIRACLE_CANDIDATES.md` -> `miracle_moment_lab` -> `gate_memorable_line_or_action`

### 信号链
`LIVE_SIGNAL_POLICY.md` -> `LIVE_SIGNAL_SOURCES.md` -> `SIGNAL_VALUE_GATE.md` -> `LIVE_SIGNAL_DECAY_RULE.md` -> `signal_curator` -> `LIVE_SIGNAL_INGESTION.md` / `ARCHAEOLOGY_LOG.md`

### 门禁链
`voice_auditor/qa/chief_editor/high_order roles` -> `gate_strategic_packet` -> `gate_high_order_packet` -> `gate_aesthetic_delta` -> `gate_quality_bar` -> `gate_memorable_line_or_action` -> `gate_publishability` -> `gate_state_sync`

## 文件标准字段
每个高阶文件至少要能回答四个问题：
1. 我是谁的上游输入？
2. 我是谁的下游输出？
3. 我在哪一层被读取？
4. 我会回写到哪里？
