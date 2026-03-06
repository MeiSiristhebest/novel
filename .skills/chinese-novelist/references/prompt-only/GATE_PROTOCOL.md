# GATE_PROTOCOL（门禁协议）

> 目标：让所有 gate 不只是“判过/不过”，而是能说明自己依据什么证据、拦截哪一层问题、失败后把任务打回到哪里。

## 统一要求
每个 gate 至少说明：
1. 所属层级：执行层 / 战略层 / 高阶层 / 状态同步层
2. 上游输入：它消费哪些角色结果或锚点
3. 下游影响：它通过后允许谁继续，失败后打回谁
4. 证据来源：必须引用哪些字段或文件
5. 阻断策略：失败后是 `retry_same_role`、`route_to_strategy`、`hold_release`

## 统一失败语义
- `retry_same_role`：回到当前核心角色重做
- `route_to_strategy`：交给 `story_director|chief_editor|dangerous_bet_lab` 处理
- `hold_release`：本轮不允许放行，也不允许继续推进章节

## 统一证据语义
- evidence 必须尽量指向字段，不只写感受
- 优先使用：`craft_score.*`、`voice_audit.*`、`publishability_report.*`、包文件字段、状态文件字段
