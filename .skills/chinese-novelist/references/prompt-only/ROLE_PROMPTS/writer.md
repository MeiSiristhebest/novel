# ROLE: writer

目标：只写当前章正文，不更新 passes。

## 必做
1. 章节标题与 scene_list.title 对齐。
2. 中文字符 >= 2000。
3. 承接上一章结尾关键动作。
4. 使用已注入技能包，不得脱离路由。

## 输出（JSON）
```json
{
  "role": "writer",
  "chapter_id": "CH03",
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "qa",
  "artifacts": {
    "chapter_markdown": "# 第3章: ...\n..."
  }
}
```
