# Repository Guidelines

This repository curates YAML presets for Genshin Impact's Lock Assist. Keep every change traceable, reviewable, and easy to reconcile with in-game behavior.

## Project Structure & Module Organization
- `presets/<set-id>/` is the source of truth. Each set directory may contain `recommended.yml`, `setting1.yml`, and `setting2.yml`.
- `docs/surveys/<set-id>.md` stores the research note, evidence trail, and authored rationale for one set.
- `docs/references/<set-id>/` stores reference screenshots or placeholder files. Use the canonical screenshot names `flower.png`, `plume.png`, `sands.png`, `goblet.png`, and `circlet.png` when images exist.
- `docs/ui-mapping.md` defines the schema abbreviations and UI mapping rules.
- `docs/target-sets.md` tracks backlog or partially authored sets.

## Build, Test, and Development Commands
- `yamllint presets docs` — structural lint.
- `yq '.preset.slots | keys' presets/moonweaver/recommended.yml` — confirm the expected five slots.
- `yq '.preset.slots[] | select(.substats_required_min == null)' presets/moonweaver/*.yml` — should print nothing.
- `rg -n '^\s*targets(_ja)?:' presets/<set-id>` — quick check that `targets` and `targets_ja` are both present when needed.

## Coding Style & Naming Conventions
- Use two-space indentation.
- Keep top-level key order as `version`, `set_*`, then `preset`.
- Directory and file names must be lowercase ASCII with hyphen-separated words.
- `targets` is the English identifier list. `targets_ja` is the Japanese display-name list in the same order.
- Add comments sparingly and only when a rule would otherwise be hard to infer from the YAML itself.

## Testing Guidelines
- Lint plus semantic review is the minimum bar.
- After editing a preset, validate the five-slot structure and confirm `substats_required_min` is present everywhere.
- If the change affects `recommended`, update the matching survey note and keep the evidence trail intact.
- If the change affects `targets`, update both `targets` and `targets_ja` together.

## Commit & Pull Request Guidelines
- Use imperative Conventional Commit messages.
- Keep commits focused and list which sets changed.
- Substantial changes should go through a PR and GitHub Copilot review.
- PRs should state the change goal, what reviewers should focus on, known tradeoffs, and any intentionally preserved behavior.

## Security & Configuration Tips
- Remove player UIDs or account-identifying data from screenshots before committing them.
- Do not commit private tooling or personal automation artifacts.

## 新規セット追加ワークフロー

新しいセットを追加する際は `docs/surveys/template.md` をコピーして `docs/surveys/<set-id>.md` を作成し、以下の手順で進める。

### 1. 準備
- 攻略サイトや公式表記をもとに `set_id` を決める。
- `docs/references/<set-id>/` を作成する。
- 調査メモ `docs/surveys/<set-id>.md` をテンプレートから作成する。

### 2. Custom Settings の調査と作成
- `setting1` / `setting2` は厳しさ違いではなく異なるアーキタイプにする。
- 攻略サイト・理論系ガイド・BWiki などを見て、対象キャラと主ステ / サブステ方針を整理する。
- `targets` と `targets_ja` を同じ順序で書く。
- `setting1` / `setting2` はスクリーンショット待ちをせず先行作成してよい。

### 3. 推奨設定の証跡収集
- `recommended` の証跡優先順位は、静止スクリーンショット → 画面録画 → 人手メモ。
- 静止画がある場合は `docs/references/<set-id>/flower.png` などの canonical name にそろえる。
- 静止画がなくても `recommended.yml` を作ることはできるが、その場合は survey note に `Evidence level: provisional` を明記する。

### 4. 推奨設定の転記
- 証跡から主ステータス、候補サブステ、必須サブステを読み取る。
- UI 文言を YAML に正確に対応させる。
- `recommended.yml` は転記に徹し、改善案は `setting1` / `setting2` に分離する。

### 5. ドキュメント更新
- 新しい略語が必要なら `docs/ui-mapping.md` を更新する。
- schema や workflow の説明が変わるなら `README.md` も更新する。

### 6. 検証
- `yamllint presets docs`
- `yq '.preset.slots | keys' presets/<set-id>/*.yml`
- `yq '.preset.slots[] | select(.substats_required_min == null)' presets/<set-id>/*.yml`
- `rg -n '^\s*targets(_ja)?:' presets/<set-id>`
