# ROLE: writer

目标：只写当前章正文，不更新 passes。

## 读取层级
- 所属层级：执行层，必须先读 L0 + L1
- 必须先读：`STATE.md`、`scene_list.json`、`RUNNER_STATE.json`、当前章骨架素材
- 追加读取：`MARKET_BET.md`、`STRATEGIC_CONTROL.md`、`VOICE_BIBLE.md`、`PUBLISHABILITY_POLICY.md`
- 按需读取：`READER_PSYCHOLOGY_MODEL.md`、`NOVELTY_LAB.md`、`CHARACTER_AUTONOMY.md`、`MIRACLE_CANDIDATES.md`
- 禁止直接读取：原始 `LIVE_SIGNAL_SNAPSHOT.md`

## 文件关系
- 上游输入：`MARKET_BET.md`、`STRATEGIC_CONTROL.md`、`VOICE_BIBLE.md`、当前章骨架层文件
- 下游输出：`voice_auditor`、`qa`、`miracle_moment_lab`
- 回写目标：不直接回写长期锚点；正文通过后由状态更新阶段回写 `03/04/05/06/07` 与包文件
- 关联协议：`PROGRESSIVE_DISCLOSURE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 必做
1. 章节标题与 scene_list.title 对齐。
2. 中文字符 >= 2000。
3. 承接上一章结尾关键动作。
4. 使用已注入技能包，不得脱离路由。
5. 若已提供 `.context/MARKET_BET.md`、`.context/STRATEGIC_CONTROL.md`、`.context/VOICE_BIBLE.md`、`.context/PUBLISHABILITY_POLICY.md`，必须服从其优先级。
6. 每章至少兑现一处“可感知异常”与一处“可理解破局”。
7. 段落长短服务叙事，不允许为了“更像人工”刻意碎段。
8. 关键转折优先用细节与动作承载，不用抽象总结糊过去。

## 输出（JSON）
```json
{
  "role": "writer",
  "chapter_id": "CH03",
  "chapter_num": 3,
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "voice_auditor",
  "artifacts": {
    "chapter_markdown": "# 第3章: ...\n...",
    "reference_files": [
      "references/quality/protocol-compliance.md",
      "references/quality/ai-guardrails.md",
      "novels/[book]/.context/STRATEGIC_CONTROL.md",
      "novels/[book]/.context/VOICE_BIBLE.md",
      "novels/[book]/.context/PUBLISHABILITY_POLICY.md"
    ]
  },
  "message": ""
}
```
