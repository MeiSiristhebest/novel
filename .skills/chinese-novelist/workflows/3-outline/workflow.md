# Workflow: 3-Outline Development

> **Stage Goal**: Complete story skeleton (coarse outline) and detailed plot points (fine outline)

---

## Checklist

### Coarse Outline (Mainline)
- [ ] Define core conflict of the whole book
- [ ] Plan volume structure
- [ ] Signature events per volume (3-5 items)
- [ ] Main plot progression

### Fine Outline (Volume 1)
- [ ] 2000-3500 word outline
- [ ] At least 30 plot points
- [ ] Core events per chapter
- [ ] Key foreshadowing points
- [ ] "Golden Three Chapters" design

---

## Available Capabilities

| Capability | Trigger | Reference |
|:-----------|:---------|:-----------|
| Golden Three Chapters | "Design opening" | `references/guides/golden-three-chapters.md` |
| Chapter Planning | "Plan chapters" | `references/guides/chapter-micro-structure.md` |
| Foreshadowing Design | "Plant foreshadowing" | `references/hooks/clue-dropping.md` |
| Pacing Control | "Adjust pacing" | `references/guides/emotional-beats.md` |
| Structure Techniques | "Three-act structure" | `references/templates/beat-sheet-template.md` |

---

## Completion Criteria

To proceed to the next stage, the following must be true (human-checkable, and runner-friendly):

1. `03-分章细纲.md` is runnable:
- Volume 1 has a clear arc (setup -> escalation -> climax -> aftershock)
- each planned chapter has an `outline_summary`
- each planned chapter has `scene_types` (so later routing can load the right scene skill packs)
- Volume 1 includes 30+ plot points (or an equivalent density that supports daily serialization)
- the "Golden Three Chapters" design is explicit and not left to improvisation
2. `.context/VOLUME_01.md` (or the current volume file) exists and has:
- volume targets + key events
- a chapter status placeholder list (so later updates can flip planned -> drafted -> QA pass)
3. `04-伏笔追踪表.md`, `05-时间线.md`, `06-细节追踪表.md` exist at least as skeletons (so Phase 1/5 have something to read/write).

---

## Next Stage

After completion: `4-drafts`

## Required Reads

- `00-策划书.md`, `01-世界观圣经.md`, `02-人物深度档案.md`
- `references/templates/beat-sheet-template.md`
- `references/guides/chapter-micro-structure.md`

## Outputs (Write/Update)

- `03-分章细纲.md`: Volume 1 fine outline (30+ plot points) + chapter core events
- `.context/VOLUME_01.md` (or current volume): volume arc, targets, chapter status placeholders
- `04-伏笔追踪表.md`, `05-时间线.md`, `06-细节追踪表.md`: create skeletons if missing

## Gates & Validation

- Outline must be runnable: each planned chapter has scene_types + outline_summary.

## DoD (Definition of Done)

- Coarse outline complete: volume division + signature events
- Fine outline complete: Volume 1 has 30+ plot points
- Golden Three Chapters plan exists in `03-分章细纲.md`

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


