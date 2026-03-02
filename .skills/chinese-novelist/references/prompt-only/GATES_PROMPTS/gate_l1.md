# gate_l1

检查 L1 违规（禁词、高频AI痕迹）。

## 通过条件
- 无 blocking 级别违规命中。

## 输出
```json
{
  "gate_name": "gate_l1",
  "passed": true,
  "blocking": true,
  "message": "L1 gate pass",
  "evidence": ["banned_hits=0", "high_freq_over=0"]
}
```
