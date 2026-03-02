# Workflow: 4-Draft Preparation

> **Stage Goal**: Accumulate sufficient drafts to ensure stable serialization

---

## Checklist

- [ ] Complete chapters 1-10 first draft
- [ ] Complete chapters 11-20 first draft
- [ ] Total draft count reaches 50,000 words
- [ ] Self-check for language errors and logical issues
- [ ] Confirm opening quality (Golden Three Chapters)

---

## Available Capabilities

| Capability | Trigger | Reference |
|:-----------|:---------|:-----------|
| Chapter Writing | "Write chapter X" | Enter writing mode |
| Scene Writing | "Action scene/Dialogue scene" | `references/scenes/` |
| Self-Check Tools | "Check language errors" | `references/quality/ai-guardrails.md` |
| Opening Optimization | "Optimize opening" | `references/guides/golden-three-chapters.md` |

---

## Draft Targets

| Milestone | Chapters | Word Count | Status |
|:---------|:---------|:-----------|:-------|
| Batch 1 | 1-10 | 25k | ⏳ |
| Batch 2 | 11-20 | 25k | ⏳ |
| Total | 20 chapters | 50k | ⏳ |

---

## Completion Criteria

To proceed to the next stage, the following must be true (draft-buffer ready):

1. Draft buffer exists:
- `drafts/chapter_01.md` ... `drafts/chapter_20.md` exist (or your chosen buffer range)
- total word count meets your buffer target (default: >= 50,000 words)
2. `.context/scene_list.json` is usable for automation:
- schema-valid (no missing required fields)
- each buffered chapter is represented and points to the correct `drafts/chapter_XX.md`
- each scene item starts with `passes=false` (until QA/Polisher PASS writes it back)
3. Opening quality is not a gamble:
- the Golden Three Chapters are coherent (hook -> stakes -> promise -> escalation)
- at minimum, L1 issues (AI taste / empty emotion labels / dialogue monotone) have been addressed.

---

## Next Stage

After completion: `5-serialization`

## Required Reads

- `.context/STATE.md` and `.context/scene_list.json`
- `.context/VOLUME_XX.md` (current volume)
- `03-分章细纲.md`
- `references/quality/protocol-compliance.md` (Phase 1-5)

## Outputs (Write/Update)

- `drafts/chapter_01.md` ... `drafts/chapter_20.md` (first drafts)
- `.context/scene_list.json`: ensure each chapter points to `drafts/chapter_XX.md` and stays schema-valid

## Gates & Validation

- Opening quality gate: Golden Three Chapters must pass L1 + basic QA before entering serialization.

## DoD (Definition of Done)

- Draft buffer >= 50,000 words (or your project target)
- Chapters 1-20 first draft exist
- No obvious logical contradictions in the opening arc

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


