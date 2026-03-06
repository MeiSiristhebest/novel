# GATE: gate_memorable_line_or_action

阻断级。

## 所属层级
- 记忆点与气质层

## 文件关系
- 上游输入：`miracle_moment`、当前章正文、`MIRACLE_CANDIDATES.md`
- 下游输出：`gate_publishability`
- 失败去向：`retry_same_role`
- 关联协议：`GATE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 证据来源
- `miracle_moment.selected_type`
- `miracle_moment.selected_moment`
- `miracle_moment.candidates[*].why_only_this_book`

## 通过条件
1. 已提供 `miracle_moment`。
2. `selected_type` 为 `line|action|ending_hook` 之一，或明确说明 `none_strong_enough` 并要求重试一轮。
3. 候选必须回答“为什么只有这本书能用它”。
4. 不能是泛用鸡汤、泛悬疑金句、普通装酷动作。

## 失败示例
- 只有好听句子，没有书内独特性。
- 记忆点与人物声纹冲突。
- 章末钩只是重复“更惨了”。
