# DEPRECATIONS

## 目标
本文件集中记录 `chinese-novelist` 历史文档与接口的废弃状态、替代项和迁移建议。

## 已废弃（保留兼容）

### 1. `AUDIT_REPORT.md`
- 状态：Deprecated（历史审计快照）
- 替代：
  - `scripts/check_references.py`
  - `scripts/validate_integrity.py`
  - `tools/validate_runtime.py`

### 2. `FIXES_APPLIED.md`
- 状态：Deprecated（历史修复日志）
- 替代：
  - `CHANGELOG.md`
  - 本文件（DEPRECATIONS）

### 3. 旧运行时路径写入逻辑（`.skills/chinese-novelist/novels`）
- 状态：Deprecated
- 替代：仓库根 `novels/`

### 4. 非结构化质检结果
- 状态：Deprecated
- 替代：
  - `qa_result.json`
  - `polisher_result.json`
  - `critic_notes.md` 末尾 JSON 摘要

## 迁移建议
1. 先运行：`python tools/migrate_novel_state.py --novel <name>`（dry-run）
2. 再运行：`python tools/migrate_novel_state.py --novel <name> --apply`
3. 验证：`python tools/validate_runtime.py --novel <name>`
