# 顶级作家模拟系统 - 集成架构 (Integration Architecture)

> **设计理念**：每个模块都是"写作DNA"的一部分，通过 hooks 在写作流程的关键节点自动激活。

---

## 一、系统全景图 (System Overview)

```
┌─────────────────────────────────────────────────────────────────┐
│                    Chinese Novelist Pro                         │
│                    顶级作家模拟系统                                │
└─────────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
   ┌────▼────┐          ┌────▼────┐          ┌────▼────┐
   │ 策划层   │          │ 执行层   │          │ 质检层   │
   │Planning │          │Execution│          │Quality  │
   └────┬────┘          └────┬────┘          └────┬────┘
        │                    │                     │
   ┌────▼────────┐      ┌───▼──────────┐     ┌───▼──────────┐
   │流派基因库    │      │语言锤炼系统   │     │AI痕迹检测     │
   │世界观构建    │      │场景描写系统   │     │风格漂移检测   │
   │人物声音设计  │      │对话张力系统   │     │情节一致性检查 │
   │情绪节拍规划  │      │情绪节奏执行   │     │人物声音校验   │
   └─────────────┘      └──────────────┘     └──────────────┘
```

---

## 二、Hooks 映射表 (Hooks Mapping)

### 阶段 1：作家会议室 (Writers' Room)

| 写作步骤 | 触发的模块 | Hook 名称 | 输出 |
|---------|-----------|----------|------|
| Step 1: 核心概念 | `master-patterns-extended.json` | `hook_genre_matching` | 流派推荐列表 |
| Step 2: 风格定制 | `style-exemplars/` | `hook_style_loading` | 风格范文锁定 |
| Step 3: 角色设计 | `templates/character-depth-template.md` + **NEW: `guides/character-psychology-deep.md`** | `hook_character_voice` | 声音档案 |
| Step 4: 世界观 | `templates/world-bible-template.md` + **NEW: `scenes/sensory-library.md`** | `hook_world_immersion` | 世界质感档案 |
| Step 5: 结构设计 | `guides/emotional-beats.md` + `guides/twist-design-guide.md` | `hook_emotional_map` | 情绪曲线图 |

### 阶段 2：备战 (Pre-production)

| 文档生成 | 触发的模块 | Hook 名称 | 作用 |
|---------|-----------|----------|------|
| 00-策划书 | 所有策划模块汇总 | `hook_pitch_generation` | 整合所有决策 |
| 02-B-人物声音档案 | **NEW: `guides/character-psychology-deep.md`** | `hook_inner_voice` | 内心戏模板 |
| 07-语言风格指南 | **NEW: `guides/language-craft.md` + `guides/metaphor-library.md`** | `hook_language_profile` | 本书专属语言规则 |

### 阶段 3：深度创作 (Deep Writing)

#### 3.1 写前准备 (Context Loading)

#### 3.1 写前准备清单 (Pre-writing Checklist)
以下模块应在每一章开始写作前被加载或查阅：
- [ ] **一致性检查**：查阅 `guides/consistency-engine.md` 以避免逻辑冲突。
- [ ] **情绪节拍规划**：查阅 `guides/emotional-beats.md` 确定本章的情绪曲线（开端-发展-高潮-结尾）。
- [ ] **语言风格锁定**：查阅 `guides/language-craft.md` 确认本书的叙述语调。
- [ ] **场景类型预判**：根据大纲查阅 `scenes/scene-crafting.md` 确定本章主要场景类型。

| 步骤 | 触发条件 | 调用模块 | 输出 |
|-----|---------|---------|------|
| 1. 一致性加载 | 每章开始 | `guides/consistency-engine.md` | 禁止事项清单 |
| 2. 情绪节拍加载 | 每章开始 | `guides/emotional-beats.md` | 本章情绪曲线 |
| 3. 语言风格加载 | 每章开始 | **NEW: `guides/language-craft.md`** | 语言规则集 |
| 4. 场景类型检测 | 分析大纲 | **NEW: `scenes/scene-crafting.md`** | 场景写作策略 |

