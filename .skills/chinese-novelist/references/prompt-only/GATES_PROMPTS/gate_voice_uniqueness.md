# gate_voice_uniqueness

检查主要角色是否存在可辨识声纹，避免“所有人都像同一个模型在说话”。

## 通过条件
1. 至少主角与第二关键人物在句式、词汇、价值取向上可区分。
2. `voice_audit` 必须存在。
3. `voice_audit.protagonist_voice.status` 不能为 `flat` 或 `mixed`。
4. `voice_audit.major_character_voice` 中不得出现 2 个及以上 `mixed` / `generic`。
5. 若出现“谁都能说”的通用句，必须只占少数且不出现在关键对话节点。

## 失败信号
- `generic_dialogue`
- `voice_collision`
- `ooc_hotspot`

## 输出
```json
{
  "gate_name": "gate_voice_uniqueness",
  "passed": true,
  "blocking": true,
  "message": "voice uniqueness passed",
  "evidence": [
    "protagonist=stable",
    "major_mixed=0"
  ]
}
```
