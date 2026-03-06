# gate_strategic_packet

检查本轮是否完成必要的战略层审查。

## 所属层级
- 战略层

## 文件关系
- 上游输入：`STRATEGIC_PACKET.json`、`voice_audit`、`chief_editor_report`、`story_decisions`、`feedback_triage`、`market_bet`
- 下游输出：`gate_high_order_packet`、最终放行链
- 失败去向：`route_to_strategy`
- 关联协议：`GATE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 证据来源
- `strategic_required`
- `voice_audit.overall_verdict`
- `chief_editor_report.rating`
- `chief_editor_report.route_to_story_director`
- `story_decisions.release_decision`

## 通过条件
1. 若 `strategic_required=false`：直接通过。
2. 若 `strategic_required=true`：必须提供 `strategic_packet`。
3. `voice_audit` 每章必须存在，且 `overall_verdict` 不能为 `REWRITE_HOTSPOTS`。
4. 若本章属于黄金三章、卷中点、卷末或用户显式要求“能不能火”：必须存在 `chief_editor_report`，且 `rating` 不能为 `C`。
5. 若 `chief_editor_report.route_to_story_director=true`：必须存在 `story_decisions`，且 `release_decision` 不能为 `hold` 或 `reoutline`。
6. 若本轮注入了反馈材料：必须存在 `feedback_triage`。
7. 若本轮是开书/新卷/新 Arc，或系统判定卖点失焦：必须存在 `market_bet`。

## 失败处理
- 缺 `voice_audit`：直接打回 `writer/voice_auditor`
- 缺主编审稿或战略决策：打回 `chief_editor/story_director`

## 输出
```json
{
  "gate_name": "gate_strategic_packet",
  "passed": true,
  "blocking": true,
  "message": "strategic packet passed",
  "evidence": [
    "voice_audit=PASS",
    "chief_editor=A",
    "story_director=not_required"
  ]
}
```
