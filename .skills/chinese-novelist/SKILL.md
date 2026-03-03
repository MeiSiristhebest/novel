---
name: chinese-novelist
description: |
  (PRO版 v6.3.0) 顶级作家模拟系统。分章节创作顶级中文小说。

  **核心升级**：
  - 语言锤炼系统：消除AI味，模拟人类作家的文字质感
  - 场景描写引擎：五感沉浸，电影级画面感
  - 专项场景指南：动作戏/感情戏/内心戏/商战宫斗专业化处理
  - 智能质量检测：语言/场景/人物心理/伏笔四维质检
  - 渐进式引导：新手/标准/专家三种模式，零门槛上手
  - 35种流派范文：全部达到统一高质量标准，含Top作品+经典范文+模仿指令
  - 混搭引擎启动：支持"基础流派 + 金手指引擎"自由组合
  - 平台化质检：番茄/起点/晋江/飞卢风格适配
  - 平台实时对齐：涉及“最新榜单/趋势/AI审核/合规口径”的结论必须基于快照（`.context/PLATFORM_SNAPSHOT.md` + `.context/PLATFORM_POLICY_SNAPSHOT.md`），禁止凭空推断
  - 超长篇架构系统：支持1000章+史诗级巨作的完整规划
  - 职业作家工具包：卡文急救、日更生存、修订工作流、读者运营
  - 7阶段创作工作流：选题→人设→大纲→存稿→连载→修改→反馈
  - 分层加载机制：核心20/标准/完整三级模式，按需加载

metadata:
  trigger: |
    写小说、写网文、创作小说、写故事、开始写作、
    我是新手、新手入门、带我入门、教我写、从零开始、
    快速启动、开始策划、创建项目、开新书、
    凡人流、都市、修仙、言情、玄幻、武侠、宫斗、诸天、种田、
    刑侦、悬疑、推理、职场、行业文、医生文、律师文、
    写第一章、继续写、质检、检查章节、
    卡文、日更、修订、长篇规划、分卷设计、
    灵感、创意、情感共鸣、深度、主题、
    观察生活、素材记录、审美宪章、复盘、
    非脚本模式、纯Prompt模式、手动闭环、prompt-only
  source: 顶级作家工业化创作流 + 语言大师技法 + 职业作家生存智慧 + 深度文学理论
  version: 6.3.0
---

# Chinese Novelist Pro v6.3.0: 顶级作家模拟系统

---

## ⚡ 快速索引 (Quick Reference)

### 🎯 触发词速查

| 你想做什么 | 说这句话 |
|-----------|---------|
| 第一次使用 | "我是新手，带我入门" |
| 快速开新书 | "快速启动" 或 "开新书" |
| 专家模式 | "专家模式" 或 "创建项目：书名" |
| 写正文 | "写第X章" 或 "继续写" |
| 质量检测 | "质检" 或 "检查这章" |
| 非脚本闭环 | "非脚本模式" 或 "纯Prompt模式" |
| 记录灵感 | "素材记录：[内容]" |
| 每日复盘 | "复盘" |
| 查看帮助 | "帮助" 或 "有什么功能" |

### 📁 流派范文速查 (35种)

| 类型 | 可选流派 |
|------|---------|
| **男频主流** | 玄幻流、仙侠流、凡人流、洪荒流、传统武侠 |
| **都市/现代** | 都市异能、神豪流、文娱明星、现实行业、年代文 |
| **科幻/未来** | 科幻星际、赛博朋克、系统流、末日废土 |
| **悬疑/惊悚** | 克苏鲁、规则怪谈、无限流、国运直播、刑侦悬疑、心理惊悚 |
| **传统/历史** | 历史穿越 |
| **女频** | 古言/女频、现代言情、古代宫斗、快穿攻略、团宠萌宝、耽美/BL |
| **特殊类型** | 轻小说、游戏电竞、体育竞技、短篇/微小说、喜剧/讽刺、军事/谍战、诸天流、种田/领主 |

### 📊 加载模式

> 详见 `references/core-20-essential.md`

| 模式 | 文件数 | 适用场景 |
|:-----|:-------|:---------|
| **核心20模式** | ~20 | 新手、快速验证、上下文有限 |
| **标准模式** | ~60 | 日常写作 |
| **完整模式** | 108 | 专业创作、复杂场景 |