#### 3.2 撰写正文 (Drafting)

#### 3.2 写作中的实时指引 (Real-time Guidance)
在写作过程中，根据当前撰写的内容类型，实时参考以下指南：

| 正在写的内容 | 参考指南 (Prompt/Guide) |
| :--- | :--- |
| **环境描写** | **`scenes/sensory-library.md`** (五感词库) + **`scenes/scene-crafting.md`** (环境情绪映射) |
| **人物对话** | **`guides/character-voice-card.md`** (声音一致性) + **`scenes/dialogue-writing.md`** (潜台词设计) |
| **动作/战斗** | **`scenes/action-scene-guide.md`** (节奏控制) + **`scenes/sensory-library.md`** (打击感描写) |
| **情感/暧昧** | **`guides/golden-sentences.md`** (金句提取) + **`guides/metaphor-library.md`** (意象隐喻) |
| **章节结尾** | **`guides/emotional-beats.md`** (悬念/钩子检查) |

**实时 Hook 触发示例**：

| 写作场景 | 自动激活 | 提供什么 |
|---------|---------|---------|
| 正在写**环境描写** | `scenes/sensory-library.md` | 五感词汇库 + 环境情绪映射 |
| 正在写**人物对话** | `guides/character-voice-card.md` + `scenes/dialogue-writing.md` | 声音检查 + 潜台词模板 |
| 正在写**动作戏** | `scenes/action-scene-guide.md` | 节奏控制 + 慢镜头技巧 |
| 正在写**感情戏** | `scenes/romance-scene-guide.md` | 暧昧张力 + 身体语言库 |
| 正在写**情绪高潮** | `guides/golden-sentences.md` + `guides/metaphor-library.md` | 金句模板 + 意象库 |

#### 3.3 质量控制 (QC)

#### 3.3 写后质量检查 (Post-writing QC)
写作完成后，请依次运行以下检查指令（Prompts）：
1. **AI 痕迹与语言质量**：运行 `scene-critic.md`
2. **场景表现力**：运行 `scene-critic.md`
3. **人物声音一致性**：对照 `guides/character-voice-card.md`
4. **风格漂移**：对照 `style-exemplars/` 中的范文
5. **情绪传达**：对照 `guides/emotional-beats.md` 检查预期情绪是否达成

---

## 三、新旧模块协同工作示例 (Integration Examples)

### 示例 1：写一场打斗戏

```yaml
场景类型: 动作戏（主角 vs 三个敌人）

# Hook 调用链
1. hook_scene_type_detection (scene-crafting.md)
   └─> 检测到"动作戏" → 激活 action-scene-guide.md

2. hook_action_rhythm (action-scene-guide.md)
   └─> 提供节奏方案: 快-慢-快-爆发

3. hook_sensory_combat (sensory-library.md)
   └─> 调用动作场景专用的五感词汇:
       - 视觉: 寒光、血雾、残影
       - 听觉: 金属碰撞、骨裂声
       - 触觉: 剑风、血腥味

4. hook_language_craft (language-craft.md)
   └─> 应用短句规则 + 动词优先原则

5. hook_emotional_beat (emotional-beats.md)
   └─> 确保"压抑 → 转折 → 高潮"节奏

# 最终输出
┌──────────────────────────────────────┐
│ 高质量动作场景                         │
│ - 节奏紧凑（短句为主）                 │
│ - 画面感强（五感丰富）                 │
│ - 情绪饱满（符合情绪曲线）             │
│ - 无AI味（通过语言规则过滤）           │
└──────────────────────────────────────┘
```

### 示例 2：写人物内心戏

