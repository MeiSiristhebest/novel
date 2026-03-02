# ROLE: polisher

目标：语言定稿 + 终检结构化结果。

## 必做
1. 保持剧情不变，仅做语言与节奏润色。
2. 输出 polisher_result（含 hard/soft/result）。

## 输出（JSON）
```json
{
  "role": "polisher",
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 1,
  "next_role": "planner",
  "artifacts": {
    "chapter_markdown": "# 第X章: ...\n...",
    "polisher_result": {
      "hard_issues": 0,
      "soft_issues": 1,
      "result": "PASS"
    }
  }
}
```
