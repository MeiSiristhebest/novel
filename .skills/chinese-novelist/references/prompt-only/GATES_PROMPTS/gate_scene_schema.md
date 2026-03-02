# gate_scene_schema

检查 `scene_list.json` 结构合法性。

## 通过条件
1. JSON 可解析。
2. 必填字段完整。
3. `chapter_mode/scene_types/passes` 符合约束。

## 输出
```json
{
  "gate_name": "gate_scene_schema",
  "passed": true,
  "blocking": true,
  "message": "scene_list schema ok",
  "evidence": ["items=20", "required fields present"]
}
```
