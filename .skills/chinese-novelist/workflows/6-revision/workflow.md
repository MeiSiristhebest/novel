# Workflow: 6-Revision & Polishing

> **Stage Goal**: Optimize quality of completed chapters

---

## Checklist

### Structure Level
- [ ] Check if chapter pacing is reasonable
- [ ] Check for plot loopholes
- [ ] Check if all foreshadowing is recovered
- [ ] Check if character arc is complete

### Language Level
- [ ] Fix language errors and typos
- [ ] Optimize dialogue naturalness
- [ ] Delete redundant descriptions
- [ ] Strengthen golden sentences and emotional peaks

### AI Trace Check
- [ ] Follow `references/quality/ai-guardrails.md` (Chinese writing context)
- [ ] Remove obvious AI connective fillers and abstract summaries
- [ ] Ensure show-dont-tell and sentence variety

---

## Available Capabilities

| Capability | Trigger | Reference |
|:-----------|:---------|:-----------|
| Chapter QC | "QC chapter X" | `references/quality/` |
| Language Polishing | "Polish" | `references/guides/language-craft.md` |
| AI De-flavoring | "Remove AI taste" | `references/quality/ai-guardrails.md` |
| Editor Review | "Get editor opinion" | `references/prompts/chief-editor.md` |

---

## Completion Criteria

To proceed to the next stage, the following must be true (publish-ready):

1. Volume QC coverage is complete:
- every chapter in the volume has been reviewed for structure + logic + consistency
- key checks are recorded somewhere persistent (recommended: `.context/VOLUME_XX.md` + `00-全局设定/07-项目状态.md`), not only in chat
2. Quality gates are cleared for Chinese web-serial context:
- L1 issues are cleared (AI taste, abstract telling, repetitive sentence patterns, flat dialogue)
- the chapter meets the score thresholds in `references/quality/quality-checklist.md` and `references/quality/genre-quality-checklist.md`
- `references/quality/ai-guardrails.md` is satisfied (no forbidden patterns)
3. Consistency does not regress:
- `00-全局设定/04-伏笔追踪表.md`, `00-全局设定/05-时间线.md`, `00-全局设定/06-细节追踪表.md` are updated to reflect any revisions.

---

## Next Stage

After completion: `7-feedback`

## Required Reads

- Completed chapters `drafts/chapter_XX.md`
- `00-全局设定/04-伏笔追踪表.md`, `00-全局设定/05-时间线.md`, `00-全局设定/06-细节追踪表.md` (consistency)
- `references/quality/quality-checklist.md` + `references/quality/genre-quality-checklist.md`

## Outputs (Write/Update)

- Revised chapters (either in-place under `drafts/` or in a dedicated revision folder)
- For each revised chapter, keep QA/Polisher structured results under `.context/` for traceability

## Gates & Validation

- Must pass L1 + checklist score thresholds before publishing
- Consistency must not regress relative to trackers

## DoD (Definition of Done)

- Full volume QC complete
- AI trace check cleared per `ai-guardrails.md`
- No obvious language errors or structural loopholes

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



