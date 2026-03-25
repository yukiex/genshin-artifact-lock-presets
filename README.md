# Genshin Artifact Lock Presets

Curated YAML presets for Genshin Impact's Artifact Auto-Lock / Lock Assist.

This repository stores one directory per artifact set under `presets/<set-id>/`. Each set may contain:

- `recommended.yml` — a direct transcription of the in-game recommended rule set
- `setting1.yml` — a custom preset for the primary authored archetype
- `setting2.yml` — a custom preset for a second meaningful archetype

There is no aggregate catalog file anymore. The per-set YAML files are the source of truth.

## Current Coverage

| Set ID | Japanese Name | Recommended | Custom presets |
| --- | --- | --- | --- |
| `moonweaver` | 月を紡ぐ夜の歌 | yes | yes |
| `night-of-the-sky` | 天穹の顕現せし夜 | yes | yes |
| `finale-of-the-deep` | 深廊の終曲 | yes | yes |
| `song-of-days-past` | 長き夜の誓い | yes | yes |
| `obsidian-codex` | 黒曜の秘典 | yes | yes |
| `ashen-hero-scroll` | 灰燼の都に立つ英雄の絵巻 | yes | yes |
| `wanderers-troupe` | 大地を流浪する楽団 | yes | yes |
| `tenacity-of-the-millelith` | 千岩牢固 | no | partial |
| `aubade-of-morningstar-and-moon` | 暁の星と月の歌 | no | yes |
| `a-day-carved-from-rising-winds` | 風立ちの日 | no | yes |
| `deepwood-memories` | 深林の記憶 | no | yes |
| `gilded-dreams` | 金メッキの夢 | no | yes |
| `marechaussee-hunter` | ファントムハンター | no | yes |
| `golden-troupe` | 黄金の劇団 | no | yes |

The planned / in-progress target list lives in `docs/target-sets.md`.

## Repository Layout

```text
genshin-artifact-lock-presets/
├─ README.md
├─ AGENTS.md
├─ docs/
│  ├─ ui-mapping.md
│  ├─ target-sets.md
│  ├─ surveys/
│  │  ├─ template.md
│  │  ├─ moonweaver.md
│  │  └─ ...
│  └─ references/
│     ├─ moonweaver/
│     │  ├─ flower.png
│     │  ├─ plume.png
│     │  ├─ sands.png
│     │  ├─ goblet.png
│     │  └─ circlet.png
│     └─ ...
└─ presets/
   ├─ moonweaver/
   │  ├─ recommended.yml
   │  ├─ setting1.yml
   │  └─ setting2.yml
   └─ ...
```

## YAML Schema

```yaml
version: 1
set_id: moonweaver
set_name_ja: 月を紡ぐ夜の歌
preset:
  key: recommended | setting1 | setting2
  name: Recommended (baseline)
  nickname_en: Moonweaver
  intent: support_offfield
  targets: [Xingqiu, Yelan]
  targets_ja: [行秋, 夜蘭]
  slots:
    flower:
      main_allowed: [HP]
      substats_required_any_of: [CR, CD, ER, EM]
      substats_required_min: 2
      substats_required_all_of: [ER]
```

### Field notes

- `targets` is an English identifier list for readability in code and diffs.
- `targets_ja` is the Japanese display-name list in the same order as `targets`.
- `recommended` should be transcription, not theorycraft.
- `setting1` and `setting2` should be different archetypes, not strict / lenient copies.

## Quick Start

1. Open a per-set YAML file, for example `presets/night-of-the-sky/setting2.yml`.
2. In the in-game Lock Assist UI, pick the matching artifact set.
3. For each slot:
   - check the substats listed in `substats_required_any_of`
   - set the threshold to `substats_required_min`
   - require every stat listed in `substats_required_all_of`
   - use `main_allowed` only as a hint for filtering main stats
4. Keep `recommended` enabled when it exists, then layer `setting1` or `setting2` on top if you want a narrower filter.

## Research and Evidence Files

- Survey notes live under `docs/surveys/`.
- Reference screenshots live under `docs/references/<set-id>/`.
- Screenshot filenames are standardized as `flower.png`, `plume.png`, `sands.png`, `goblet.png`, and `circlet.png`.
- New sets should start from `docs/surveys/template.md`.

## Validation Commands

- `yamllint presets docs`
- `yq '.preset.slots | keys' presets/<set-id>/recommended.yml`
- `yq '.preset.slots[] | select(.substats_required_min == null)' presets/<set-id>/*.yml`
- `rg -n '^\s*targets(_ja)?:' presets/<set-id>`

## Contribution Notes

- Keep YAML indentation at two spaces.
- Keep top-level key order as `version`, `set_*`, then `preset`.
- If `targets` exists, `targets_ja` must also exist and stay in the same order.
- Update `docs/ui-mapping.md` if you introduce new abbreviations.
- Update the matching survey note whenever preset logic changes.

## Disclaimer

This repository is unofficial and not affiliated with HoYoVerse. Artifact evaluation changes as new characters, weapons, and teams appear, so authored presets should be treated as maintained heuristics rather than absolute truth.
