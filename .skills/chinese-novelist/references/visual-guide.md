# 视觉流程图 (Visual Process Guide)

> **维护者**：Chinese Novelist Pro Team
> **适用范围**：流程可视化与培训辅助
> **状态**：Active
> **最后校验**：2026-03-01

> **用途**: 用 Mermaid 图表直观展示系统流程
> **渲染**: 支持 Mermaid 的 Markdown 编辑器（VS Code、GitHub、Obsidian 等）

---

## 1. 新手入门决策树

```mermaid
flowchart TD
    Start([用户进入系统]) --> Q1{之前用过吗？}
    Q1 -->|没有| Newbie["说：'我是新手，带我入门'"]
    Q1 -->|用过| Q2{想怎么开始？}

    Newbie --> Guided[引导模式：5轮访谈]
    Guided --> G1[核心概念] --> G2[流派风格]
    G2 --> G3[主角设定] --> G4[世界观]
    G4 --> G5[确认] --> Files[渐进生成8个文件]

    Q2 -->|快速开始| Quick["说：'快速启动'"]
    Q2 -->|我是老手| Expert["说：'专家模式'"]
    Q2 -->|继续写| Resume["说：'继续写' 或 '写第X章'"]

    Quick --> AllFiles[一次性生成全部文件]
    Expert --> Template[批量生成空模板]
    Resume --> Writing[进入写作模式]

    Files --> Writing
    AllFiles --> Writing
    Template --> Writing
```

---

## 2. Phase 0-5 执行流程图

```mermaid
flowchart TD
    subgraph P0 ["Phase 0: 会话初始化 (仅首次)"]
        P0A[读取 SKILL.md] --> P0B[读取项目文件 00~07]
        P0B --> P0C[查询流派 Hub Hook]
    end

    subgraph P1 ["Phase 1: 上下文加载 (每次 MUST)"]
        P1A[读取 STATE.md] --> P1B[读取 VOLUME_XX.md]
        P1B --> P1C[读取分章细纲]
        P1C --> P1D[读取伏笔/时间线/细节表]
        P1D --> P1E[生成写前摘要]
    end

    subgraph P2 ["Phase 2: 三层路由"]
        P2A{场景类型?} --> P2B[加载场景 Hook]
        P2A --> P2C[加载流派 Hook]
        P2A --> P2D{有金手指?}
        P2D -->|是| P2E[加载 Engine 模块]
        P2D -->|否| P2F[跳过 Engine]
        P2B --> P2G[激活语言规范]
        P2C --> P2G
        P2E --> P2G
        P2F --> P2G
    end

    subgraph P3 ["Phase 3: 写作执行"]
        P3A[选择章节骨架] --> P3B[开篇钩子 5%]
        P3B --> P3C[铺垫阻力 30%]
        P3C --> P3D[高潮转折 50%]
        P3D --> P3E[结尾钩子 15%]
    end

    subgraph P4 ["Phase 4: 三级质检"]
        P4A["L1 基础扫描 (MUST)"] --> P4B{通过?}
        P4B -->|否| P4FIX[修改后重检] --> P4A
        P4B -->|是| P4C{"执行 L2?"}
        P4C -->|"应当 (SHOULD)"| P4D[80分评分制]
        P4C -->|跳过| P4E["L3 可以 (MAY)"]
        P4D --> P4E
    end

    subgraph P5 ["Phase 5: 状态更新 (MUST)"]
        P5A[更新项目状态] --> P5B[更新卷状态]
        P5B --> P5C[更新伏笔/时间线/细节表]
        P5C --> P5D[追加进度日志]
    end

    P0 --> P1 --> P2 --> P3 --> P4 --> P5
```

---

## 3. 场景路由决策树

```mermaid
flowchart TD
    Scene([分析本章场景]) --> ST{场景类型?}

    ST -->|战斗/打斗| A1["action-scene-guide.md"]
    ST -->|感情/暧昧| A2["romance-scene-guide.md + emotional-beats.md"]
    ST -->|打脸/逆袭| A3["face-slapping.md + audience-reaction.md"]
    ST -->|家族斗争| A4["family-conflict.md"]
    ST -->|突破晋级| A5["power-system.md"]
    ST -->|关键对话| A6["dialogue-subtext.md + dialogue-writing.md"]
    ST -->|生死危机| A7["tension-building.md + suspense-building.md"]
    ST -->|日常生活| A8["chapter-micro-structure.md"]
    ST -->|比赛竞技| A9["match-commentary.md + match-tension.md"]
    ST -->|群像团战| A10["ensemble-cast-guide.md + team-dynamics.md"]
    ST -->|副本探险| A11["dungeon-design.md + tension-building.md"]
    ST -->|商战权谋| A12["business-palace-guide.md + political-intrigue.md"]
    ST -->|未识别| DEFAULT["默认：language-craft.md + chapter-micro-structure.md + ai-guardrails.md"]

    A1 & A2 & A3 & A4 & A5 & A6 & A7 & A8 & A9 & A10 & A11 & A12 & DEFAULT --> LANG[激活语言规范]
    LANG --> GENRE[加载流派范文]
    GENRE --> ENGINE{有 Engine?}
    ENGINE -->|是| ENG[加载 Engine 模块]
    ENGINE -->|否| WRITE[开始写作]
    ENG --> WRITE
```

---

## 4. 加载模式选择

```mermaid
flowchart LR
    User([用户]) --> Mode{选择模式}

    Mode -->|新手/快速| Core20["核心20模式<br/>~20 文件"]
    Mode -->|日常写作| Standard["标准模式<br/>~60 文件"]
    Mode -->|专业创作| Full["完整模式<br/>108 文件"]

    Core20 --> T1[Tier 1: 系统核心 x4]
    Core20 --> T2[Tier 2: 流派范文 x1]
    Core20 --> T3[Tier 3: 场景指南 x1~2]
    Core20 --> T4[Tier 4: 项目文件 x8]
    Core20 --> T5[Tier 5: 质检工具 x3]
    Core20 --> T6[Tier 6: 结构辅助 x1]

    Standard --> Core20
    Standard --> HubHooks[流派 Hub Hook 组]
    Standard --> CraftHooks[常用技法 Hook]

    Full --> Standard
    Full --> AllHooks[全部 92 个 Hook]
    Full --> Theory[理论文件]
    Full --> AdvancedQA[高级分析工具]
```
