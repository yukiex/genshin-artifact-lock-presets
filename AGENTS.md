# Repository Guidelines
This repo curates YAML presets for Genshin Impact's Lock Assist; keep every contribution traceable and easy to verify against in-game behavior.

## Project Structure & Module Organization
- `presets/lock-presets.yml` is the canonical catalog consumed by downstream tooling; keep it synchronized with any per-set edits.
- `presets/<set>/` folders (currently `tsukuyo/` and `tenkyu/`) hold human-friendly files named `recommended.yml`, `setting1.yml`, and `setting2.yml`—copy this pattern when adding sets.
- `docs/ui-mapping.md` defines every abbreviation and mapping between UI toggles and YAML keys, and `README.md` hosts the user-facing explanation; update them whenever wording, abbreviations, or slot semantics change.

## Build, Test, and Development Commands
- `yamllint presets docs` – structural lint; catches indentation drift and stray tabs before commit.
- `yq eval '.preset.slots | keys' presets/tsukuyo/recommended.yml` – confirms each file covers the five expected slots; swap the path for the file you touched.
- `yq eval '.preset.slots[] | select(.substats_required_min == null)' presets -o=json` – should return nothing; use it to guarantee every slot declares a minimum.

## Coding Style & Naming Conventions
Indent with two spaces, keep keys ordered as `version`, `set_*`, then `preset`, and wrap long inline lists so continued lines align under the opening bracket. Directories and files stay lowercase with hyphen-separated folders; slot keys (`flower` … `circlet`) and abbreviations must match the table in `docs/ui-mapping.md`. Use descriptive inline comments sparingly to flag intent (e.g., why a goblet excludes HP%).

## Testing Guidelines
Lint plus semantic review is the minimum bar. After editing an individual preset, mirror the same numbers in `presets/lock-presets.yml`, document at least one manual scenario in the PR (e.g., “Tsukuyo strict goblet keeps only ElementalDMG%”), and attach UI screenshots whenever the change alters visible filters. Treat new abbreviations as schema changes—add them to `docs/ui-mapping.md` and verify they render correctly.

## Commit & Pull Request Guidelines
Follow an imperative Conventional Commit style with the set as the scope (`feat(tsukuyo): tighten ER floor`). Keep commits focused, reference related issues, and list which presets were touched. PRs should describe intent, note the lint/YQ commands you ran, and call out README/docs updates. Request a review before merging to ensure both lenient and strict presets stay consistent.

## Security & Configuration Tips
Strip player UIDs or HoYo account data from screenshots, and avoid committing personal automation scripts or dumps. Keep secrets in local env vars rather than YAML files.
