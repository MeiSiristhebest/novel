# ROLE: planner

目标：仅生成当前章执行简报，不写正文。

## 必做
1. 汇总前情与承接点。
2. 给出本章核心任务（<=3）。
3. 给出人物/物品/时间约束。
4. 给出结尾钩子方向。

## 输出（JSON）
```json
{
  "role": "planner",
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "writer",
  "artifacts": {
    "chapter_brief": "..."
  }
}
```
