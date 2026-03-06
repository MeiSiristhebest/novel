# gate_high_order_packet

检查高阶创作能力是否在需要时被调用。

## 所属层级
- 高阶创作层

## 文件关系
- 上游输入：`HIGH_ORDER_PACKET.json`、高阶角色结果、信号使用结果
- 下游输出：`gate_aesthetic_delta`、`gate_memorable_line_or_action`
- 失败去向：`route_to_strategy` 或 `retry_same_role`
- 关联协议：`GATE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 证据来源
- `high_order_required`
- `high_order_triggers`
- `novelty_lab`
- `reader_psychology_model`
- `reader_behavior_model`
- `ruthless_cut_review`
- `character_pressure_test`
- `character_gravity`
- `live_signal_decision`

## 通过条件
1. 若 `high_order_required=false`：直接通过。
2. 若命中“新卷/新 Arc/新鲜感乏力”：必须存在 `novelty_lab`。
3. 若命中“黄金三章/卷中点/反馈高压”：必须存在 `reader_psychology_model`。
4. 若命中“读者状态漂移/掉读风险”：必须存在 `reader_behavior_model`。
5. 若命中“剧情拖肥散/主编降级/无新增变量”：必须存在 `ruthless_cut_review`。
6. 若命中“人物关系关键转折/核心人物初期定型”：必须存在 `character_pressure_test`。
7. 若命中“人物压场不足”：必须存在 `character_gravity`。
8. 若提供 `LIVE_SIGNAL_SNAPSHOT.md`，高阶角色必须写明 `live_signal_usage=used|ignored`，不得默默污染正文。

## 失败处理
- 缺关键高阶角色：转回对应高阶角色
- 高阶角色已执行但无结论：不放行

## 输出
```json
{
  "gate_name": "gate_high_order_packet",
  "passed": true,
  "blocking": true,
  "message": "high-order packet passed",
  "evidence": [
    "novelty_lab=present",
    "reader_psychology_model=present",
    "live_signal_usage=used"
  ]
}
```
