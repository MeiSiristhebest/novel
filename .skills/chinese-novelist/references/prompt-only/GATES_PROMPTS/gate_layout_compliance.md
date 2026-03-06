# gate_layout_compliance

检查文本排版是否自然，避免出现异常短排版、刻意断句、伪口语化碎片排版。

## 通过条件
1. 不存在连续 3 段以上的单句短段，且这些短段并非出于明确叙事目的。
2. 不存在大量 2-8 字的机械切段。
3. 不存在为了“像人工”而故意插入的错别字、异常空行、无意义停顿。
4. 段落长短有节奏变化，但总体服务场景推进，不服务规避嫌疑。

## 失败信号
- `too_many_micro_paragraphs`
- `artificial_line_breaks`
- `layout_evasion_risk`

## 输出
```json
{
  "gate_name": "gate_layout_compliance",
  "passed": true,
  "blocking": true,
  "message": "layout looks natural",
  "evidence": [
    "micro_paragraphs=1",
    "artificial_breaks=0"
  ]
}
```