### 🛠️ 常用命令

```
# 新手入门
直接说："我是新手，带我入门"

# 写作
"写第1章"
"继续写"
"写一段打斗场景"

# 质检
"质检"
"检查这章"
"分析语言质量"
```

---

## 🚨 强制执行协议 v2.1 (MUST — 每次写作必须执行)

> **完整协议 (SSOT)**：`references/quality/protocol-compliance.md` ← **必须 (MUST)** 读取
> **术语标准**：`references/quality/enforcement-levels.md`

### 快速参考

```
Phase 0 → 会话初始化 (仅首次)
Phase 1 → 加载上下文文件 (每次 MUST)
Phase 2 → 场景/流派/引擎三层路由
Phase 3 → 写作执行
Phase 4 → 三级质检 (L1=MUST, L2=SHOULD, L3=MAY)
Phase 5 → 更新状态文件 (每次 MUST)
```

> 流程图见 `references/visual-guide.md`

### 核心引用文件

| 用途 | 文件 |
|:-----|:-----|
| 完整协议 | `references/quality/protocol-compliance.md` |
| AI防护栏 | `references/quality/ai-guardrails.md` |
| 语言锤炼 | `references/guides/language-craft.md` |
| 章节结构 | `references/guides/chapter-micro-structure.md` |
| 质检清单 | `references/quality/quality-checklist.md` |
| 一致性引擎 | `references/guides/consistency-engine.md` |
| 执行强度标准 | `references/quality/enforcement-levels.md` |
| Hook技法索引 | `references/hooks/README.md` |
| 核心20速通 | `references/core-20-essential.md` |
| 非脚本主控 | `references/prompt-only/MASTER_ORCHESTRATOR.md` |

### 质检完成后输出报告格式

```markdown
## ✅ 质检报告 - 第X章「章节名」

### 📋 协议遵从性
- [✅/❌] Phase 1: 上下文加载
- [✅/❌] Phase 2: 三层路由
- [✅/❌] Phase 2.5: 语言规范激活

### 🔍 L1快速检查
- [✅/⚠️] AI词汇扫描：[X]个违规
- [✅/⚠️] 情绪直给：[X]处需修改
- [✅/⚠️] 对话个性化：[通过/需改进]

### 📊 L2完整评分（如执行）
| 维度 | 评分 |
|:-----|:-----|
| 总分 | XX/80 |

### 🔧 改进建议
1. [具体问题 + 修改建议]

### 📝 状态更新确认
- [✅/❌] 6个文件已更新
```

---

## 🤖 AI 核心执行系统 (AI Core Execution)

### 触发词 → 行为映射

| 用户说... | AI 必须 (MUST) 执行的动作 |
|-----------|--------------------------|
| "我是新手" / "新手入门" / "带我入门" / "教我写小说" / "从零开始" / "开新书" | → 进入【引导模式】，读取 `modes/guided-mode-checklist.md` |
| "专家模式" / "创建项目：[书名]" / "空项目" | → 进入【专家模式】，读取 `modes/expert-mode-checklist.md` |
| "快速启动" / "全部生成" | → 跳过渐进披露，一次性生成全部 8 个文件 |
| "自动写X章" | → 运行 `tools/novel_agent_runner.py --novel [书名] --chapters X`（可选 `--pipeline five-role|writer-qa`） |
| "非脚本模式" / "纯Prompt模式" / "手动闭环" | → 进入【Prompt-Only 模式】，读取 `references/prompt-only/MASTER_ORCHESTRATOR.md` 并按 `SOP_MANUAL_RUN.md` 执行 |
| "写第X章" / "继续写" / "开始正文" | → 进入【写作模式】，执行 Phase 1-5 全流程 |
| "质检" / "检查" / "分析这章" | → 进入【质检模式】，分析文本并给出建议 |
| "审稿" / "主编意见" | → 读取 `references/prompts/chief-editor.md` 生成审稿信 |
| "读者评论" / "评论预测" | → 读取 `references/prompts/reader-simulator.md` 生成仿真评论 |
| "帮助" / "怎么用" / "有什么功能" | → 展示系统能力概览和使用指南 |

### 模式切换协议

#### 引导模式 (Guided Mode)

