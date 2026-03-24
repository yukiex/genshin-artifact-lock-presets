# Genshin Lock Set Authoring Checklist

Use this checklist together with `SKILL.md` when adding or revising one set.

## 1. Pre-flight

- [ ] I am inside the correct repository layout containing `README.md`, `AGENTS.md`, `docs/`, and `presets/`.
- [ ] I opened `AGENTS.md` and checked the section `新規セット追加ワークフロー`.
- [ ] I opened `README.md` and confirmed the current schema, naming style, and preset catalog.
- [ ] I opened `docs/ui-mapping.md` and will use its abbreviations exactly.
- [ ] I opened `docs/lock-assist-survey-template.md`.
- [ ] I opened one full example set end to end, including one survey note.

## 2. Minimum source quality

Required minimum evidence for a new authored set:

- [ ] 1 official or primary-like source for Lock Assistance wording or set naming
- [ ] 1 English theory source such as KQM
- [ ] 1 Chinese detailed build source such as BWiki `/攻略`
- [ ] 1 validation or reality-check source if `setting1` or `setting2` contains meaningful inference

Notes:
- JP-only authoring is allowed only when EN/CN coverage is clearly weak, and that exception must be written into the survey note.
- Bilibili or forum posts may support a decision, but should not be the only source for the main logic.

## 3. Set identity and naming

- [ ] I recorded the official Japanese set name.
- [ ] I recorded an official or widely used English set name.
- [ ] I chose a `set_id` that matches this repo’s naming style.
- [ ] If the `set_id` was ambiguous, I documented rejected alternatives in the survey note.

## 4. Research output

- [ ] I identified which characters actually use the set.
- [ ] I identified two meaningful archetypes for `setting1` and `setting2`.
- [ ] `setting1` and `setting2` are not just strict and lenient copies.
- [ ] I wrote down why each archetype exists.
- [ ] I wrote down what options I rejected.

## 5. Files to create or update

- [ ] `presets/<set-id>/recommended.yml`
- [ ] `presets/<set-id>/setting1.yml`
- [ ] `presets/<set-id>/setting2.yml`
- [ ] `presets/lock-presets.yml`
- [ ] `docs/<set-id>-lock-assist-survey.md`
- [ ] `docs/reference/<set-id>-lock/` exists or was updated
- [ ] `docs/ui-mapping.md` was updated if new abbreviations or mapping rules were introduced
- [ ] `README.md` was updated if schema wording or contributor instructions changed

## 6. Recommended transcription gate

Do not invent `recommended`.

- [ ] I have `recommended` evidence in one of these forms: still screenshots, screen recording, or a human-written per-slot memo.
- [ ] I used the best available evidence in this priority order: still screenshots, then screen recording, then memo.
- [ ] I transcribed the evidence exactly without “improving” it.
- [ ] I recorded the evidence artifact or memo reference for each slot in the survey note.
- [ ] If the evidence is not still screenshots, the survey note says `Evidence level: provisional`.
- [ ] If the evidence looked suboptimal, I kept that logic in `recommended` and moved improvements to `setting1/2`.

## 7. YAML content checks

For each of `recommended.yml`, `setting1.yml`, and `setting2.yml`:

- [ ] top-level key order is `version`, `set_id`, `set_name_ja`, `preset`
- [ ] slots exist for `flower`, `plume`, `sands`, `goblet`, `circlet`
- [ ] every slot has `main_allowed`
- [ ] every slot has `substats_required_all_of`
- [ ] every slot has `substats_required_any_of`
- [ ] every slot has `substats_required_min`
- [ ] abbreviations match `docs/ui-mapping.md`
- [ ] elemental goblets are explicitly enumerated when needed
- [ ] two-space indentation is preserved

## 8. Survey note completeness

The survey note must include:

- [ ] source log with page title, URL, language, accessed date, usage, and evidence type
- [ ] recommended transcription table for all five slots
- [ ] archetype decision log for `setting1`
- [ ] archetype decision log for `setting2`
- [ ] explicit `Inference:` blocks wherever the final YAML is not directly stated by sources
- [ ] final list of changed files
- [ ] unresolved ambiguity or remaining uncertainty, if any

## 9. Sync and validation

- [ ] `presets/lock-presets.yml` matches the per-set YAML files.
- [ ] I ran `yamllint presets docs` or reported why I could not.
- [ ] I ran structural checks with local `yq` or equivalent, or reported the blocker.
- [ ] I explicitly mentioned any missing screenshots, provisional evidence, lint failures, or pre-existing repo issues.

## 10. Final report

The final report should mention:

- [ ] what files changed
- [ ] what exact sources were used
- [ ] what parts are transcription versus authored inference
- [ ] what remains uncertain

## Suggested source buckets

Use these buckets in the survey note so later contributors can audit decisions quickly:

- `Official`
- `Guide-EN`
- `Guide-ZH`
- `Guide-JA`
- `Validation`
- `Screenshot`
