# PROGRESSIVE_DISCLOSURE_PROTOCOL（渐进式披露协议）

> 目标：禁止一次性把所有 `.context` 和设定文件全文塞进上下文；必须按层级、按角色、按触发逐步展开。

## 一、总原则
1. 先读 `STATE.md`、`scene_list.json`、`RUNNER_STATE.json`，确认当前章节与角色。
2. 再读当前轮必须的卷级/章级锚点。
3. 再按角色读取关联文件，禁止全量扫库。
4. 每一轮都要记录：为什么读这个文件、它服务哪个决策、读完会回写到哪里。
5. `ROUTING_CONTEXT.md` 只能保存清单、证据、摘要，不保存全文注入内容。

## 二、四层读取模型
### L0 运行态层（必须先读）
- `.context/STATE.md`
- `.context/scene_list.json`
- `.context/RUNNER_STATE.json`

用途：确定 `chapter_id`、`next_role`、强制门禁、当前激活锚点。

### L1 当前章骨架层
- `03-分章细纲.md` 的当前章、前一章、后一章
- `.context/VOLUME_XX.md`
- 当前卷 Arc 细纲
- `04-伏笔追踪表.md`
- `05-时间线.md`
- `06-细节追踪表.md`

用途：确定本章任务、上下文滑窗、因果连续性。

### L2 战略与高阶层（按触发读取）
- `MARKET_BET.md`
- `STRATEGIC_CONTROL.md`
- `VOICE_BIBLE.md`
- `READER_PSYCHOLOGY_MODEL.md`
- `NOVELTY_LAB.md`
- `CHARACTER_AUTONOMY.md`
- `DANGEROUS_BET_REGISTER.md`
- `AESTHETIC_LADDER.md`
- `READER_STATE_MACHINE.md`
- `CHARACTER_PRESSURE_INDEX.md`
- `SACRIFICE_LEDGER.md`
- `MIRACLE_CANDIDATES.md`

用途：只给相关角色，不进入所有轮次。

### L3 外部信号层（最晚读取）
- `LIVE_SIGNAL_POLICY.md`
- `LIVE_SIGNAL_SOURCES.md`
- `ARCHAEOLOGY_PROTOCOL.md`
- `SIGNAL_VALUE_GATE.md`
- `LIVE_SIGNAL_DECAY_RULE.md`
- `LIVE_SIGNAL_SNAPSHOT.md`
- `LIVE_SIGNAL_INGESTION.md`
- `ARCHAEOLOGY_LOG.md`
- `PLATFORM_*` 文件

用途：校准与约束，不直接生成正文表达。

## 三、角色读取矩阵
### writer
- 必读：L0 + L1 + `MARKET_BET.md` + `STRATEGIC_CONTROL.md` + `VOICE_BIBLE.md`
- 按需：`NOVELTY_LAB.md`、`READER_PSYCHOLOGY_MODEL.md`、`CHARACTER_AUTONOMY.md`、`MIRACLE_CANDIDATES.md`
- 禁止直接读取：`LIVE_SIGNAL_SNAPSHOT.md`

### signal_curator
- 必读：L0 + `LIVE_SIGNAL_*` + `SIGNAL_VALUE_GATE.md` + `ARCHAEOLOGY_PROTOCOL.md`
- 输出去向：`LIVE_SIGNAL_INGESTION.md`、`ARCHAEOLOGY_LOG.md`

### dangerous_bet_lab / novelty_lab
- 必读：L0 + `MARKET_BET.md` + `NOVELTY_LAB.md` + `DANGEROUS_BET_REGISTER.md`
- 可读：`LIVE_SIGNAL_SNAPSHOT.md`，但只能用于抽象校准

### reader_psychology_director / reader_behavior_modeler
- 必读：L0 + `READER_PSYCHOLOGY_MODEL.md` + `READER_STATE_MACHINE.md`
- 可读：`LIVE_SIGNAL_INGESTION.md`、`ARCHAEOLOGY_LOG.md`

### character_pressure_test / character_gravity_director / voice_auditor
- 必读：L0 + `VOICE_BIBLE.md` + `CHARACTER_AUTONOMY.md` + `CHARACTER_PRESSURE_INDEX.md`

### ruthless_cut_review / story_director
- 必读：L0 + `STRATEGIC_CONTROL.md` + `SACRIFICE_LEDGER.md`
- 可读：`MARKET_BET.md`、`DANGEROUS_BET_REGISTER.md`

### miracle_moment_lab
- 必读：L0 + 当前章正文 + `VOICE_BIBLE.md` + `MIRACLE_CANDIDATES.md`
- 禁止：用外部热信号直接造句

## 四、回写原则
1. 危险下注结论回写 `DANGEROUS_BET_REGISTER.md` 或 `STRATEGIC_PACKET.json`。
2. 审美升级结论回写 `AESTHETIC_LADDER.md` 摘要和 `HIGH_ORDER_PACKET.json`。
3. 读者动态判断回写 `READER_STATE_MACHINE.md` 的状态结论摘要。
4. 人物压场评估回写 `CHARACTER_PRESSURE_INDEX.md`。
5. 被砍掉的“局部好东西”回写 `SACRIFICE_LEDGER.md`。
6. 记忆点候选只回写 `MIRACLE_CANDIDATES.md` 或包文件，不污染长期正文锚点。
