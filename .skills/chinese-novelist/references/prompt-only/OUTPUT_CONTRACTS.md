# OUTPUT_CONTRACTS（Prompt-Only 统一输出契约）

## 0) 阅读确认输出块（强制）

当输出包含“策划/正文/质检报告/战略报告”等创作工件时，必须在末尾附加如下区块：

```markdown
---
📚 **本次参考文件**：
- `path/to/file.md`
- `path/to/another.md`
---
```

## 1) 角色输出契约
```json
{
  "role": "writer|qa|initializer|planner|critic|reviser|polisher|market_bet|chief_editor|story_director|feedback_triage|voice_auditor|novelty_lab|reader_psychology_director|ruthless_cut_review|character_pressure_test|signal_curator|dangerous_bet_lab|aesthetic_upgrade_director|reader_behavior_modeler|character_gravity_director|miracle_moment_lab",
  "chapter_id": "CH03",
  "chapter_num": 3,
  "result": "PASS|FAIL|INFO|WARN",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "qa",
  "artifacts": {
    "chapter_markdown": "",
    "reference_files": [],
    "qa_result": {},
    "critic_notes": "",
    "polisher_result": {},
    "aesthetic_judgment": {"option_a":"","option_b":"","winner":"A|B","reason":[]},
    "craft_score": {"hook_strength":0,"tension_curve":0,"voice_consistency":0,"novelty":0,"commercial_readability":0,"total":0,"tier":"S|A|B|C"},
    "market_bet": {},
    "chief_editor_report": {},
    "story_decisions": {},
    "feedback_triage": {},
    "voice_audit": {},
    "publishability_report": {"layout_naturalness":"pass|warn|fail","detail_specificity":"pass|warn|fail","homogeneity_risk":"low|medium|high","rewrite_trace_risk":"low|medium|high","publishability":"publish_ready|revise_for_publishability|hold","notes":[]},
    "dangerous_bet": {},
    "aesthetic_delta": {"chosen_axis":"","decision":"keep|raise|rebuild","delta_vs_last_3":"","delta_vs_best_chapter":"","new_height_reached":false,"next_raise_actions":[]},
    "novelty_lab": {},
    "reader_psychology_model": {},
    "reader_behavior_model": {},
    "ruthless_cut_review": {},
    "character_pressure_test": {},
    "character_gravity": {},
    "miracle_moment": {},
    "signal_curation": {},
    "live_signal_decision": {"used": false, "reason": ""}
  },
  "message": "",
  "meta": {"generated_at": "YYYY-MM-DD HH:mm:ss"}
}
```

## 2) Gate 报告契约
```json
{"gate_name":"gate_context_pack","passed":true,"blocking":true,"message":"loaded 12 files, deferred 3","evidence":["..."]}
```

## 3) 汇总门禁契约（GATE_REPORT.json）
```json
{"chapter_id":"CH03","all_passed":false,"blocking_failure":"gate_chapter_wordcount","gates":[{"gate_name":"gate_chapter_wordcount","passed":false,"blocking":true,"message":"chapter chars 1780 < 2000","evidence":["count=1780"]}]}
```

## 4) RUNNER_STATE 更新契约
```json
{"pipeline":"writer-qa","next_role":"writer","iteration":12,"current_chapter":3,"last_gate_results":{},"last_error":null,"last_role":"qa"}
```

## 5) 路由追踪契约
```json
{
  "generated_at": "YYYY-MM-DD HH:mm:ss",
  "role": "writer",
  "chapter_num": 3,
  "chapter_id": "CH03",
  "scene_types": ["副本探险"],
  "genre": "system-litrpg",
  "platform": null,
  "strategic_triggers": ["voice_control", "publishability_review"],
  "strategic_required_roles": ["voice_auditor", "chief_editor", "aesthetic_upgrade_director"],
  "high_order_triggers": ["golden_chapter"],
  "high_order_required_roles": ["signal_curator", "novelty_lab", "reader_psychology_director", "reader_behavior_modeler", "miracle_moment_lab"],
  "required_files": [],
  "selected_files": [],
  "deferred_files": [],
  "missing_files": [],
  "reference_files": [],
  "batches": [{"batch": 1, "files": []}],
  "selection_reason": {}
}
```

## 6) 战略包契约（STRATEGIC_PACKET.json）
```json
{"chapter_id":"CH03","chapter_num":3,"strategic_required":true,"strategic_triggers":["golden_chapter","voice_control"],"market_bet":null,"dangerous_bet":null,"aesthetic_delta":null,"chief_editor_report":null,"story_decisions":null,"feedback_triage":null,"voice_audit":null}
```

## 7) 高阶包契约（HIGH_ORDER_PACKET.json）
```json
{"chapter_id":"CH03","chapter_num":3,"high_order_required":true,"high_order_triggers":["golden_chapter","novelty_fatigue"],"signal_curation":null,"novelty_lab":null,"reader_psychology_model":null,"reader_behavior_model":null,"ruthless_cut_review":null,"character_pressure_test":null,"character_gravity":null,"miracle_moment":null,"live_signal_decision":null}
```

## 8) 文件体积约束
- `.context/NEXT_PROMPT.md` 与 `.context/ROUTING_CONTEXT.md` 禁止包含全文注入正文。
- 全文注入内容仅存在于当前会话上下文，不持久化落盘。
- `.context/STRATEGIC_PACKET.json` 与 `.context/HIGH_ORDER_PACKET.json` 只保留结论，不粘贴长篇分析正文。
