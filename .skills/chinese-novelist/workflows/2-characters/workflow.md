# Workflow: 2-Synopsis & Characters

> **Stage Goal**: Complete story synopsis and main character settings

---

## Checklist

- [ ] Write one-sentence logline
- [ ] Write 500-word story synopsis
- [ ] Complete protagonist profile
  - [ ] Basic info (name/age/occupation)
  - [ ] Personality traits (3 core keywords)
  - [ ] Fatal flaw
  - [ ] Core desire (Want) and true need (Need)
  - [ ] Catchphrases and language habits
  - [ ] Childhood trauma (optional)
- [ ] Complete main supporting characters (2-3 people)
- [ ] Define character relationship network

---

## Available Capabilities

| Capability | Trigger | Reference |
|:-----------|:---------|:-----------|
| Character Creation | "Help me design a character" | `references/guides/character-psychology-deep.md` |
| Character Template | "Character profile format" | `references/templates/character-depth-template.md` |
| Dialogue Design | "Design catchphrases" | `references/scenes/dialogue-writing.md` |
| Relationship Network | "Character relationships" | `references/hooks/team-dynamics.md` |

---

## Completion Criteria

To proceed to the next stage, the following must be true (human-checkable, and outline-ready):

1. `00-全局设定/00-策划书.md` includes:
- one-sentence logline
- ~500-word story synopsis (range is fine, but it must be long enough to outline from)
2. `00-全局设定/02-人设档案.md` is usable for drafting (not just a sketch):
- protagonist: basic info, 3 core traits, fatal flaw, Want/Need, voice/catchphrases, behavioral tells
- at least 2 key supporting characters: basic info + story function + relationship to protagonist
- relationship network is explicit (who wants what from whom, and what conflicts exist)
3. No major contradictions with existing `00-全局设定/01-世界观圣经.md` / project facts (if they already exist).

---

## Next Stage

After completion: `3-outline`

## Required Reads

- `00-全局设定/00-策划书.md` (genre, selling points, logline slot)
- `references/templates/character-depth-template.md`
- `references/guides/character-psychology-deep.md`

## Outputs (Write/Update)

- `00-全局设定/00-策划书.md`: one-sentence logline + 500-word synopsis
- `00-全局设定/02-人设档案.md`: protagonist + 2-3 key supports + relationship network

## Gates & Validation

- Character settings must be internally consistent and usable for outlining.

## DoD (Definition of Done)

- Logline exists in `00-全局设定/00-策划书.md`
- Protagonist profile completeness >= 80% in `00-全局设定/02-人设档案.md`
- At least 2 supporting characters have basic settings + relationships

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




