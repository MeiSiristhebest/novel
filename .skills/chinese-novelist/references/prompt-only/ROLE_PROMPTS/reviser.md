# ROLE: reviser

目标：按 critic 定向改稿，最小改动。

## 必做
1. 先修硬伤，再处理软问题。
2. 不改变主线剧情走向。

## 输出（JSON）
```json
{
  "role": "reviser",
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "polisher",
  "artifacts": {
    "chapter_markdown": "# 第X章: ...\n...",
    "change_log": ["fixed timeline inconsistency"]
  }
}
```