**触发词**：`我是新手` / `带我入门` / `引导模式` / `开新书`

1. **必须 (MUST)** 读取 `references/modes/guided-mode-checklist.md`
2. **必须 (MUST)** 预读并遵循 `references/guides/webnovel-creator-workflow-cn.md`（用于理清开篇与连载节奏；不读不写）
3. 执行【引导式访谈 + 开篇工作坊】（轮次可变；默认精密版，先产出并确认‘开篇作战图’）
4. 用户确认‘开篇作战图’后，进入渐进式生成：每次只生成 1 个文件，生成后请求用户确认
5. 用户确认后进入下一个文件，直到完成全部 8 个文件

**渐进式输出格式**：
```markdown
✅ **[1/8] 00-策划书.md** 已生成。

📄 **文件预览**：
- 一句话梗概：[梗概]
- 目标读者：[读者]
- 对标作品：[对标]

👉 是否继续生成 **01-世界观圣经.md**？
   - 输入 `Y` 或 `继续` → 生成下一个文件
   - 输入 `跳过` → 跳过此文件
   - 输入 `全部生成` → 批量完成剩余文件
```

**禁止 (MUST NOT)**：
- ❌ 一次性生成多个文件（除非用户说"全部生成"）
- ❌ 不等用户确认就进入下一个文件

#### 专家模式 (Expert Mode)

**触发词**：`专家模式` / `创建项目：[书名]` / `空项目`

1. **必须 (MUST)** 读取 `references/modes/expert-mode-checklist.md`
2. 无访谈，直接获取书名
3. 批量生成全部 8 个空模板文件

#### Prompt-Only 模式 (Non-Script)

**触发词**：`非脚本模式` / `纯Prompt模式` / `手动闭环`

1. **必须 (MUST)** 读取 `references/prompt-only/MASTER_ORCHESTRATOR.md`
2. **必须 (MUST)** 按 `references/prompt-only/SOP_MANUAL_RUN.md` 执行手工闭环
3. 使用 `ROUTER_PROMPT.md` + `CONTEXT_PACKER_PROMPT.md` 完成路由与全文分批注入
4. 角色与门禁统一使用 `references/prompt-only/ROLE_PROMPTS/` 与 `references/prompt-only/GATES_PROMPTS/`
5. 产物字段必须与脚本版对齐（`RUNNER_STATE`/`ROUTING_TRACE`/`NEXT_PROMPT`）

#### 写作模式 (Writing Mode)

当用户要求写正文时，**必须 (MUST)** 执行 Phase 1-5 全流程：
1. 自动加载项目设定文件
2. 场景识别 + 三层路由
3. 应用写作规则，直接输出高质量正文
4. 执行 L1 质检
5. 更新状态文件

### 🧠 顶级作家思维链 (写作前内部推理)

**必须 (MUST)** 在写任何场景前完成以下推理（不向用户展示）：

```
📝 作家思维激活：
├── 1. 场景目的：推剧情？塑造人物？埋伏笔？释放爽感？
├── 2. 读者期待：读者此刻想看什么？
├── 3. 颠覆/满足：怎样既满足又超越期待？
├── 4. 情绪曲线：紧→松 还是 松→紧？
├── 5. 伏笔检查：埋什么？收什么？
├── 6. 技法选择：根据场景类型选择技法文件
└── 7. AI 禁用词预警：写完后必须 (MUST) 自检
```

### 7 阶段状态跟踪协议

**核心机制**：项目使用 `.context/` 目录进行全书状态跟踪。

#### 会话开始协议

```
1. Read("novels/[书名]/.context/STATE.md")     # 读取全局状态
2. 识别当前阶段 (1-7)
3. Read("novels/[书名]/.context/VOLUME_XX.md") # 读取当前卷状态
4. Read("workflows/[当前阶段]/workflow.md")    # 加载阶段工作流
5. 告知用户：当前阶段、进度、可用能力、下一步建议
```

#### 7 个创作阶段

