# 核心 20 文件速通清单 (Core 20 Essential Files)

> **维护者**：Chinese Novelist Pro Team
> **适用范围**：快速加载与最小可用上下文
> **状态**：Active
> **最后校验**：2026-03-01

> **用途**: 为 AI 提供最小化但足够的上下文，支持快速启动写作
> **适用场景**: 新手入门、快速验证、上下文窗口有限时
> **完整模式**: 如需完整 108 文件，参见 SKILL.md 的 Hook 引用表

---

## 分层加载架构

### Tier 1: 系统核心 (4个 — 必须 MUST)

每次会话都**必须 (MUST)** 加载：

| # | 文件 | 用途 |
|:--|:-----|:-----|
| 1 | `SKILL.md` | 系统身份 + 触发词映射 + 协议索引 |
| 2 | `references/quality/protocol-compliance.md` | Phase 0-5 全流程主控协议 |
| 3 | `references/guides/language-craft.md` | 语言锤炼核心规范 |
| 4 | `references/quality/ai-guardrails.md` | AI 防护栏 + 禁用词清单 |

### Tier 2: 流派范文 (1个 — 按项目加载)

根据用户选择的流派加载 **1 个** 范文：

| # | 文件 | 用途 |
|:--|:-----|:-----|
| 5 | `references/style-exemplars/xuanhuan.md` | 流派风格模板 + Top作品解析 |

> 35 种流派列表见 SKILL.md 快速索引

### Tier 3: 场景指南 (按需 — 应当 SHOULD)

根据当前章节场景类型加载（通常 1-2 个）：

| # | 文件 | 触发场景 |
|:--|:-----|:---------|
| 6 | `references/scenes/action-scene-guide.md` | 动作戏/打斗 |
| 7 | `references/scenes/romance-scene-guide.md` | 感情戏/暧昧 |
| 8 | `references/scenes/dialogue-writing.md` | 关键对话 |

### Tier 4: 项目文件 (8个 — 项目存在时自动加载)

| # | 文件 | 用途 |
|:--|:-----|:-----|
| 9 | `novels/[书名]/00-全局设定/00-策划书.md` | 核心设定 |
| 10 | `novels/[书名]/00-全局设定/01-世界观圣经.md` | 世界观规则 |
| 11 | `novels/[书名]/00-全局设定/02-人设档案.md` | 角色数据 |
| 12 | `novels/[书名]/03-分章细纲.md` | 章节大纲 |
| 13 | `novels/[书名]/00-全局设定/04-伏笔追踪表.md` | 伏笔状态 |
| 14 | `novels/[书名]/00-全局设定/05-时间线.md` | 时间节点 |
| 15 | `novels/[书名]/00-全局设定/06-细节追踪表.md` | 人物/物品状态 |
| 16 | `novels/[书名]/00-全局设定/07-项目状态.md` | 进度跟踪 |

### Tier 5: 质检工具 (3个 — 质检时加载)

| # | 文件 | 用途 |
|:--|:-----|:-----|
| 17 | `references/quality/quality-checklist.md` | 80分评分制质检清单 |
| 18 | `references/prompts/scene-critic.md` | 场景微观质检 |
| 19 | `references/prompts/chief-editor.md` | 主编宏观审稿 |

### Tier 6: 结构辅助 (1个 — 应当 SHOULD)

| # | 文件 | 用途 |
|:--|:-----|:-----|
| 20 | `references/guides/chapter-micro-structure.md` | 章节骨架模板 |

> 引导模式/开篇工作坊时，**应当 (SHOULD)** 额外加载：`references/guides/webnovel-creator-workflow-cn.md`（网文创作工作流与开篇投放策略）。
> 平台已明确（起点/番茄/晋江/飞卢）时，**应当 (SHOULD)** 额外加载：`references/guides/platform-playbook-cn.md`（平台榜单口径与写作策略对齐）。
> 若用户要求 **最新榜单/趋势/合规口径**：必须先按该文件第 0 节完成《实时榜单快照》与《平台政策快照》，否则不得输出“最新结论”。

---

## 加载模式对照

| 模式 | 文件数 | 适用场景 | 加载内容 |
|:-----|:-------|:---------|:---------|
| **核心20模式** | ~20 | 新手、快速验证、上下文有限 | Tier 1-6 |
| **标准模式** | ~60 | 日常写作 | 核心20 + 流派Hub Hook + 常用技法 |
| **完整模式** | 108 | 专业创作、复杂场景 | 全部引用文件 |

---

## 如何从核心20升级到标准/完整模式

当 AI 在核心20模式下遇到以下情况时，**应当 (SHOULD)** 自动扩展加载：

1. **场景需要专项技法** → 加载 `references/hooks/` 下对应 Hook
2. **流派有特殊需求** → 加载 `references/hooks/README.md` 中的流派推荐清单
3. **用户要求深度质检** → 加载 L3 高级分析工具（style-drift-detector, reader-simulator 等）
4. **长篇规划** → 加载 long-form-structure.md, arc-planning.md 等


