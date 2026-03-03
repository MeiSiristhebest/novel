# AI全流程写作协议 v2.1 (Full-Pipeline Writing Protocol)

> **维护者**：Chinese Novelist Pro Team
> **适用范围**：写作主流程 Phase 0-5 协议
> **状态**：Active (SSOT)
> **最后校验**：2026-03-01

> **🤖 AI系统指令**：本文档是**唯一的全流程主控协议 (SSOT)**。
> 每次写作会话**必须 (MUST)** 按照本文档的 Phase 0-5 顺序执行，**禁止 (MUST NOT)** 跳过任何 Phase。
> 完整协议 = 可靠输出 + 可复现成功 + 全状态追踪
> **术语标准**：参见 `references/quality/enforcement-levels.md`

---

## Phase 0：会话初始化 (Session Init)

**触发条件**：每次新会话开始时 / 用户说"开始写作"

### 0.1 身份确认
- [ ] 读取 `SKILL.md` → 确认身份为"Chinese Novelist Pro"
- [ ] 读取 `AGENTS.md` → 确认触发-响应矩阵

### 0.2 项目全局建模
- [ ] 读取 `00-策划书.md` → 确认书名、核心卖点、目标平台
- [ ] 读取 `01-世界观圣经.md` → 确认世界观规则（力量体系、禁忌）
- [ ] 读取 `02-人物深度档案.md` → 加载所有角色数据
- [ ] 读取 `07-项目状态.md`（或STATE.md） → 确认当前阶段/卷/章

