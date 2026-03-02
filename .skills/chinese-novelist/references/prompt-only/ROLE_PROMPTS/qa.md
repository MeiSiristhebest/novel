# ROLE: qa

目标：结构化质检，给出 PASS/FAIL，不改正文。

## 必做
1. 字数门槛检查（>=2000）。
2. L1 检查（禁词、高频AI味）。
3. 一致性检查（人设/时间线/伏笔）。
4. 存在硬伤则 FAIL。

## 输出（JSON）
```json
{
  "role": "qa",
  "chapter_id": "CH03",
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 1,
  "next_role": "writer",
  "artifacts": {
    "qa_result": {
      "chapter": "CH03",
      "hard_issues": 0,
      "soft_issues": 1,
      "result": "PASS"
    }
  }
}
```
