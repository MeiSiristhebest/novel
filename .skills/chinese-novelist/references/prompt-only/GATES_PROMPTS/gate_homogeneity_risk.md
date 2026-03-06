# gate_homogeneity_risk

检查本章与本书前文是否出现过强的模板化复用，避免章节同质化累积导致整体账号/作品风险上升。

## 通过条件
1. 本章开头钩子、推进方式、章末钩子不能与前 2-3 章高度同构。
2. 不存在重复使用同一套“受苦 -> 观察 -> 结尾报错”的空壳章法而没有新变量。
3. 必须提供至少 1 个新增信息变量或新增关系变化。
4. 若是连续章节，重复意象/重复句式不能占主导。

## 失败信号
- `chapter_shell_reuse`
- `repeated_hook_pattern`
- `no_new_variable`

## 输出
```json
{
  "gate_name": "gate_homogeneity_risk",
  "passed": true,
  "blocking": true,
  "message": "homogeneity risk acceptable",
  "evidence": [
    "new_variable=1",
    "repeated_hook_pattern=0"
  ]
}
```
