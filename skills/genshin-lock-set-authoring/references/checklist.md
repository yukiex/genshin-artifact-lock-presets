# Genshin Lock Set Authoring Checklist

Use this checklist with `SKILL.md` when adding or revising one set.

## 1. Pre-flight

- [ ] I am in the correct repository.
- [ ] I opened `AGENTS.md`.
- [ ] I opened `README.md`.
- [ ] I opened `docs/ui-mapping.md`.
- [ ] I opened `docs/surveys/template.md`.
- [ ] I opened one complete example set and its survey note.

## 2. Minimum source quality

- [ ] I have at least one primary-like or official source for naming or Lock Assist wording.
- [ ] I have at least one EN or CN build source.
- [ ] If I relied mostly on JP sources, I wrote down why.
- [ ] If I made meaningful inference, I left an `Inference:` note.

## 3. Files to create or update

- [ ] `presets/<set-id>/recommended.yml`
- [ ] `presets/<set-id>/setting1.yml`
- [ ] `presets/<set-id>/setting2.yml`
- [ ] `docs/surveys/<set-id>.md`
- [ ] `docs/references/<set-id>/`
- [ ] `README.md` if schema or workflow wording changed
- [ ] `docs/ui-mapping.md` if abbreviations changed

## 4. Recommended transcription gate

- [ ] I have evidence for `recommended` in screenshot, recording, or memo form.
- [ ] I used the strongest available evidence.
- [ ] I transcribed it exactly.
- [ ] If I did not have still screenshots, the survey note says `Evidence level: provisional`.

## 5. YAML checks

- [ ] Top-level key order is correct.
- [ ] All five slots exist.
- [ ] Every slot has `main_allowed`.
- [ ] Every slot has `substats_required_any_of`.
- [ ] Every slot has `substats_required_min`.
- [ ] Every slot has `substats_required_all_of`.
- [ ] If `targets` exists, `targets_ja` also exists.
- [ ] `targets` and `targets_ja` are in the same order.

## 6. Survey note checks

- [ ] The survey note records source URLs.
- [ ] The survey note explains `setting1`.
- [ ] The survey note explains `setting2`.
- [ ] The survey note lists changed files.
- [ ] The survey note records remaining uncertainty.

## 7. Validation

- [ ] I ran `yamllint presets docs` or documented the blocker.
- [ ] I ran `yq '.preset.slots | keys' presets/<set-id>/*.yml`.
- [ ] I ran `yq '.preset.slots[] | select(.substats_required_min == null)' presets/<set-id>/*.yml`.
- [ ] I ran `rg -n '^\s*targets(_ja)?:' presets/<set-id>`.
