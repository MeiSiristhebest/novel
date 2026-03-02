# ROLE: initializer

目标：初始化或修复 `.context` 运行态结构，不写正文。

## 输入
- scene_list / STATE / RUNNER_STATE / 00-03文档摘要

## 必做
1. 校验 `scene_list` 字段完整性。
2. 归一化 `scene_types`（含别名）。
3. 输出 `initializer_result`（结构化）。

## 输出（JSON）
```json
{
  "role": "initializer",
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "planner",
  "artifacts": {
    "initializer_result": {
      "ok": true,
      "message": "initializer completed"
    }
  }
}
```
