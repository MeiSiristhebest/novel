# gate_state_sync

检查状态同步块是否完整可落盘。

## 所属层级
- 状态同步层

## 文件关系
- 上游输入：`RUNNER_STATE` 更新建议、`NEXT_PROMPT.md`、`scene_list` 更新建议
- 下游输出：下一轮运行态
- 失败去向：`hold_release`
- 关联协议：`GATE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 证据来源
- `RUNNER_STATE` patch
- `NEXT_PROMPT.chapter_id`
- `scene_list` 更新建议
- `NEXT_PROMPT.md` 内容体积

## 通过条件
1. 提供了 `RUNNER_STATE` 更新建议。
2. 提供了 `.context/NEXT_PROMPT.md`。
3. 若 QA/Polisher PASS，提供 `scene_list.passes` 更新建议。
4. `NEXT_PROMPT.chapter_id` 必须等于当前 `scene_list` 第一条 `passes=false` 的章节。
5. `NEXT_PROMPT.md` 不能包含全文注入内容（禁止出现“Batch Fulltext Context”等大体积残留）。

## 失败处理
- 任一状态块缺失：不允许结束本轮
- 章号不匹配：禁止推进到下一章

## 输出
```json
{
  "gate_name": "gate_state_sync",
  "passed": true,
  "blocking": true,
  "message": "state sync payload ready",
  "evidence": [
    "runner_state_patch=true",
    "next_prompt=true",
    "chapter_match=true",
    "stale_context=false"
  ]
}
```
