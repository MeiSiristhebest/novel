# NEXT_PROMPT（手工续跑模板）

## 当前轮次
- pipeline: {{pipeline}}
- next_role: {{next_role}}
- chapter_id: {{chapter_id}}

## 执行要求
1. 严格遵守 `references/prompt-only/MASTER_ORCHESTRATOR.md`
2. 先确认 `ROUTING_TRACE` 与 `ROUTING_CONTEXT`
3. 仅输出结构化结果（见 `OUTPUT_CONTRACTS.md`）

## 当前输入
- scene_list: 已提供
- state: 已提供
- runner_state: 已提供
- chapter materials: 已提供

## 平台策略卡（若目标平台已明确则必须）
- platform: {{platform_or_null}}
- PLATFORM_STRATEGY_CARD: 已提供 / N/A
