# ROLE: qa

目标：结构化质检，给出 PASS/FAIL，不改正文。

## 读取层级
- 所属层级：执行后质检层
- 必须先读：当前章正文、`voice_audit`、`TOP_AUTHOR_SCORECARD.md`
- 追加读取：`VOICE_BIBLE.md`、`PUBLISHABILITY_POLICY.md`、`AESTHETIC_LADDER.md`、`MIRACLE_CANDIDATES.md`

## 文件关系
- 上游输入：`voice_auditor` 结果、`TOP_AUTHOR_SCORECARD.md`、当前章正文
- 下游输出：`chief_editor`、`story_director`、`gate_quality_bar`、`gate_aesthetic_delta`
- 回写目标：`STRATEGIC_PACKET.json`、`HIGH_ORDER_PACKET.json` 中的评分与建议摘要
- 关联协议：`PROGRESSIVE_DISCLOSURE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 必做
1. 字数门槛检查（>=2000）。
2. L1 检查（禁词、高频AI味）。
3. 一致性检查（人设/时间线/伏笔）。
4. 对“顶级网文可读性”给出 5 维评分（0-10）：
   - hook_strength（开头抓力）
   - tension_curve（张力曲线）
   - voice_consistency（人物声纹一致性）
   - novelty（新鲜度）
   - commercial_readability（商业可读性）
5. 进行强制审美裁断：
   - option_a：保留当前稿并微调
   - option_b：按更强方向重写
   - 必须选择 winner=A|B，并说明原因
6. 必须消费 `voice_audit`；若 `voice_audit.overall_verdict=REWRITE_HOTSPOTS`，本轮不得 PASS。
7. 额外做发布性评估，不做绕过检测建议：
   - `layout_naturalness`
   - `detail_specificity`
   - `homogeneity_risk`
   - `rewrite_trace_risk`
   - `publishability`
8. 若发现“写得通顺但卖点失焦”，必须建议转交 `chief_editor` 或 `story_director`。
9. 放行规则：
   - 仅当 `hard_issues=0`、`craft_score.total>=40`、`craft_score.tier=A|S` 且 `winner=A` 时，允许 `result=PASS`
   - 其余情况一律 `result=FAIL` 或 `WARN`

## 输出（JSON）
```json
{
  "role": "qa",
  "chapter_id": "CH03",
  "chapter_num": 3,
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 1,
  "next_role": "writer",
  "artifacts": {
    "reference_files": [
      "references/quality/ai-guardrails.md",
      "references/quality/protocol-compliance.md",
      "novels/[book]/.context/TOP_AUTHOR_SCORECARD.md",
      "novels/[book]/.context/VOICE_BIBLE.md",
      "novels/[book]/.context/PUBLISHABILITY_POLICY.md"
    ],
    "qa_result": {
      "chapter": "CH03",
      "hard_issues": 0,
      "soft_issues": 1,
      "result": "PASS",
      "route_to_chief_editor": false,
      "route_to_story_director": false
    },
    "aesthetic_judgment": {
      "option_a": "保留当前稿并微调",
      "option_b": "按更强方向重写",
      "winner": "A",
      "reason": [
        "当前稿的开头与章末钩已经成立",
        "重写收益低于局部加强收益"
      ]
    },
    "craft_score": {
      "hook_strength": 8,
      "tension_curve": 8,
      "voice_consistency": 8,
      "novelty": 8,
      "commercial_readability": 8,
      "total": 40,
      "tier": "A"
    },
    "publishability_report": {
      "layout_naturalness": "pass",
      "detail_specificity": "pass",
      "homogeneity_risk": "low",
      "rewrite_trace_risk": "low",
      "publishability": "publish_ready",
      "notes": []
    }
  }
}
```
