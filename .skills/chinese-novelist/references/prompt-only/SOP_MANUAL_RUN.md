# SOP_MANUAL_RUN（手工执行）

## 一、准备
1. 打开 `MASTER_ORCHESTRATOR.md`。
2. 从项目复制以下文件内容到会话：
   - `.context/scene_list.json`
   - `.context/STATE.md`
   - `.context/RUNNER_STATE.json`
   - 当前章节素材（03/04/05/06）

## 二、单轮执行步骤
1. 粘贴运行态上下文。
2. 发送 `references/prompt-only/ROUTER_PROMPT.md`。
3. 发送 `references/prompt-only/CONTEXT_PACKER_PROMPT.md`。
4. 根据 `next_role` 发送对应角色文件（目录 `references/prompt-only/ROLE_PROMPTS/`）。
5. 顺序发送全部门禁文件（目录 `references/prompt-only/GATES_PROMPTS/`）。
6. 若全部通过，要求模型输出：
   - `RUNNER_STATE` 更新块
   - `scene_list` 更新块
   - `.context/NEXT_PROMPT.md`

## 三、落盘顺序（必须）
1. 保存 `.context/ROUTING_TRACE.json`
2. 保存 `.context/ROUTING_CONTEXT.md`
3. 保存/更新角色产物（章节正文、qa_result、critic_notes 等）
4. 保存 `.context/GATE_REPORT.json`
5. 保存 `.context/RUNNER_STATE.json`
6. 最后保存 `.context/NEXT_PROMPT.md`

## 四、失败回滚
当任一 blocking gate 失败：
1. 不修改 `scene_list.passes`
2. `RUNNER_STATE.last_error` 写入失败原因
3. 保留本轮 `ROUTING_TRACE` 与 `GATE_REPORT` 便于复盘

## 五、常见检查
1. `scene_list` 必须合法 JSON。
2. 当前章中文字符必须 >=2000。
3. 章节标题必须与 `scene_list.title` 对齐。
4. 发生一致性硬伤时必须 FAIL。

## 六、与脚本版互转
- Prompt-Only 产物可直接交给脚本版继续。
- 脚本版跑到中途也可切回 Prompt-Only 手工续跑。