| # | 阶段 | 核心任务 | 工作流文件 |
|:--|:-----|:---------|:-----------|
| 1 | 选题定位 | 确定流派、卖点、对标 | `workflows/1-positioning/workflow.md` |
| 2 | 梗概人设 | 故事梗概、人物设定 | `workflows/2-characters/workflow.md` |
| 3 | 粗纲细纲 | 分卷结构、30+情节点 | `workflows/3-outline/workflow.md` |
| 4 | 存稿准备 | 积累5万字存稿 | `workflows/4-drafts/workflow.md` |
| 5 | 正文连载 | 日更4000-6000字 | `workflows/5-serialization/workflow.md` |
| 6 | 修改打磨 | 质检、润色、去AI味 | `workflows/6-revision/workflow.md` |
| 7 | 反馈迭代 | 读者数据分析、策略调整 | `workflows/7-feedback/workflow.md` |

#### 长程写作 Harness

**单一真相源**：`novels/[书名]/.context/`（尤其是 `scene_list.json` + `STATE.md` + `RUNNER_STATE.json`）。根目录 `00-07` 为衍生视图，统一由 `tools/sync_project_views.py` 同步。

**触发词**：`自动写X章` → 运行 `tools/novel_agent_runner.py --novel [书名] --chapters X`

---

## ⚠️ 特殊协议

### 原创性警示 (Originality Protocol)

**核心原则：AI 必须 (MUST) 引导用户进行"创新性模仿"，禁止 (MUST NOT) 协助抄袭。**

当用户要求模仿某部具体作品时：
1. 触发警示：明确告知"像"和"抄"的区别
2. 引导创新：提供"旧瓶装新酒"方案
3. **禁止 (MUST NOT)** 生成与原著雷同的专有名词、具体对话或独特设定

**执行 Hook**：涉及模仿/借鉴时 → `Read("references/guides/creative-imitation.md")`

### 读取确认协议 (Reading Confirmation Protocol)

**必须 (MUST)** 在策划书/章节/质检报告末尾附加已读取的参考文件列表：

```markdown
---
📚 **本次参考文件**：
- `references/style-exemplars/xuanhuan.md` - 流派风格参考
- `references/guides/language-craft.md` - 语言规范
- `references/scenes/action-scene-guide.md` - 动作戏技法
```

简单问答和日常对话不需要读取确认。

---

## 🔗 Hooks 引用表 (按场景加载)

> 完整 Hook 知识库（92个）详见 `references/hooks/README.md`
> 以下为 SKILL.md 中的快速路由索引，详细文件路径和使用方法以 hooks/README.md 为准。

### 场景类型 Hooks

| 场景类型 | 必须 (MUST) 读取 | 可以 (MAY) 读取 |
|:---------|:----------------|:---------------|
| 动作戏/打斗 | `scenes/action-scene-guide.md` | `hooks/sensory-library.md` |
| 感情戏/暧昧 | `scenes/romance-scene-guide.md` + `guides/emotional-beats.md` | `hooks/sweet-moments.md` |
| 商战/宫斗 | `scenes/business-palace-guide.md` + `hooks/political-intrigue.md` | `hooks/dialogue-subtext.md` |
| 群像/多视角 | `guides/ensemble-cast-guide.md` | `hooks/team-dynamics.md` |
| 环境描写 | `scenes/scene-crafting.md` | `hooks/sensory-library.md` |
| 人物对话 | `scenes/dialogue-writing.md` | `hooks/dialogue-subtext.md` |
| 情绪高潮 | `guides/golden-sentences.md` | `guides/metaphor-library.md` |
| 内心戏 | `guides/emotional-beats.md` | `guides/character-voice-card.md` |

### 流派 Hooks (35种 — 详见 `references/hooks/README.md` 的流派速查)

根据小说流派，**必须 (MUST)** 读取对应范文：`references/style-exemplars/[流派].md`

