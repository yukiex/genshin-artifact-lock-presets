---
name: genshin-lock-set-authoring
description: Add or revise a Genshin Impact artifact set in this repository by researching current Lock Assistance behavior, collecting EN/CN-first build references, authoring per-set YAML presets, syncing presets/lock-presets.yml, and leaving a traceable survey note with exact URLs and evidence.
---

# Genshin Lock Set Authoring

Use this skill only inside the `genshin-artifact-lock-presets` repository layout that contains `presets/`, `docs/`, `README.md`, and `AGENTS.md`.

This skill is for authoring or revising one artifact set end to end:
- decide or confirm `set_id`
- create or update `recommended`, `setting1`, `setting2`
- transcribe in-game Lock Assist screenshots into YAML
- sync `presets/lock-presets.yml`
- leave a traceable survey note with exact sources, access dates, and inference notes

## Core Principles

1. EN/CN first, JP second
   - Prefer English and Chinese theory/build sources when they are more concrete than Japanese summaries.
   - Use Japanese guides as a consensus check or fallback, not the only authority.

2. `recommended` is transcription, `setting1/2` are authored
   - `recommended` evidence priority is: still screenshots, then screen recording, then a human-written per-slot memo.
   - If still screenshots are unavailable, `recommended` may be authored from recording or memo, but the survey note must say `Evidence level: provisional`.
   - `setting1` and `setting2` must represent different character archetypes, not merely strict or lenient variants.

3. Traceability beats cleverness
   - Every authored threshold needs a source trail.
   - If you infer something that no source states directly, label it as `Inference:` in the survey note.

4. Keep the aggregate file in sync
   - `presets/lock-presets.yml` is the distribution catalog and must never drift from per-set files.

## Open These Files First

Open these files before making any edits:

1. `AGENTS.md`
   - Follow the repo contribution rules and the section `新規セット追加ワークフロー`.

2. `README.md`
   - Confirm schema, current set naming, current repo layout, and validation checklist.
   - Treat README as the source of truth for current folder coverage and set examples.

3. `docs/ui-mapping.md`
   - Use this to map game UI strings into YAML abbreviations and slot semantics.

4. `docs/lock-assist-survey-template.md`
   - Copy this template before writing any new survey note.

5. One complete existing example
   - Open one existing set end to end:
     - `presets/tenkyu/recommended.yml`
     - `presets/tenkyu/setting1.yml`
     - `presets/tenkyu/setting2.yml`
     - `presets/lock-presets.yml`
     - one survey note such as `docs/kokuyo-hiten-lock-assist-survey.md`

6. `references/checklist.md`
   - Use the checklist in this skill directory as the final done-definition and source-quality gate.

## Source Priority

Use sources in this order unless the task explicitly needs something else.

### A. Official or primary-like sources for feature semantics
Use these for Lock Assistance behavior, wording, and set names:
- HoYoLAB version update or feature preview posts about Artifact Auto-Lock or Lock Assistance
- HoYoWiki artifact pages
- in-game screenshots supplied by the human

Use these sources to answer:
- what the feature is currently called
- what UI wording exists
- what the in-game recommended plan actually selects
- whether the current UI allows or forbids a mapping

### B. English theorycrafting sources
Use these for build logic:
- KQM artifact guide
- KQM character guides or quick guides

Use KQM when you need:
- ER requirement reasoning
- whether ER Sands is a real option
- whether Goblet can be ATK%, EM, or elemental damage depending on team
- whether Crit-only filtering would be too narrow
- target character lists for a specific archetype

### C. Chinese detailed build sources
Use these for main stat and substat specificity:
- BWiki artifact pages
- BWiki character `/攻略` pages
- Bilibili long-form artifact or build articles only as supplementary evidence

Use BWiki when you need:
- 主词条推荐 / 副词条推荐
- stat priority ordering with reasons
- archetype splits that Japanese guides often summarize too loosely
- concrete examples such as Favonius builds wanting CR or ER-until-threshold support logic

### D. Validation or reality-check sources
Use these after drafting `setting1/2`:
- Genshin Optimizer
- gcsim artifact substat optimizer
- Akasha artifact rankings or artifact pages

Use them to sanity-check:
- whether a preset is obviously overfitted
- whether the chosen stat family matches real optimized or ranked builds
- whether CV-only logic would miss valid HP%, DEF%, EM, or ER pieces

### E. Japanese fallback or consensus sources
Use only after checking EN/CN sources, or when EN/CN is sparse:
- Game8
- GameWith
- 神ゲー攻略
- Gamerch

Use JP sources mainly to:
- confirm recommended users of a set
- cross-check that a proposed archetype is not fringe
- fill gaps when newer sets have weak EN coverage

## Practical Research Playbook

For each new set, research in this order.

