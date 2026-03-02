# gate_context_pack

检查路由包是否完整可执行。

## 通过条件
1. `ROUTING_TRACE.required_files` 全部已加载或已进入下一批计划。
2. `missing_files` 为空。
3. `ROUTING_CONTEXT` 明确声明全文注入（FULLTEXT_INCLUDED=true）。

## 输出
```json
{
  "gate_name": "gate_context_pack",
  "passed": true,
  "blocking": true,
  "message": "required files loaded",
  "evidence": ["required=12", "missing=0", "deferred=3"]
}
```
