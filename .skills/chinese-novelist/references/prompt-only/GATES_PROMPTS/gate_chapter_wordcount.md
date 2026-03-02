# gate_chapter_wordcount

检查章节中文字符数。

## 通过条件
- 当前章节中文字符 >= 2000。

## 输出
```json
{
  "gate_name": "gate_chapter_wordcount",
  "passed": false,
  "blocking": true,
  "message": "chapter chars 1880 < 2000",
  "evidence": ["count=1880", "threshold=2000"]
}
```