### 0.3 流派能力索引
- [ ] 查询 `references/hooks/README.md` → 确认本项目流派对应的Hub Hook清单
- [ ] 查询 `references/templates/genre_registry_v3.json` → 确认流派范文路径
- [ ] 确认是否需要加载 Engine Module（签到/抽卡/种田等）
  - Engine路由表见下方 [Engine Module路由](#engine-module路由表)

### 0.4 工作流阶段加载
- [ ] 读取 `novels/[书名]/.context/STATE.md` → 识别当前阶段 (1-7)
- [ ] 读取 `workflows/[阶段编号]-[阶段名]/workflow.md` → 加载当前阶段能力和指引

**Phase 0输出**：AI在内部建立项目心智模型，无需输出给用户。

---

## Phase 1：上下文加载 (Context Loading)

**触发条件**：用户说"写第X章" / "继续写" / "正文"
**🚨 CRITICAL — 必须 (MUST) 执行，禁止 (MUST NOT) 跳过任何步骤**

> 参考 `references/guides/consistency-engine.md` 的 **写前加载清单**

### 1.1 状态与进度
- [ ] 读取 `07-项目状态.md`（或`.context/STATE.md`） → 确认当前章节
- [ ] 读取 `.context/VOLUME_XX.md` → 确认本卷剧情弧线、目标

### 1.2 大纲与细纲
- [ ] 读取 `03-分章细纲.md` → 提取本章：
  - 核心事件
  - 场景类型
  - 冲突目标
  - 字数目标

### 1.3 一致性检查
- [ ] 读取 `04-伏笔追踪表.md` → 检查：
  - 需要回收的伏笔
  - 需要埋设的新伏笔
- [ ] 读取 `05-时间线.md` → 确认当前故事时间点
- [ ] 读取 `06-细节追踪表.md`（若不存在可回退 `08-素材碎片.md`；旧名 `06-素材碎片.md` 仅作历史兼容）→ 检查：
  - 人物当前状态（位置、伤势、情绪）
  - 物品持有状态
  - 不可做的事（如：右手断了就不能用右手）

### 1.4 前文衔接
- [ ] 读取上一章最后 500 字 → 确保衔接自然
- [ ] 生成**内部写前摘要**（不写入正文）：

```markdown
## 第[X]章 写前摘要

### 上一章发生了什么
- [一句话概括核心事件]
- [结尾悬念/钩子]

### 当前人物状态
| 人物 | 位置 | 身体状态 | 情绪状态 | 持有物品 |
|-----|------|---------|---------|---------|
| 主角 | [?] | [?]     | [?]     | [?]     |

### 本章必须处理
- [ ] 回应上一章悬念：[?]
- [ ] 推进伏笔：[?]
- [ ] 核心目标：[?]

### 禁止事项（基于细节追踪表）
- ❌ [例如：主角右手已断]
- ❌ [例如：小红已死亡]
```

---

## Phase 2：场景分析与资源路由 (Scene Routing)

**🤖 AI指令**：根据Phase 1提取的场景类型，执行三层路由。

### 2.1 场景类型路由

根据本章大纲中的关键词，匹配场景类型，加载对应文件：

| 场景类型 | 识别关键词 | 必读文件 | 可选文件 |
|:--------|:----------|:---------|:---------|
| 🗡️ **动作战斗** | 战斗/打斗/厮杀/对决/追杀 | `scenes/action-scene-guide.md` | `hooks/sensory-library.md` |
| 💘 **情感戏** | 告白/分离/重逢/误会/心动 | `scenes/romance-scene-guide.md` + `guides/emotional-beats.md` | `hooks/sweet-moments.md` |
| 👊 **打脸场景** | 羞辱/轻视/震惊/逆袭/碾压 | `hooks/face-slapping.md` | `hooks/audience-reaction.md` |
| 🏠 **家族斗争** | 宗族/亲戚/长辈欺压/极品 | `hooks/family-conflict.md` | `hooks/power-struggle.md` |
| 🌟 **突破晋级** | 突破/晋级/领悟/顿悟/升级 | `hooks/power-system.md` | `hooks/sensory-library.md` |
| 🎯 **关键对话** | 谈判/揭秘/对峙/告知真相 | `hooks/dialogue-subtext.md` + `scenes/dialogue-writing.md` | `hooks/tension-building.md` |
| 🛡️ **生死危机** | 绝境/濒死/追杀/陷阱 | `hooks/tension-building.md` + `hooks/suspense-building.md` | `hooks/sensory-library.md` |
| 🎪 **日常生活** | 修炼/日常/休息/准备 | `guides/chapter-micro-structure.md` | `hooks/relaxed-tone.md` |
| 🏟️ **比赛竞技** | 比赛/对抗/竞赛/排位 | `hooks/match-commentary.md` + `hooks/match-tension.md` | `hooks/tournament-arc.md` |
| 👥 **群像/团战** | 团队/合作/配合/多人 | `guides/ensemble-cast-guide.md` + `hooks/team-dynamics.md` | `hooks/rivalry-dynamics.md` |
| 🏰 **副本探险** | 副本/迷宫/古墓/秘境 | `hooks/dungeon-design.md` + `hooks/tension-building.md` | `hooks/map-design.md` |
| 🎭 **商战权谋** | 朝堂/博弈/阴谋/商战 | `scenes/business-palace-guide.md` + `hooks/political-intrigue.md` | `hooks/bureaucracy-rules.md` |

**多场景组合**：一章可匹配多个场景类型，全部加载对应文件。
- 战斗+打脸 → 加载 `references/scenes/action-scene-guide.md` + `references/hooks/face-slapping.md`
- 情感+危机 → 加载 `references/scenes/romance-scene-guide.md` + `references/hooks/tension-building.md`
- 副本+团战 → 加载 `references/hooks/dungeon-design.md` + `references/hooks/team-dynamics.md`

### 2.1.1 场景检测兜底机制

当场景类型**无法识别**时（大纲关键词不匹配上表任何类型）：

- **必须 (MUST)** 默认归类为"日常/叙事场景"
- **必须 (MUST)** 加载以下基础文件：
  - `references/guides/language-craft.md`
  - `references/guides/chapter-micro-structure.md`
  - `references/quality/ai-guardrails.md`
- **可以 (MAY)** 询问用户确认场景类型后再加载专项 Hook

### 2.2 流派Hook路由

> 参考 `references/hooks/README.md` 的分类索引

根据**项目流派**（从STATE.md获取），额外加载流派专属Hook：

| 流派 | 核心必读Hook | 辅助Hook |
|:----|:------------|:---------|
| **系统流/LitRPG** | `system-panel.md`, `gamification.md`, `game-mechanics.md` | `gold-finger-design.md`, `level-design.md` |
| **凡人流/修仙** | `power-system.md`, `resource-economy.md`, `auction-house.md` | `master-disciple.md`, `faction-design.md` |
| **悬疑/推理/克苏鲁** | `suspense-building.md`, `clue-dropping.md`, `logical-twist.md` | `unknown-fear.md`, `sanity-check.md` |
| **民俗志怪恐怖** | `folk-customs.md`, `ritual-horror.md`, `unknown-fear.md` | `clue-dropping.md`, `tension-building.md` |
| **言情/古言/宫斗** | `romance-triggers.md`, `emotional-buildup.md`, `dialogue-subtext.md` | `betrayal-impact.md`, `culture-customs.md` |
| **电竞/竞技/体育** | `game-mechanics.md`, `match-commentary.md`, `match-tension.md` | `rivalry-dynamics.md`, `training-montage.md` |
| **直播文/国运文** | `hooks/audience-reaction.md`, `hooks/danmu-reaction.md`, `hooks/national-pride.md` | `hooks/face-slapping.md`, `hooks/misunderstanding.md` |
| **赛博朋克/科幻** | `high-tech-low-life.md`, `tech-description.md` | `scientific-research.md`, `survival-guide.md` |
| **种田/领主/基建** | `kingdom-building.md`, `resource-management.md` | `trade-routes.md`, `resource-economy.md` |
| **无限流/综漫** | `hooks/world-hopping.md`, `hooks/dungeon-design.md` | `hooks/tension-building.md`, `hooks/team-dynamics.md` |

### 2.3 Engine Module路由表

根据**金手指/玩法类型**（从策划书/世界观获取），加载引擎模块：

#### Engine 推断规则

- **必须 (MUST)** 优先读取策划书（`00-策划书.md`）中的"金手指"章节来确定 Engine 类型
- 无 Engine 描述 → 跳过 Engine 路由，使用传统叙事模式
- **禁止 (MUST NOT)** 在策划书未明确描述时随意猜测 Engine 类型
- **可以 (MAY)** 询问用户确认 Engine 类型

| 玩法类型 | Engine文件 |
|:--------|:----------|
| 签到/打卡系统 | `engine-modules/sign-in-system.md` |
| 抽卡/转盘系统 | `engine-modules/draw-card.md` |
| 宠物/御兽系统 | `engine-modules/pet-system.md` |
| 种田/基建系统 | `engine-modules/infrastructure-farming.md` |
| 聊天群/论坛系统 | `engine-modules/chat-group.md` |
| 拍卖行机制 | `engine-modules/auction-house.md` |
| 爷爷/老祖系统 | `engine-modules/grandfather.md` |
| 战神回归系统 | `engine-modules/god-of-war.md` |
| 娱乐明星系统 | `engine-modules/entertainment-star.md` |
| 赛博跑者系统 | `engine-modules/cyberpunk-runner.md` |
| 无限流副本 | `engine-modules/infinite-flow.md` |
| 快穿系统 | `engine-modules/quick-transmigration.md` |
| 团宠/萌宝系统 | `engine-modules/group-pet-baby.md` |
| 假千金/真千金 | `engine-modules/fake-heiress.md` |
| 火葬场/追妻 | `engine-modules/crematorium.md` |
| 宅斗/宫斗机制 | `engine-modules/house-conflict.md` |
| 医妃/药妃系统 | `engine-modules/medical-consort.md` |
| 女仙侠系统 | `engine-modules/female-xianxia.md` |

### 2.4 章节结构选择

> 参考 `references/guides/chapter-micro-structure.md`

根据本章场景类型，选择章节骨架模板：

| 场景类型 | 推荐结构 |
|:--------|:---------|
| 打脸/逆袭 | **打脸章**：压抑→转机→爆发→余韵 |
| 探索/解谜 | **探索章**：困惑→探索→惊吓→逃离 |
| 感情/日常 | **感情章**：氛围→互动→波折→升华 |
| 通用 | **标准章**：开篇钩子(5%)→铺垫阻力(30%)→高潮转折(50%)→结尾钩子(15%) |

### 2.5 语言规范激活

- [ ] 加载 `references/guides/language-craft.md` 核心原则
  - 节奏控制（长短句交替）
  - 动词优先（精准有力的动词替代形容词堆砌）
  - 留白技巧（不说满）
- [ ] 加载 `references/quality/ai-guardrails.md` 禁用词清单
  - 绝对禁用词：此外、然而、非常、值得注意的是...
  - 禁用句式：一丝...、不禁...、缓缓地...
- [ ] 加载 `references/guides/show-dont-tell.md` 展示原则
- [ ] 加载流派范文 → 激活风格模仿

---

## Phase 3：写作执行 (Writing Execution)

### 3.1 标准章节骨架

> 参考 `references/guides/chapter-micro-structure.md`

```
[1] 开篇钩子 (前5% ≈ 150字)
    ├─ In Medias Res / 悬念切入 / 反常切入
    ├─ 禁止：天气描写、起床、世界观大段介绍
    └─ 参考：references/guides/hook-techniques.md（10种经典钩子）

[2] 铺垫与阻力 (30% ≈ 900字)
    ├─ 情境建立（谁、在哪、要做什么）
    ├─ 阻力出现（敌人/环境/规则）
    └─ 尝试与失败（第一招失败，情况变糟）

[3] 高潮与转折 (50% ≈ 1500字)
    ├─ 核心冲突（本章最激烈时刻）
    ├─ 主动时刻（主角必须主动做点什么）
    └─ 信息揭示（读者获得新的剧情碎片）

[4] 结尾钩子 (后15% ≈ 450字)
    ├─ 选择一种悬念：危机/信息/选择
    ├─ 参考：references/guides/hook-techniques.md
    └─ 确保读者想看下一章
```

### 3.2 写作规范

- **节奏控制**：动作戏=短句密集；情感戏=慢镜头长句
- **五感沉浸**：每个重要场景至少调动3种感官（参考 `scenes/sensory-library.md`）
- **对话潜台词**：角色不会把心里话全说出来
- **展示不告知**：永远不写"他很愤怒"，要写"他的指节捏得发白"
- **禁用AI词汇**：严格遵守 `ai-guardrails.md` 的禁用清单

---

## Phase 4：三级质检 (Three-Level QA)

**🤖 AI指令**：章节完成后，**立即**执行质检，**不要等用户要求**。

### L1：快速检查（必须 MUST | ~2分钟）

> 每次写完都**必须 (MUST)** 执行，无例外

#### 第1关：AI词汇扫描

扫描生成文本，检测**绝对禁用词汇**：

| 类别 | 禁用词 |
|:----|:-------|
| 学术连接词 | 此外、另外、值得注意的是、综上所述、总而言之 |
| 机械转折 | 句首的"然而"、"但是"、"不过" |
| 过度强调 | 非常、极其、十分、相当、尤其 |
| 抽象总结 | 这表明、这意味着、这说明 |
| AI高频词 | 缓缓、目光、瞬间、不禁、一丝 |

如发现 → 列出位置 + 修改建议

#### 第2关：情绪直给检查

| 禁止（讲述） | 要求（展示） |
|:------------|:------------|
| 他很愤怒 | 他握紧拳头，指节发白 |
| 她很害怕 | 她的瞳孔骤缩，后退一步 |
| 他很开心 | 他嘴角翘起，露出虎牙 |
| 他很紧张 | 他反复捏着衣角 |

#### 第3关：对话个性化

- [ ] 遮住角色名，能分辨谁在说话吗？
- [ ] 是否有潜台词？（角色不会把心里话全说出来）
- [ ] 是否过度礼貌？（真实对话比书面语粗糙）

---

### L2：完整质检（应当 SHOULD | ~5分钟）

> 参考 `references/quality/quality-checklist.md` 的完整清单（263行/80分制）

**评分表**（每项1-10分）：

| 维度 | 评分 | 说明 |
|:-----|:-----|:-----|
| 开头吸引力 | /10 | 前3段是否抓住读者？ |
| 情节推进 | /10 | 本章是否推进主线？ |
| 人物塑造 | /10 | 人物行为一致且有深度？ |
| 对话质量 | /10 | 对话自然且推动情节？ |
| 悬念设置 | /10 | 结尾钩子够硬？ |
| 节奏控制 | /10 | 张弛有度？ |
| 展示而非讲述 | /10 | 用行动/对话而非陈述？ |
| 语言质量 | /10 | 无AI痕迹，用词精确？ |
| **总分** | **/80** | **>60可交付，>70优秀** |

> 参考 `references/quality/genre-quality-checklist.md` 执行流派专项检查

---

### L3：高级分析（可以 MAY | 按需或每5章一次）

以下高级分析工具可通过触发词激活，或在关键节点（卷末/转折章）自动执行：

| 工具 | 文件 | 触发词 | 用途 |
|:----|:-----|:------|:-----|
| 🎭 风格漂移检测 | `prompts/style-drift-detector.md` | "检测风格" / "是不是换人写了" | 对比第1章与当前章的5维风格一致性 |
| 📝 主编审稿 | `prompts/chief-editor.md` | "主编审稿" / "能不能火" | 商业价值S/A/B/C评级 |
| 🎬 场景批评 | `prompts/scene-critic.md` | "批评这段" / "场景分析" | 5维场景品质深度分析 |
| 📖 读者模拟 | `prompts/reader-simulator.md` | "读者会怎么想" | 模拟不同类型读者反应 |
| 🔍 语言分析 | `prompts/language-analyzer.md` | "分析语言质量" | 深度语言指标量化分析 |
| 😴 懒人模式 | `prompts/lazy-mode.md` | "简单点" / "快速写" | 最小化流程的快速写作 |
| 🎭 同人OOC检测 | `prompts/fanfic-ooc.md` | "检测OOC" | 同人角色一致性检测 |

**建议自动触发节点**：
- 每卷末尾 → 自动执行风格漂移检测
- 黄金三章（第1-3章）完成后 → 自动执行主编审稿
- 重要战斗/情感高潮章 → 自动执行场景批评

---

## Phase 5：状态更新与一致性维护 (State Update)

> 参考 `references/guides/consistency-engine.md` 的 **增量更新机制**

**🚨 每章写完后，必须 (MUST) 更新以下文件：**

### 5.1 必更新文件

| 文件 | 更新内容 |
|:----|:---------|
| `07-项目状态.md` (STATE.md) | 当前章节+1、场景类型、总字数累计 |
| `.context/VOLUME_XX.md` | 章节状态：⏳ → ✅，更新剧情摘要 |
| `03-分章细纲.md` | 标记本章完成，填写实际摘要（如与计划有偏差，记录偏差） |
| `04-伏笔追踪表.md` | 标记已揭示的伏笔、添加新埋的伏笔 |
| `05-时间线.md` | 添加本章时间节点和事件 |
| `06-细节追踪表.md` | 更新人物/物品/地点的状态变化（`08-素材碎片.md` 仅作可选补充；旧名 `06-素材碎片.md` 仅作历史兼容） |

> SSOT 规则：运行时状态以 `.context/` 为准；根目录 `00-07` 建议通过 `tools/sync_project_views.py` 进行衍生同步。

### 5.2 一致性校验

更新前执行快速校验：
- [ ] 本章出场人物是否都还活着/在场？
- [ ] 人物称呼是否与之前一致？
- [ ] 物品使用是否之前已获得？
- [ ] 消耗品数量是否正确？
- [ ] 时间流逝是否合理？

---

## 📊 质检结果报告模板

所有检查完成后，生成如下报告：

```markdown
## ✅ 质检报告 - 第X章「章节名」

### 📋 协议遵从性
- [✅/❌] Phase 1: 上下文加载（STATE + VOLUME + 细纲 + 伏笔 + 时间线 + 细节表）
- [✅/❌] Phase 2: 场景路由（场景类型 + 流派Hook + Engine + 章节结构）
- [✅/❌] Phase 2.5: 语言规范激活（language-craft + ai-guardrails）

### 🔍 L1快速检查
- [✅/⚠️] AI词汇扫描：[X]个违规
- [✅/⚠️] 情绪直给：[X]处需修改
- [✅/⚠️] 对话个性化：[通过/需改进]

### 📊 L2完整评分（如执行）
| 维度 | 评分 |
|:-----|:-----|
| 开头吸引力 | X/10 |
| 情节推进 | X/10 |
| ... | ... |
| **总分** | **XX/80** |

### 🔧 改进建议
1. [具体问题 + 修改建议]
2. ...

### 📝 状态更新确认
- [✅/❌] 项目状态已更新
- [✅/❌] 伏笔表已更新
- [✅/❌] 时间线已更新
- [✅/❌] 细节追踪表已更新
```

---

## 🔄 会话结束自检

**🤖 AI指令**：会话结束前，运行总体自检：

- [ ] 每次写作前是否执行了Phase 1（上下文加载）？
- [ ] 每次写作前是否执行了Phase 2（场景路由）？
- [ ] 每次写作后是否执行了Phase 4（至少L1质检）？
- [ ] 每次写作后是否执行了Phase 5（状态更新）？
- [ ] 是否有需要补救的遗漏步骤？

如有未执行项 → 在会话结束时主动告知用户。

---

## 🎯 协议执行优先级

### 必须 (MUST) 执行（任何情况下禁止跳过）

1. Phase 1: 上下文加载（STATE + 细纲 + 伏笔表）
2. Phase 2.1: 场景类型路由（含兜底机制）
3. Phase 2.5: 语言规范激活（ai-guardrails.md）
4. Phase 4 L1: 快速三关质检
5. Phase 5.1: 状态更新6个文件

### 应当 (SHOULD) 执行（除非有明确理由）

1. Phase 0: 会话初始化全局建模
2. Phase 1.3: 一致性检查（时间线+细节表）
3. Phase 2.2: 流派Hook路由
4. Phase 4 L2: 完整80分评分

### 可以 (MAY) 执行（时间允许或关键节点）

1. Phase 2.3: Engine Module路由
2. Phase 4 L3: 高级分析工具
3. 风格漂移检测（每卷末）

---

**⚠️ 最后提醒**：此文档不是"建议"，是**必须 (MUST) 执行的协议**。
**每一次写作都必须 (MUST) 走完 Phase 1-5 全流程。不走全流程 = 不合格。**