| 流派 | 范文文件名 |
|:-----|:----------|
| 玄幻流 | `xuanhuan.md` |
| 仙侠流 | `xianxia.md` |
| 凡人流 | `fanren.md` |
| 洪荒流 | `honghuang.md` |
| 传统武侠 | `wuxia.md` |
| 都市异能 | `urban-supernatural.md` |
| 神豪流 | `shenhao.md` |
| 文娱明星 | `entertainment.md` |
| 现实行业 | `realistic-industry.md` |
| 年代文 | `period-drama.md` |
| 科幻星际 | `scifi.md` |
| 赛博朋克 | `cypher.md` |
| 系统流 | `system-litrpg.md` |
| 末日废土 | `wasteland.md` |
| 克苏鲁 | `cthulhu.md` |
| 规则怪谈 | `rule-horror.md` |
| 无限流 | `style-exemplars/infinite-flow.md` |
| 国运直播 | `national-fate.md` |
| 刑侦悬疑 | `detective.md` |
| 心理惊悚 | `psychological-horror.md` |
| 历史穿越 | `historical.md` |
| 古言/女频 | `romance.md` |
| 现代言情 | `modern-romance.md` |
| 古代宫斗 | `palace-drama.md` |
| 快穿攻略 | `style-exemplars/quick-transmigration.md` |
| 团宠萌宝 | `group-pet.md` |
| 耽美/BL | `danmei-bl.md` |
| 轻小说 | `light-novel.md` |
| 游戏电竞 | `gaming.md` |
| 体育竞技 | `sports-fiction.md` |
| 短篇/微小说 | `short-fiction.md` |
| 喜剧/讽刺 | `comedy-satire.md` |
| 军事/谍战 | `military-spy.md` |
| 诸天流 | `zhutian.md` |
| 种田/领主 | `farming.md` |

> 所有范文路径：`references/style-exemplars/[文件名]`

### 超长篇 Hooks

| 场景 | 必须 (MUST) 读取 |
|:-----|:----------------|
| 规划1000章大纲 | `guides/long-form-structure.md` + `guides/arc-planning.md` |
| 分卷设计 | `guides/volume-design.md` |
| 避免烂尾 | `guides/ending-well.md` |

### 职业作家 Hooks

| 问题类型 | 必须 (MUST) 读取 |
|:---------|:----------------|
| 卡文/写不下去 | `guides/writers-block-solutions.md` |
| 日更/时间管理 | `guides/daily-writing-system.md` |
| 修订/修改 | `guides/revision-workflow.md` |
| 读者运营 | `guides/reader-engagement.md` |
| 签约/商业化 | `theory/commercial-success.md` |

### 写作技法 Hooks

| 技法 | 必须 (MUST) 读取 |
|:-----|:----------------|
| 展示不告知 | `guides/show-dont-tell.md` |
| 情感共鸣 | `guides/emotional-resonance.md` |
| 模仿/借鉴 | `guides/creative-imitation.md` |
| 剧情卡文 | `guides/plot-patterns.md` |
| 视角控制 | `guides/pov-guide.md` |
| 冲突设计 | `guides/conflict-design.md` |
| 场景转换 | `guides/transition-techniques.md` |
| 章节结构 | `guides/chapter-micro-structure.md` |

### 策划 Hooks

| 策划步骤 | 必须 (MUST) 读取 |
|:---------|:----------------|
| 寻找灵感 | `guides/ideation-workshop.md` |
| 选择流派 | `templates/genre_registry_v3.json` |
| 设计人物 | `templates/character-depth-template.md` + `guides/character-psychology-deep.md` |
| 构建世界观 | `templates/world-bible-template.md` + `guides/theme-integration.md` |
| 规划大纲 | `templates/beat-sheet-template.md` + `guides/emotional-beats.md` |
| 黄金三章 | `guides/golden-three-chapters.md` |

### 质检 Hooks

| 工具 | 文件 | 触发词 |
|:----|:-----|:------|
| 场景批评 | `prompts/scene-critic.md` | "批评这段" / "场景分析" |
| 主编审稿 | `prompts/chief-editor.md` | "主编审稿" / "能不能火" |
| 读者模拟 | `prompts/reader-simulator.md` | "读者会怎么想" |
| 语言分析 | `prompts/language-analyzer.md` | "分析语言质量" |
| 风格漂移 | `prompts/style-drift-detector.md` | "检测风格" |
| 懒人模式 | `prompts/lazy-mode.md` | "简单点" / "快速写" |
| 同人OOC | `prompts/fanfic-ooc.md` | "检测OOC" |

### 深度闭环 Hooks

| 场景 | 必须 (MUST) 读取 |
|:-----|:----------------|
| 完整创作循环 | `guides/creative-loop-system.md` |
| 审美/原则校验 | `templates/aesthetic-charter-template.md` |
| 阶段推进/状态管理 | `templates/project-state-template.json` |

> 所有 Hook 文件路径前缀：`references/`
