# data/ 目录说明

## 用途

`data/` 目录存放 **Python 工具脚本使用的模板文件**，用于初始化项目的 `.context/` 隐藏状态目录。

`.context/` 是运行时唯一事实源（SSOT）。根目录 `00-07` 文档属于衍生视图，应通过 `tools/sync_project_views.py` 同步更新。

## 与 references/templates/ 的区别

| 目录 | 服务对象 | 生成内容 | 入口工具 |
|:-----|:---------|:---------|:---------|
| `data/` | `tools/novel_agent_runner.py` | `.context/` 运行态文件（STATE.md, VOLUME_XX.md, scene_list.json 等） | 长程写作 Harness |
| `references/templates/` | `tools/quick_start.py`（部分使用）+ 手工 | 用户可见模板/注册表（SSOT：genre_registry_v3.json）。QuickStart v3.1+ 直接写 00-02 最小骨架，但仍会读取注册表。 | QuickStart + 手工 |

两者不重复，服务于不同入口与不同文件层级。

## 文件清单

| 文件 | 用途 |
|:-----|:-----|
| `state-template.md` | `.context/STATE.md` 的模板 |
| `volume-template.md` | `.context/VOLUME_XX.md` 的模板 |
| `session-log-template.md` | `.context/SESSION_LOG.md` 的模板 |
| `scene-list-template.json` | `.context/scene_list.json` 的模板 |
| `progress-template.md` | `.context/PROGRESS.md` 的模板 |
| `command-whitelist.txt` | `command` 后端白名单（`tools/novel_agent_runner.py` 读取并做前缀匹配） |

## Schema 对应（最佳实践）

- `.context/scene_list.json` 对应 `schemas/scene_list.schema.json`（严格模式会校验 `schema_version` 等关键字段）。
- `.context/RUNNER_STATE.json` 对应 `schemas/runtime_state.schema.json`。
- `.context/ROUTING_TRACE.json`、`.context/PHASE5_SYNC_TRACE.json` 对应 `schemas/routing_trace.schema.json`、`schemas/phase5_sync_trace.schema.json`（严格模式门禁会校验）。
