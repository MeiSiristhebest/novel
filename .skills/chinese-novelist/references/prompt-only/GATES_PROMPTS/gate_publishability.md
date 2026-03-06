# gate_publishability

做综合发布性判断。目标不是绕过检测，而是降低误判风险、提高原创性与可发布性。

## 所属层级
- 发布性与放行层

## 文件关系
- 上游输入：`qa`、`publishability_report`、发布性相关子 gate
- 下游输出：最终放行决策
- 失败去向：`retry_same_role`
- 关联协议：`GATE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 证据来源
- `publishability_report.layout_naturalness`
- `publishability_report.detail_specificity`
- `publishability_report.homogeneity_risk`
- `publishability_report.rewrite_trace_risk`
- `publishability_report.publishability`

## 通过条件
1. `gate_layout_compliance` 已通过。
2. `gate_detail_specificity` 已通过。
3. `gate_voice_uniqueness` 已通过。
4. `gate_homogeneity_risk` 已通过。
5. `qa` 未报告严重 AI 味、严重一致性硬伤或严重卖点失焦。
6. 不存在明显“整合改写痕迹”或“提示词加工痕迹”主导正文。
7. 综合判断应更接近“人工自然写作”而非“机械平滑生成”。

## 结果档位
- `publish_ready`：可发布
- `revise_for_publishability`：需修后再发
- `hold`：不建议发布

## 失败处理
- 只要 `publishability != publish_ready`，默认不放行
- 不给任何规避检测建议，只给质量修订方向

## 输出
```json
{
  "gate_name": "gate_publishability",
  "passed": true,
  "blocking": true,
  "message": "publish_ready",
  "evidence": [
    "layout=pass",
    "details=pass",
    "voice=pass",
    "homogeneity=low"
  ]
}
```
