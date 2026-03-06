# gate_quality_bar

检查章节是否达到“顶级作者化”的最低放行线。

## 所属层级
- 执行后质检层

## 文件关系
- 上游输入：`qa`、`TOP_AUTHOR_SCORECARD.md`
- 下游输出：`chief_editor`、放行决策
- 失败去向：`retry_same_role` 或 `route_to_strategy`
- 关联协议：`GATE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 证据来源
- `craft_score.total`
- `craft_score.tier`
- `aesthetic_judgment.winner`

## 通过条件
1. `craft_score.total >= 40`
2. `craft_score.tier` 必须为 `A` 或 `S`
3. 必须提供 `aesthetic_judgment`
4. `aesthetic_judgment.winner` 必须为 `A`（当前稿胜出）

## 失败处理
- 若分数不够：打回 `writer`
- 若卖点失焦但文本合格：转交 `chief_editor` 或 `story_director`

## 输出
```json
{
  "gate_name": "gate_quality_bar",
  "passed": true,
  "blocking": true,
  "message": "quality bar passed",
  "evidence": [
    "total=42",
    "tier=A",
    "winner=A"
  ]
}
```