### 1. Confirm the set itself
Find and record:
- official Japanese set name
- official or widely used English set name
- candidate `set_id`
- why the chosen `set_id` matches repo convention

`set_id` rules:
- lowercase ASCII only
- hyphen-separated when needed
- stable and mnemonic
- prefer existing repo naming style over perfect romanization
- if there is ambiguity, document rejected alternatives in the survey note

Do not blindly force one naming style. Match the repo’s existing convention and document your rationale.

### 2. Decide which characters actually matter
Collect a target list from EN/CN sources:
- who actually uses the set
- which archetypes are materially different
- whether support, reaction, burst-reliant, HP-scaling, DEF-scaling, or EM-scaling variants exist

If the set has only one real archetype, still design `setting1/2` as the two most meaningful subtypes.
Good examples:
- on-field crit carry
- reaction or ER-heavy driver
Not good examples:
- strict mode
- lenient mode

### 3. Design authored presets
Author three files:
- `recommended.yml`
- `setting1.yml`
- `setting2.yml`

Their roles are:

#### `recommended`
- transcribe from the best available evidence in this order: still screenshots, then screen recording, then human per-slot memo
- no theory improvement
- if still screenshots are missing, continue only when recording or memo exists and mark the survey note as `Evidence level: provisional`

#### `setting1`
- the most common or highest-confidence authored archetype
- should be useful for many players of the set

#### `setting2`
- a second real archetype, not a weaker copy
- should justify its existence with materially different stat priorities
- `setting1` and `setting2` may be created before `recommended` evidence is finalized

### 4. Validate the authored logic
Before finalizing `setting1/2`, ask:
- does this archetype really want ER before offensive stats?
- is Goblet allowed to be ATK% or EM, or should it be elemental-only?
- is Circlet allowed to be ATK%, Healing%, HP%, or DEF% in this archetype?
- are HP%, DEF%, EM, or ER actually valid substats here?
- is a Favonius build forcing CR as a practical requirement?

Then cross-check with:
- KQM quick guide if available
- BWiki `/攻略`
- Genshin Optimizer, gcsim, or Akasha for sanity

## Screenshot Transcription Rules

Transcribe `recommended` from the strongest available evidence:
- still screenshots under `docs/reference/<set-id>-lock/`
- or a screen recording that clearly shows all five slots
- or a human-written per-slot note

Expected slots:
- flower
- plume
- sands
- goblet
- circlet

For each slot, map exactly:
- main stats selected in UI -> `main_allowed`
- candidate substats under “any of these” -> `substats_required_any_of`
- threshold like “at least N” -> `substats_required_min`
- yellow highlighted mandatory stats -> `substats_required_all_of`

### Important mapping rules

1. Flower and plume mains are always fixed in YAML:
   - flower: `[HP]`
   - plume: `[ATK]`

2. Use `docs/ui-mapping.md` abbreviations exactly:
   - `CR`, `CD`, `ER`, `EM`, `ATK%`, `HP%`, `DEF%`, `ATK`, `HP`, `DEF`
   - elemental goblets must be enumerated explicitly
   - add `PhysicalDMG%` only if the plan should allow physical goblets

3. If the UI offers a broad elemental-damage selection, YAML must still enumerate:
   - `PyroDMG%`
   - `HydroDMG%`
   - `ElectroDMG%`
   - `AnemoDMG%`
   - `CryoDMG%`
   - `GeoDMG%`
   - `DendroDMG%`

4. Do not silently “fix” the screenshot during transcription.
   - If the in-game recommendation looks questionable, transcribe it faithfully into `recommended`.
   - Put improved logic into `setting1/2`, not into `recommended`.

5. Record the exact evidence artifact for every slot in the survey note.
6. If the evidence is a recording or memo rather than still screenshots, add `Evidence level: provisional` to the survey note.

## Survey Note Requirements

Create:
- `docs/<set-id>-lock-assist-survey.md`

Create or reuse:
- `docs/reference/<set-id>-lock/`

The survey note must contain all of the following.

### A. Source log
For every non-screenshot source, record:
- page title
- URL
- language (`EN`, `ZH`, `JA`, `Official`)
- access date in `YYYY-MM-DD`
- what you used it for
- whether it is direct evidence or inference support

Use this table shape inside the survey note:

| Kind | Page title | URL | Lang | Accessed | Used for | Evidence type |
| --- | --- | --- | --- | --- | --- | --- |
| Official | ... | ... | Official | 2026-03-24 | Lock Assistance wording or feature semantics | direct |
| Guide | ... | ... | EN | 2026-03-24 | ER or main-stat or substat priority | direct |
| Guide | ... | ... | ZH | 2026-03-24 | archetype split or stat rationale | direct |
| Validation | ... | ... | EN | 2026-03-24 | sanity-check authored preset | supporting |

