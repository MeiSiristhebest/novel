# Workflow: 1-Genre Positioning

> **Stage Goal**: Define target audience, select genre, establish core selling points

---

## Checklist

- [ ] Define writing goal (publishing/self-entertainment/competition)
- [ ] Determine target reader demographics
- [ ] Select base genre
- [ ] Select goldfinger engine (optional)
- [ ] Define core selling points (1-2 items)
- [ ] Select reference works (2-3 books)

---

## Available Capabilities

| Capability | Trigger | Reference |
|:-----------|:---------|:-----------|
| Genre Navigation | "What genres are available" | `references/templates/genre_registry_v3.json` |
| Engine Selection | "What goldfingers are available" | `references/engine-modules/` |
| Market Analysis | "Analyze this genre" | `references/theory/commercial-success.md` |
| Benchmark Analysis | "Analyze this book" | `references/theory/deconstructing-masterpieces.md` |

---

## Completion Criteria

To proceed to the next stage, the following must be true (human-checkable, and runner-friendly):

1. `00-全局设定/00-策划书.md` has explicit, copy-pastable facts (do not keep them only in chat):
- target readers + platform
- genre keyword(s) (must include the Chinese keyword you want detection to hit)
- 1-2 core selling points
- 2-3 reference works
2. Engine decision is explicit:
- either an engine/module keyword is written into `00-全局设定/00-策划书.md` or `00-全局设定/01-世界观圣经.md`
- or it is explicitly marked as none (so later routing does not "guess")
3. If you intend to use a deterministic style exemplar, record the chosen exemplar filename under `references/style-exemplars/` in `00-全局设定/00-策划书.md` (so prompts can load it without sampling).

---

## Next Stage

After completion: `2-characters`

## Required Reads

- `references/templates/genre_registry_v3.json` (genre list + style exemplar SSOT)
- `references/project-structure.md` (project files you will write)
- If the project already exists: `00-全局设定/00-策划书.md` and `00-全局设定/01-世界观圣经.md`

## Outputs (Write/Update)

- `00-全局设定/00-策划书.md` must explicitly record:
  - target readers + platform
  - genre keyword(s) (must include the Chinese keyword used for detection)
  - core selling points (1-2)
  - reference works (2-3)
  - goldfinger / engine (optional)

> Note: the runner detects genre/engine from `00-全局设定/00-策划书.md` and `00-全局设定/01-世界观圣经.md`. Do not keep these only in chat.

## Gates & Validation

- DoD is content-level: the next stage should be able to proceed without guessing genre/engine.

## DoD (Definition of Done)

- Genre chosen and written into `00-全局设定/00-策划书.md` using an explicit keyword
- Engine choice written into `00-全局设定/00-策划书.md` (or explicitly marked as none)
- 1-2 selling points + 2-3 reference works recorded

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



