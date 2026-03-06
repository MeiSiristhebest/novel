# gate_detail_specificity

检查文本是否具备足够具体的经验颗粒，而不是泛化总结或抽象概括。

## 通过条件
1. 本章至少有 3 处可验证的具体细节：物体、动作、感官、时间、空间、伤势、道具、声音等。
2. 关键转折处优先用场景细节承载，而不是用总结句解释。
3. 不允许整章主要靠“他感到/他意识到/这意味着”推进。
4. 副本、规则、破局必须能落到具体操作，不允许只讲概念。

## 失败信号
- `summary_heavy`
- `insufficient_scene_granularity`
- `abstract_resolution`

## 输出
```json
{
  "gate_name": "gate_detail_specificity",
  "passed": true,
  "blocking": true,
  "message": "detail density passed",
  "evidence": [
    "concrete_details>=5",
    "abstract_resolution=0"
  ]
}
```
