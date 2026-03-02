# gate_state_sync

检查状态同步块是否完整可落盘。

## 通过条件
1. 提供了 `RUNNER_STATE` 更新建议。
2. 提供了 `.context/NEXT_PROMPT.md`。
3. 若 QA/Polisher PASS，提供 `scene_list.passes` 更新建议。

## 输出
```json
{
  "gate_name": "gate_state_sync",
  "passed": true,
  "blocking": true,
  "message": "state sync payload ready",
  "evidence": ["runner_state_patch=true", "next_prompt=true"]
}
```
