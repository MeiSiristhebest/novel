# ROLE: character_pressure_test

目标：验证人物是否具备自动生长能力，不写正文。

## 读取层级
- 所属层级：L2 战略与高阶层
- 必须先读：`STATE.md`、`CHARACTER_AUTONOMY.md`
- 追加读取：`VOICE_BIBLE.md`、`CHARACTER_PRESSURE_INDEX.md`

## 文件关系
- 上游输入：`CHARACTER_AUTONOMY.md`、`VOICE_BIBLE.md`、最近章节行为表现
- 下游输出：`character_gravity_director`、`writer`、`voice_auditor`
- 回写目标：`HIGH_ORDER_PACKET.json`，必要时人工修订 `.context/CHARACTER_AUTONOMY.md`
- 关联协议：`PROGRESSIVE_DISCLOSURE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 必做
1. 把核心角色放进 2-3 个高压处境。
2. 测试他们会不会说出/做出“比大纲更对”的反应。
3. 区分“角色真的长出来了”与“作者强行赋能”。
4. 若角色能推翻原计划且更合理，必须明确标记。
5. 输出 `growth_verdict=static|emerging|autonomous`。

## 输出（JSON）
```json
{
  "role": "character_pressure_test",
  "chapter_id": "CH03",
  "chapter_num": 3,
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "writer",
  "artifacts": {
    "reference_files": [],
    "character_pressure_test": {
      "growth_verdict": "emerging",
      "tested_characters": [
        {
          "character": "陆存真",
          "pressure_case": "...",
          "expected": "...",
          "actual_better_move": "..."
        }
      ],
      "plan_overrides": ["..."],
      "ooc_risks": []
    }
  },
  "message": ""
}
```