### B. Recommended transcription table
For each slot, record:
- evidence artifact or memo reference
- main stats
- candidate substats
- mandatory substats
- exact UI wording if visible

### C. Archetype decision log
For `setting1` and `setting2`, write:
- target archetype
- target characters
- main stat rationale
- substat rationale
- why this differs from the other setting
- what was rejected and why

### D. Explicit inference blocks
Whenever the source does not directly say the final YAML condition, add:

`Inference: ...`

Examples:
- `Inference: KQM says ER until requirement, BWiki lists CR for Favonius, so sands allows ER% and circlet allows CR for the support archetype.`
- `Inference: The set is mostly used by on-field carries, but one ZH guide highlights a reaction-driver variant, so setting2 is assigned to EM/ER-heavy usage.`

### E. Final file checklist
Mark all affected files:
- `presets/<set-id>/recommended.yml`
- `presets/<set-id>/setting1.yml`
- `presets/<set-id>/setting2.yml`
- `presets/lock-presets.yml`
- `docs/ui-mapping.md` if needed
- `README.md` if schema wording changed

## Editing Rules

- Keep two-space indentation.
- Keep key order:
  - `version`
  - `set_id`
  - `set_name_ja`
  - `preset`
- Keep slot order:
  - `flower`
  - `plume`
  - `sands`
  - `goblet`
  - `circlet`
- Keep filenames and directories lowercase and hyphenated.
- Preserve existing wrapping style for inline lists.
- Use `targets` for discoverability, but remember it does not affect lock logic.

Do not introduce new abbreviations or field names unless you also update:
- `docs/ui-mapping.md`
- `README.md` if the schema meaning changed

## Workflow

1. Read `AGENTS.md`, `README.md`, `docs/ui-mapping.md`, `docs/lock-assist-survey-template.md`, and `references/checklist.md`.
2. Open one full existing example set and survey note.
3. Confirm set names and decide `set_id`.
4. Create:
   - `docs/reference/<set-id>-lock/`
   - `docs/<set-id>-lock-assist-survey.md`
   - `presets/<set-id>/recommended.yml`
   - `presets/<set-id>/setting1.yml`
   - `presets/<set-id>/setting2.yml`
5. Research target characters and two archetypes from EN/CN-first sources.
6. Wait for the best available `recommended` evidence. Prefer still screenshots, but proceed with recording or memo if provided.
7. Transcribe evidence exactly into `recommended.yml`.
8. Author `setting1.yml` and `setting2.yml` from theory and build sources.
9. Mirror all finalized values into `presets/lock-presets.yml`.
10. Update `docs/ui-mapping.md` or `README.md` only if required.
11. Run validation commands.
12. Update the survey note with exact URLs, dates, filenames, and inference notes.
13. Summarize:
   - what was changed
   - what sources were used
   - what remains uncertain

## Validation

Run:

```bash
yamllint presets docs
```

Then verify structure using whichever `yq` is installed locally.
If it is Mike Farah `yq`:

```bash
yq eval '.preset.slots | keys' presets/<set-id>/recommended.yml
yq eval '.. | select(has("substats_required_min"))' presets/<set-id>/*.yml >/dev/null
```

If it is the Python wrapper around `jq`, adapt the command form accordingly.

Also verify:
- all three per-set YAML files contain all five slots
- `presets/lock-presets.yml` matches the per-set files
- `recommended` reflects evidence exactly
- `setting1/2` are different archetypes, not strict or lenient clones

If still screenshots are missing, or if a source is ambiguous, say so explicitly in the final report and note whether `recommended` is provisional.

## Default Search Queries

Use these as starting points.

### Official
- `site:hoyolab.com Genshin "Artifact Auto-Lock"`
- `site:hoyolab.com Genshin "Lock Assistance"`
- `site:wiki.hoyolab.com Genshin artifacts lock assistance`

### English theory
- `site:keqingmains.com/q "<character name>" quick guide`
- `site:keqingmains.com "<set name>" artifacts`
- `site:keqingmains.com "<character name>" ER requirements`

### Chinese detail
- `site:wiki.biligame.com/ys "<character name>/攻略" 圣遗物`
- `site:wiki.biligame.com/ys "<set name>" 圣遗物`
- `site:bilibili.com/read "<set name>" 圣遗物 主词条 副词条`

### Japanese fallback
- `site:game8.jp/genshin "<set name>"`
- `site:gamewith.jp/genshin "<set name>"`
- `site:kamigame.jp/genshin "<set name>"`
- `site:gamerch.com/genshinwiki "<set name>"`

## Done Definition

The task is complete only when all of the following are true:
- one set has complete `recommended`, `setting1`, `setting2`
- `presets/lock-presets.yml` is in sync
- survey note exists and includes exact URLs, access dates, evidence artifacts, and inference notes
- lint or structural checks were run, or blockers were reported explicitly
- any uncertainty is written down instead of hidden
