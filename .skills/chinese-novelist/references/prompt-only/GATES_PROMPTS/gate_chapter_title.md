# gate_chapter_title

检查章节标题与 `scene_list.title` 对齐。

## 通过条件
1. 第一行是 Markdown 标题。
2. 标题核心语义与 `scene_list.title` 一致。

## 输出
```json
{
  "gate_name": "gate_chapter_title",
  "passed": true,
  "blocking": true,
  "message": "title aligned",
  "evidence": ["expected=第3章:史莱姆的正确打法", "actual=# 第三章：史莱姆的正确打法"]
}
```
