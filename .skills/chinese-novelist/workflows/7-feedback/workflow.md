# Workflow: 7-Feedback & Iteration

> **Stage Goal**: Optimize subsequent creation based on reader feedback

---

## Checklist

### Data Collection
- [ ] Collect reader comments (positive/negative)
- [ ] Analyze drop-off points (which chapter lost readers)
- [ ] Track subscription/favorite trends
- [ ] Identify readers' favorite plots

### Analysis & Adjustment
- [ ] Summarize successful elements
- [ ] Identify areas needing improvement
- [ ] Adjust subsequent creation direction
- [ ] Update character/plot strategy

---

## Available Capabilities

| Capability | Trigger | Reference |
|:-----------|:---------|:-----------|
| Reader Simulation | "Simulate reader comments" | `references/prompts/reader-simulator.md` |
| Review Analysis | "Review this volume" | `references/theory/learning-from-reading.md` |
| Strategy Adjustment | "Adjust strategy" | `references/theory/commercial-success.md` |

---

## Feedback Analysis Template

| Dimension | Reader Feedback | Adjustment Plan |
|:---------|:----------------|:----------------|
| Pacing | (to be collected) | |
| Characters | (to be collected) | |
| Cool Factor | (to be collected) | |
| Emotion | (to be collected) | |

---

## Completion Criteria

The following conditions must be met (so the next volume is directionally correct, not random):

1. Feedback is summarized into concrete, testable changes:
- what worked (keep)
- what caused drop-off (fix)
- what the reader is actually paying for (double down)
2. Adjustments are written into project artifacts (not only in chat):
- `00-全局设定/07-项目状态.md`: lessons learned + next direction + risk list
- `.context/VOLUME_XX.md`: retrospective + what changes in the next volume
- `00-全局设定/00-策划书.md`: update positioning if your assumptions were wrong
3. The next outline reflects the adjustments:
- before returning to serialization, the next volume plan (or the next chapters) is updated in `03-分章细纲.md` / the next `.context/VOLUME_XX.md`.

---

## Next Stage

- Start new volume: Return to `5-serialization`
- Book complete: Project archive

## Required Reads

- `.context/STATE.md` + `.context/VOLUME_XX.md`
- Recent chapters + session logs (if present)
- Reader feedback samples (comments, ratings, drop-off points)

## Outputs (Write/Update)

- `00-全局设定/07-项目状态.md`: lessons learned + next volume direction
- `.context/VOLUME_XX.md`: retrospective + adjustments for next volume
- `00-全局设定/00-策划书.md`: update positioning if the market signal contradicts assumptions
- `08-素材碎片.md` (optional): quote snippets, reader language, hook ideas

## Gates & Validation

- Adjustments must be reflected in the next outline before restarting serialization.

## DoD (Definition of Done)

- Feedback summarized into actionable changes
- Next volume direction confirmed and written into state/volume docs

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



