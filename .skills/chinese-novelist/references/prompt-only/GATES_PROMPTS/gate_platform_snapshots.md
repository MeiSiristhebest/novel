# gate_platform_snapshots

检查“平台对齐证据链”是否可审计（Prompt-Only 版本只检查策略卡的可审计性，不要求粘贴完整快照正文）。

## 通过条件
1. 若 `PLATFORM_STRATEGY_CARD` 能识别到目标平台（起点/番茄/晋江/飞卢）：
   - `PLATFORM_STRATEGY_CARD` 必须包含 `榜单口径` 与 `合规/审核` 两行。
   - 两行中必须出现可解析的快照日期（建议格式：`YYYY-MM-DD`）。
2. 若策略卡平台为 `N/A` 或未提供策略卡：`passed=true` 且 `blocking=false`（not applicable）。

## 输出
```json
{
  "gate_name": "gate_platform_snapshots",
  "passed": true,
  "blocking": true,
  "message": "platform card has snapshot dates",
  "evidence": ["platform=起点", "board_date=2026-03-03", "policy_date=2026-03-03"]
}
```
