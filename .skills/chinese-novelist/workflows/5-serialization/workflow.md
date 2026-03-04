# Workflow: 5-Serialization

> **Stage Goal**: Maintain stable updates, advance plot

---

## Daily Checklist

- [ ] Read current volume state (.context/VOLUME_XX.md)
- [ ] Read scene list (.context/scene_list.json)
- [ ] Read progress log (.context/PROGRESS.md)
- [ ] Confirm today's chapter goal
- [ ] Select one scene with passes=false
- [ ] Write 4000-6000 words
- [ ] Run QA gate before marking passes=true
- [ ] Update chapter progress
- [ ] Update foreshadowing tracker
- [ ] Record session log

---

## Available Capabilities

| Capability | Trigger | Reference |
|:-----------|:---------|:-----------|
| Continue Chapter | "Continue writing" | Load context and continue |
| Action Scene | "Write action scene" | `references/scenes/action-scene-guide.md` |
| Dialogue Scene | "Write dialogue" | `references/scenes/dialogue-writing.md` |
| Romance Scene | "Write romance scene" | `references/scenes/romance-scene-guide.md` |
| Daily Scene | "Write daily life" | `references/hooks/relaxed-tone.md` |
| Foreshadowing Recovery | "Recover foreshadowing" | `references/hooks/clue-dropping.md` |
| Chapter Hook | "Design hook" | `references/guides/hook-techniques.md` |

---

## Serialization Status

| Metric | Target | Current |
|:-------|:-------|:--------|
| Daily Word Count | 4000-6000 | ? |
| Weekly Chapters | 7 chapters | ? |
| Draft Buffer | >= 3 chapters | ? |

---

## Rollback Trigger Conditions

If the following issues are discovered, return to `3-outline`:
- Plot hits a dead end
- Character collapse that cannot be fixed
- Structural logical flaws

---

## Completion Criteria

This stage is iterative. For a single round / chapter to count as "complete" (and safe to proceed to the next round), all blocking gates must PASS:

1. Context is loaded without guessing:
- runtime state files are readable (`.context/STATE.md`, `.context/VOLUME_XX.md`, `.context/scene_list.json`, `.context/RUNNER_STATE.json`)
- routing produces a trace (`.context/ROUTING_TRACE.json`) and an injection excerpt (`.context/ROUTING_CONTEXT.md`)
- missing required files are blocked by gates (strict mode)
2. Writing and QA succeed:
- the selected scene is written, and QA/Polisher PASS
- in non-dry-run runs, `passes=true` is written back into `.context/scene_list.json`
3. Phase 5 sync is done:
- `00-全局设定/07-项目状态.md` + `.context/VOLUME_XX.md` + `03/04/05/06` are updated for this chapter
- `.context/RUNNER_STATE.json` reflects the new progress

---

## Next Stage

When a volume is complete, proceed to: `6-revision`

## Required Reads

- `.context/STATE.md`
- `.context/VOLUME_XX.md` (current volume)
- `.context/scene_list.json` (select one scene where `passes=false`)
- `03-分章细纲.md`, `00-全局设定/04-伏笔追踪表.md`, `00-全局设定/05-时间线.md`, `00-全局设定/06-细节追踪表.md`

## Outputs (Write/Update)

- `drafts/chapter_XX.md` (new chapter)
- `.context/qa_result.json`, `.context/polisher_result.json` (structured outputs)
- `.context/RUNNER_STATE.json` (progress + last_error)
- When QA/Polisher PASS and not dry-run: write `.context/scene_list.json` item `passes=true`
- Phase 5 sync must update the 6 state views:
  - `00-全局设定/07-项目状态.md`
  - `.context/VOLUME_XX.md`
  - `03-分章细纲.md`
  - `00-全局设定/04-伏笔追踪表.md`
  - `00-全局设定/05-时间线.md`
  - `00-全局设定/06-细节追踪表.md`

## Gates & Validation (Strict)

- Context pack gates: language pack + engine pack (if applicable) + scene schema
- Quality gates: L1 + wordcount + consistency
- Phase 5 gate: 6-file sync is required; any blocking failure stops the round

> Reference: `references/quality/protocol-compliance.md` Phase 4/5.

## DoD (Definition of Done)

- Chapter written and QA PASS
- `passes=true` recorded for the selected scene (non-dry-run)
- 6 state views updated for this chapter

## Commands (Optional)

> These are optional helpers. If you run the full automation, prefer the wrapper scripts.

### PowerShell

```pwsh
# From repo root
pwsh -File .skills/chinese-novelist/tools/run-novel-automation.ps1 -Novel "<NovelName>" -Pipeline writer-qa -Rounds 1 -StrictGates true -SyncViews true -AuditProtocol true
```

### Bash

```bash
# From repo root
bash .skills/chinese-novelist/tools/run-novel-automation.sh "<NovelName>" writer-qa 1 true true 1 claude sonnet "" OPENAI_API_KEY "" false true
```