```yaml
场景类型: 主角面临选择（要不要复仇）

# Hook 调用链
1. hook_scene_type_detection
   └─> 检测到"内心戏" → 激活 character-psychology-deep.md

2. hook_inner_voice (character-psychology-deep.md)
   └─> 提供内心戏写法:
       - 碎片化思维流
       - 记忆闪回触发器
       - 情绪与理性的对抗

3. hook_metaphor_selection (metaphor-library.md)
   └─> 调用"情绪/抽象概念"类比喻:
       复仇 → 吞噬自己的毒药

4. hook_golden_sentence (golden-sentences.md)
   └─> 提供升华句式模板

5. hook_voice_consistency (character-voice-card.md)
   └─> 检查内心独白是否符合人物性格

# 最终输出
┌──────────────────────────────────────┐
│ 深刻的人物内心戏                       │
│ - 符合人物性格（声音一致）             │
│ - 有文学深度（比喻/象征）             │
│ - 引发共鸣（真实的心理冲突）           │
└──────────────────────────────────────┘
```

### 示例 3：写感情戏（暧昧/告白场景）

```yaml
场景类型: 男女主角雨中对峙（暧昧升温）

# Hook 调用链
1. hook_scene_type_detection
   └─> 检测到"感情戏" → 激活 romance-scene-guide.md

2. hook_environment_mood (scene-crafting.md)
   └─> 环境映射情绪: 雨 → 压抑中的释放

3. hook_sensory_enhance (sensory-library.md)
   └─> 五感强化:
       - 雨打在脸上的触感
       - 湿透衣服贴在皮肤上
       - 对方呼吸的声音

4. hook_subtext_design (dialogue-writing.md)
   └─> 对话潜台词:
       表面: "你为什么要来？"
       潜台词: "我很高兴你来了"

5. hook_body_language (romance-scene-guide.md)
   └─> 身体语言库:
       - 避开眼神 → 心虚/害羞
       - 攥紧拳头 → 压抑情感

# 最终输出
┌──────────────────────────────────────┐
│ 张力十足的感情戏                       │
│ - 环境有情绪（雨中的暧昧）             │
│ - 对话有层次（潜台词丰富）             │
│ - 细节有温度（五感 + 身体语言）        │
└──────────────────────────────────────┘
```

---

## 四、模块依赖关系图 (Module Dependencies)

```
核心基础层 (Foundation)
├─ quality/ai-guardrails.md ──────────────────┐
├─ guides/consistency-engine.md ─────────────┤ 所有模块必须遵守
└─ guides/emotional-beats.md ────────────────┘

语言表达层 (Language)
├─ guides/language-craft.md (NEW) ───┐
├─ guides/metaphor-library.md (NEW) ─┤ 提升文字质量
└─ guides/golden-sentences.md (NEW) ─┘

场景构建层 (Scene)
├─ scenes/scene-crafting.md (NEW) ────────┐
├─ scenes/sensory-library.md (NEW) ───────┤ 画面感 + 沉浸感
├─ scenes/action-scene-guide.md (NEW) ───┤
└─ scenes/romance-scene-guide.md (NEW) ──┘

人物塑造层 (Character)
├─ guides/character-voice-card.md
└─ guides/character-psychology-deep.md (NEW) ──> 深层内心戏

流派风格层 (Genre)
├─ master-patterns-extended.json
└─ style-exemplars/ ──────────────> 锁定文风

工具检测层 (Tools & Prompts)
├─ quality/ai-guardrails.md
├─ references/prompts/scene-critic.md (NEW)
├─ references/prompts/chief-editor.md (NEW)
└─ references/prompts/reader-simulator.md
```

---

## 五、智能 Hook 触发机制 (Smart Hook Triggering)

### 5.1 基于场景类型的自动识别

### 5.1 场景识别与路由 (Scene Routing)
根据大纲中的关键词，手动或提示 AI 选择对应的写作策略：

