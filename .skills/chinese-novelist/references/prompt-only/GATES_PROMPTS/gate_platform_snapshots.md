# gate_platform_snapshots

检查“平台对齐证据链”是否可审计。

## 通过条件
1. 若目标平台已明确（来自 `platform` 字段，或项目设定中可识别到起点/番茄/晋江/飞卢）：
   - `.context/PLATFORM_STRATEGY_CARD.md` 必须存在；
   - 策略卡必须包含 `榜单口径` 与 `合规/审核` 两行；
   - 两行中必须出现可解析的快照日期（建议格式：`YYYY-MM-DD`）；
   - `.context/PLATFORM_SNAPSHOT.md` 与 `.context/PLATFORM_POLICY_SNAPSHOT.md` 必须存在且非空。
2. 仅当平台未知（`platform=null` 且项目文件中也未出现平台声明）时，允许 `passed=true && blocking=false`（not applicable）。

## 输出
```json
{
  "gate_name": "gate_platform_snapshots",
  "passed": true,
  "blocking": true,
  "message": "platform evidence chain verified",
  "evidence": [
    "platform=番茄",
    "strategy_card=true",
    "board_date=2026-03-06",
    "policy_date=2026-03-06",
    "snapshot_file=true",
    "policy_snapshot_file=true"
  ]
}
```
