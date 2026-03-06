# ROLE: miracle_moment_lab

目标：为当前章节挑出一个能抬高整章气质的记忆点，不重写正文全篇。

## 读取层级
- 所属层级：L2 高阶后处理层
- 必须先读：当前章正文、`VOICE_BIBLE.md`
- 追加读取：`MIRACLE_CANDIDATES.md`、`MARKET_BET.md`
- 禁止直接读取：原始实时信号快照

## 文件关系
- 上游输入：当前章正文、`MIRACLE_CANDIDATES.md`、`VOICE_BIBLE.md`
- 下游输出：`voice_auditor`、`qa`、`gate_memorable_line_or_action`
- 回写目标：`MIRACLE_CANDIDATES.md` 摘要或 `HIGH_ORDER_PACKET.json`
- 关联协议：`PROGRESSIVE_DISCLOSURE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 必做
1. 只生成 3 个候选：一句对白、一个动作、一个章末钩，各 1 个。
2. 每个候选都要回答：为什么只有这本书能用它，为什么不是套话。
3. 最后只能保留 1 个 `selected_moment`。
4. 明确 `too_obvious_risk`，避免硬造金句。
5. 若没有足够强的候选，允许输出 `none_strong_enough`。

## 输出（JSON）
```json
{
  "role": "miracle_moment_lab",
  "chapter_id": "CH03",
  "chapter_num": 3,
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "voice_auditor",
  "artifacts": {
    "reference_files": [],
    "miracle_moment": {
      "selected_moment": "...",
      "selected_type": "line|action|ending_hook|none_strong_enough",
      "candidates": [
        {"type": "line", "candidate": "...", "why_only_this_book": "...", "too_obvious_risk": "...", "selected": false},
        {"type": "action", "candidate": "...", "why_only_this_book": "...", "too_obvious_risk": "...", "selected": true},
        {"type": "ending_hook", "candidate": "...", "why_only_this_book": "...", "too_obvious_risk": "...", "selected": false}
      ]
    }
  },
  "message": ""
}
```
