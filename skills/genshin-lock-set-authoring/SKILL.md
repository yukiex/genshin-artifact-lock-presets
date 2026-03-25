---
name: genshin-lock-set-authoring
description: Add or revise a Genshin Impact artifact set in this repository by researching Lock Assist behavior, authoring per-set YAML presets, maintaining survey notes under docs/surveys, and keeping targets/targets_ja aligned.
---

# Genshin Lock Set Authoring

Use this skill only inside this repository.

## Purpose

This skill is for adding or revising one artifact set end to end:

- confirm `set_id`
- create or update `presets/<set-id>/recommended.yml`
- create or update `presets/<set-id>/setting1.yml`
- create or update `presets/<set-id>/setting2.yml`
- create or update `docs/surveys/<set-id>.md`
- create or update `docs/references/<set-id>/`
- keep `targets` and `targets_ja` aligned

## Core Rules

1. EN/CN first, JP second
   - Prefer English theory sources and Chinese build detail when available.
   - JP-only authoring is allowed when EN/CN coverage is clearly weak; record that in the survey note.

2. `recommended` is transcription, `setting1/2` are authored
   - `recommended` must come from still screenshots, screen recording, or a human memo.
   - `setting1` and `setting2` must represent different archetypes, not strict / lenient copies.

3. Per-set files are the source of truth
   - There is no aggregate catalog file.
   - Update only the per-set YAML files and the matching survey note.

4. `targets` requires `targets_ja`
   - If a preset declares `targets`, it must also declare `targets_ja`.
   - Keep both lists in the same order.

## Open These Files First

1. `AGENTS.md`
2. `README.md`
3. `docs/ui-mapping.md`
4. `docs/surveys/template.md`
5. one complete set example under `presets/` and `docs/surveys/`
6. `skills/genshin-lock-set-authoring/references/checklist.md`

## Repository Conventions

- Survey notes live in `docs/surveys/`.
- Reference screenshots live in `docs/references/<set-id>/`.
- Canonical screenshot names are `flower.png`, `plume.png`, `sands.png`, `goblet.png`, `circlet.png`.
- Validation uses the local `yq` style: `yq '.preset.slots | keys' file.yml`.

## Workflow

### 1. Confirm the set
Record:
- Japanese set name
- English set name
- `set_id`
- naming rationale if there was ambiguity

### 2. Decide the archetypes
Find:
- who actually uses the set
- what two archetypes are worth encoding as `setting1` and `setting2`
- which stats meaningfully separate those archetypes

### 3. Author the YAML files
For each file:
- keep top-level order as `version`, `set_id`, `set_name_ja`, `preset`
- if `targets` exists, add `targets_ja`
- ensure all five slots exist
- ensure every slot has `main_allowed`, `substats_required_any_of`, `substats_required_min`, and `substats_required_all_of`

### 4. Handle `recommended`
- Use still screenshots first, then recording, then memo.
- Do not improve or reinterpret the in-game recommendation.
- If still screenshots are missing, mark the survey note as `Evidence level: provisional`.

### 5. Update the survey note
The survey note should include:
- evidence source and evidence level
- per-slot transcription table for `recommended`
- rationale and exact URLs for `setting1`
- rationale and exact URLs for `setting2`
- explicit `Inference:` notes where needed
- changed-file checklist

### 6. Validate
Run:
- `yamllint presets docs`
- `yq '.preset.slots | keys' presets/<set-id>/*.yml`
- `yq '.preset.slots[] | select(.substats_required_min == null)' presets/<set-id>/*.yml`
- `rg -n '^\s*targets(_ja)?:' presets/<set-id>`

## Final Report

The final report should mention:
- which files changed
- which sources were used
- what is transcription versus authored inference
- what remains uncertain