| 关键词示例 | 识别场景 | **必读参考文件 (Required Reading)** |
| :--- | :--- | :--- |
| 战斗、打斗、追逐、刺杀 | **动作戏** | `scenes/action-scene-guide.md`, `scenes/sensory-library.md` |
| 告白、暧昧、亲吻、争吵 | **感情戏** | `scenes/romance-scene-guide.md`, `body-language` |
| 回忆、选择、纠结、顿悟 | **内心戏** | `guides/character-psychology-deep.md`, `guides/metaphor-library.md` |
| 描写、城市、森林、进入 | **环境戏** | `scenes/scene-crafting.md`, `scenes/sensory-library.md` |
| 谈判、辩论、审问、对峙 | **对话戏** | `scenes/dialogue-writing.md`, `guides/character-voice-card.md` |

### 5.2 基于情绪节拍的动态加载

### 5.2 情绪节拍指引 (Beat Guidance)
根据当前章节在整体结构中的位置，采用不同的写作策略：

| 章节位置 | 写作任务 | 推荐使用的 Prompt/Guide |
| :--- | :--- | :--- |
| **开篇** | 制造压抑/悬念、代入感 | `scenes/sensory-library.md` (五感沉浸) |
| **铺垫** | 埋设伏笔、展示人物 | `guides/character-voice-card.md` (人物立绘) |
| **转折** | 制造意外、情绪冲击 | `guides/twist-design-guide.md` (反转设计) |
| **高潮** | 金句爆发、动作顶点 | `guides/golden-sentences.md`, `scenes/action-scene-guide.md` |
| **结尾** | 悬念钩子、情绪收尾 | `guides/emotional-beats.md` (钩子检查) |

---

## 六、实战写作流程（整合版）

### 第三阶段：深度创作（增强版）

#### 1. 写前准备（加载 5 项）

```markdown
□ 一致性检查 (guides/consistency-engine.md)
  └─ 生成禁止事项清单

□ 情绪节拍加载 (guides/emotional-beats.md)
  └─ 本章是"高潮章"，使用双峰型曲线

□ 场景类型检测 (scenes/scene-crafting.md) [NEW]
  └─ 检测到"动作戏 + 对话戏"，准备相关模块

□ 语言风格锁定 (guides/language-craft.md) [NEW]
  └─ 本书风格：凡人流（短句、动词优先、少形容词）

□ 人物声音预热 (guides/character-voice-card.md)
  └─ 主角：简短、冷静；反派：冗长、自大
```

#### 2. 撰写正文（实时 Hook 辅助）

```markdown
┌─────────────────────────────────────────┐
│ 正在写: 第 15 章 - 生死对决              │
└─────────────────────────────────────────┘

[段落 1: 环境描写]
→ 触发 hook_sensory_library
  ├─ 视觉: 血色黄昏、破碎石柱
  ├─ 听觉: 风声如泣
  └─ 嗅觉: 血腥味混杂泥土味

[段落 2: 敌人出场]
→ 触发 hook_character_voice
  ├─ 反派说话: 长句、自负、多用"你"
  └─ 潜台词: 轻蔑中透露忌惮

[段落 3-5: 打斗场景]
→ 触发 hook_action_rhythm
  ├─ 节奏: 快-快-慢-爆发
  ├─ 句式: 短句为主，动词开头
  └─ 慢镜头: 关键一击的特写

[段落 6: 主角内心]
→ 触发 hook_character_psychology
  ├─ 碎片化思维: 回忆师父的话
  └─ 情绪冲突: 愤怒 vs 冷静

[段落 7: 反转]
→ 触发 hook_twist_design
  └─ 敌人突然露出破绽（其实是陷阱）

[段落 8: 高潮]
→ 触发 hook_golden_sentence
  └─ 金句: "剑未出鞘，他已经死了。"

[段落 9: 结尾]
→ 触发 hook_cliffhanger
  └─ 钩子: 远处传来更强大的气息
```

#### 3. 质量控制（7 项检查）

