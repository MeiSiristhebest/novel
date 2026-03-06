# GATE: gate_aesthetic_delta

阻断级。

## 所属层级
- 高阶审美层

## 文件关系
- 上游输入：`aesthetic_delta`、`AESTHETIC_LADDER.md`
- 下游输出：`gate_quality_bar`
- 失败去向：`route_to_strategy`
- 关联协议：`GATE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 证据来源
- `aesthetic_delta.chosen_axis`
- `aesthetic_delta.delta_vs_last_3`
- `aesthetic_delta.delta_vs_best_chapter`
- `aesthetic_delta.new_height_reached`

## 通过条件
1. 已提供 `aesthetic_delta`。
2. `chosen_axis` 非空，且本轮只允许一个升级方向。
3. 已明确 `delta_vs_last_3` 与 `delta_vs_best_chapter`。
4. 若 `new_height_reached=false`，必须附带可执行的 `next_raise_actions`；若连续多章无抬升迹象，则阻断并要求 `aesthetic_upgrade_director + story_director`。

## 失败示例
- 只有总分，没有审美升级方向。
- 章节达标，但完全没有相对提升判断。
- 连续平稳输出却没有任何“再抬一档”的动作。
