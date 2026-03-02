# OUTPUT_CONTRACTS（Prompt-Only 统一输出契约）

## 1) 角色输出契约
```json
{
  "role": "writer|qa|initializer|planner|critic|reviser|polisher",
  "chapter_id": "CH03",
  "chapter_num": 3,
  "result": "PASS|FAIL|INFO",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "qa",
  "artifacts": {
    "chapter_markdown": "",
    "qa_result": {},
    "critic_notes": "",
    "polisher_result": {}
  },
  "message": ""
}
```

## 2) Gate 报告契约
```json
{
  "gate_name": "gate_context_pack",
  "passed": true,
  "blocking": true,
  "message": "loaded 12 files, deferred 3",
  "evidence": ["..."]
}
```

## 3) 汇总门禁契约（GATE_REPORT.json）
```json
{
  "chapter_id": "CH03",
  "all_passed": false,
  "blocking_failure": "gate_chapter_wordcount",
  "gates": [
    {
      "gate_name": "gate_chapter_wordcount",
      "passed": false,
      "blocking": true,
      "message": "chapter chars 1780 < 2000",
      "evidence": ["count=1780"]
    }
  ]
}
```

## 4) RUNNER_STATE 更新契约
```json
{
  "pipeline": "writer-qa",
  "next_role": "writer",
  "iteration": 12,
  "current_chapter": 3,
  "last_gate_results": {},
  "last_error": null,
  "last_role": "qa"
}
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
  "required_files": [],
  "selected_files": [],
  "deferred_files": [],
  "missing_files": [],
  "batches": [
    {"batch": 1, "files": []}
  ],
  "selection_reason": {}
}
```
