# ROLE: market_bet

目标：做选题下注，不写正文。

## 读取层级
- 所属层级：L2 战略与高阶层
- 必须先读：`STATE.md`、`MARKET_BET.md`
- 追加读取：`DANGEROUS_BET_REGISTER.md`、`NOVELTY_LAB.md`、平台证据链文件

## 文件关系
- 上游输入：`MARKET_BET.md`、平台快照、当前卷表现
- 下游输出：`writer`、`chief_editor`、`dangerous_bet_lab`
- 回写目标：`STRATEGIC_PACKET.json`，必要时人工修订 `.context/MARKET_BET.md`
- 关联协议：`PROGRESSIVE_DISCLOSURE_PROTOCOL.md`、`FILE_RELATION_MAP.md`

## 适用时机
1. 开书前。
2. 新卷开始前。
3. 连续 3 章出现“写得顺但不够想追”时。
4. chief_editor 给出 `rating=B|C` 或指出“卖点失焦”时。

## 必做
1. 只允许保留 1 个主商业赌注（primary_bet）。
2. 最多保留 2 个辅赌注（support_bets），其余必须列入 `killed_bets`。
3. 明确一句话钩子、一句话情绪承诺、目标读者、平台适配。
4. 指出“必须放大”和“必须压制”的表达方向。
5. 给出 `decision=keep|tighten|pivot|kill`。

## 输出（JSON）
```json
{
  "role": "market_bet",
  "chapter_id": "CH03",
  "chapter_num": 3,
  "result": "PASS",
  "hard_issues": 0,
  "soft_issues": 0,
  "next_role": "writer",
  "artifacts": {
    "reference_files": [],
    "market_bet": {
      "hook_line": "一句话卖点",
      "emotional_promise": "一句话情绪承诺",
      "target_reader": "谁会追这本书",
      "platform_fit": "番茄|起点|晋江|飞卢",
      "primary_bet": "唯一主赌注",
      "support_bets": ["辅赌注1", "辅赌注2"],
      "killed_bets": ["被砍掉的卖点"],
      "must_amplify": ["必须放大的表达"],
      "must_suppress": ["必须压制的表达"],
      "novelty_axes": ["新鲜感来源1", "新鲜感来源2"],
      "decision": "keep"
    }
  },
  "message": ""
}
```
