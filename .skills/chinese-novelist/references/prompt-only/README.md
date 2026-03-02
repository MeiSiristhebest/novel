# Prompt-Only 控制面（非脚本版本）

本目录提供一套不依赖 Python/PowerShell 的手工写作闭环协议。

## 适用场景
- 通用 LLM 对话框（ChatGPT / Claude / Codex 等）
- 无法运行本地脚本，但希望继续使用 `.context` 作为状态真相源
- 需要与脚本版 (`tools/novel_agent_runner.py`) 产物保持同构

## 核心原则
1. `.context` 是唯一事实源（SSOT）。
2. 命中文件默认全文注入，不做“前800字”截断。
3. 不固定“前4个文件”，按相关性自动选集并分批注入。
4. 任一阻断门禁失败即停机，不推进 `scene_list.passes`。

## 目录说明
- `MASTER_ORCHESTRATOR.md`：总控协议（Phase 0-5）
- `SOP_MANUAL_RUN.md`：手工执行步骤
- `ROUTER_PROMPT.md`：自动选文件 Prompt
- `CONTEXT_PACKER_PROMPT.md`：全文分批注入 Prompt
- `ROLE_PROMPTS/`：角色 Prompt 集
- `GATES_PROMPTS/`：门禁 Prompt 集
- `OUTPUT_CONTRACTS.md`：统一输出契约
- `MANUAL_TEMPLATES/`：落盘模板