```markdown
□ AI痕迹检测 (quality/ai-guardrails.md)
  └─ 检测到 3 处"然而"，已标记

□ 语言质量分析 (scene-critic.md) [NEW]
  ├─ 形容词密度: 6/100字 ✓
  ├─ 短句占比: 65% ✓
  └─ 金句数量: 2 个 ✓

□ 场景质量检查 (scene-critic.md) [NEW]
  ├─ 五感丰富度: 4/5 ✓
  ├─ 动作戏节奏: A级 ✓
  └─ 画面感评分: 8.5/10 ✓

□ 对话声音一致性 (character-voice-card.md)
  └─ 主角 vs 反派 声音区分度: 高 ✓

□ 风格漂移检测 (style-exemplars/)
  └─ 与第1章风格相似度: 92% ✓

□ 情绪节拍验证 (emotional-beats.md)
  └─ 情绪曲线符合双峰型设计 ✓

□ 一致性检查 (consistency-engine.md)
  └─ 无矛盾 ✓
```

---

## 六点五、Prompt-Only 控制面（非脚本同构）

> 目标：在通用 LLM 对话框中，不运行脚本也能复现 Runner 的关键行为。

### A. 输入与状态源
- 状态真相源固定为 `.context/`：
  - `scene_list`（运行态 JSON）
  - `STATE`（运行态 Markdown）
  - `RUNNER_STATE`（运行态 JSON）
- 文件输入方式：人工粘贴片段（可分批）。

### B. 同构流程（与脚本版对齐）
1. 路由：`references/prompt-only/ROUTER_PROMPT.md`
2. 全文分批注入：`references/prompt-only/CONTEXT_PACKER_PROMPT.md`
3. 角色执行：目录 `references/prompt-only/ROLE_PROMPTS/` 下对应角色文件
4. 门禁执行：目录 `references/prompt-only/GATES_PROMPTS/` 下全部门禁文件
5. 状态更新：输出 `RUNNER_STATE` / `NEXT_PROMPT` / `scene_list` patch

### C. 同构产物
- `ROUTING_TRACE`（运行态 JSON，建议落盘到 .context/ROUTING_TRACE.json）
- `ROUTING_CONTEXT`（运行态 Markdown，建议落盘到 .context/ROUTING_CONTEXT.md）
- `GATE_REPORT`（运行态 JSON，建议落盘到 .context/GATE_REPORT.json）
- `NEXT_PROMPT`（运行态 Markdown，建议落盘到 .context/NEXT_PROMPT.md）

### D. 强约束
- 命中文件默认全文注入，不做前800字截断。
- 不固定前4文件，按相关性自动选集并分批。
- 任一 blocking gate 失败即停机，不推进 `passes`。

---

## 七、未来扩展接口 (Future Extensions)

### 预留 Hook 插槽

### 预留扩展点 (Extension Points)
未来可以增加以下模块来增强系统能力：
*   **商业化模块**：付费点优化指南、追更率提升技巧。
*   **文学深度模块**：主题编织指南、象征手法库。
*   **读者心理模块**：期待感管理、共情触发机制。

---

## 八、总结：有机整合的关键

### ✅ 三大整合原则

1. **分层不分离**  
   - 模块虽然独立，但通过 hooks 在写作流程中自动协同
   - 作家不需要记住所有规则，系统自动提示

2. **场景驱动调用**  
   - 根据场景类型（动作/感情/内心/环境）智能激活相关模块
   - 不是"把所有规则都用上"，而是"用该用的规则"

3. **质量闭环反馈**  
   - 写完后的检测结果会反哺到下一章的写作
   - 形成"写作 → 检测 → 改进 → 再写作"的良性循环

### 📊 整合效果预期

| 维度 | 整合前 | 整合后 |
|-----|-------|-------|
| 语言质量 | 60分（AI味重） | 85分（接近人类作家） |
| 场景画面感 | 50分（平面化） | 80分（立体沉浸） |
| 人物声音 | 65分（有区分但不强） | 85分（千人千面） |
| 情绪节奏 | 75分（已有基础） | 90分（精确控制） |
| 整体可读性 | 70分 | 88分 |

**目标**：让 95% 的读者无法分辨这是 AI 写的，甚至认为这是"有自己风格的新人作家"。
