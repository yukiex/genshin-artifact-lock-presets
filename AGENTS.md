# Repository Guidelines
This repo curates YAML presets for Genshin Impact's Lock Assist; keep every contribution traceable and easy to verify against in-game behavior.

## Project Structure & Module Organization
- `presets/lock-presets.yml` is the canonical catalog consumed by downstream tooling; keep it synchronized with any per-set edits.
- `presets/<set>/` folders (currently `tsukuyo/`, `tenkyu/`, `kokuyo-hiten/`, `haijin-eiyu-emaki/`) hold human-friendly files named `recommended.yml`, `setting1.yml`, and `setting2.yml`—copy this pattern when adding sets.
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

## 新規セット追加ワークフロー (Adding New Sets)

新しいセットを追加する際は `docs/lock-assist-survey-template.md` をコピーして `docs/[set-id]-lock-assist-survey.md` を作成し、以下の手順で進める。

### 1. 準備 (AI)
- 攻略サイト（海外）などを参考にして、セットの内部ID（フォルダ名・`lock-presets.yml` で使う `id`）を決定
- `docs/reference/[set-id]-lock/` フォルダを作成
- 調査メモファイル `docs/[set-id]-lock-assist-survey.md` をテンプレートから作成

### 2. Custom Settings の調査と作成 (AI)
- `setting1` / `setting2` は「厳しさ」ではなく**異なるキャラクタータイプ**を表す
- 攻略サイト（Game8/GameWith/神ゲー攻略/Gamerch）でセット解説を調査：
  - おすすめキャラクター一覧
  - ビルドタイプ別の推奨ステータス（例: オンフィールドDPS、サポーター、元素反応ドライバー）
- 調査結果を元に、異なるアーキタイプ向けの2つの設定を作成し、調査メモに根拠URLを明記
- **運用前提**: 推奨（Recommended）を常に有効化し、必要に応じて setting1/2 を追加でオン

### 3. スクリーンショット撮影 (人間)
- ゲーム内「セットロック設定」画面で推奨設定を開く
- 各部位（flower/plume/sands/goblet/circlet）のスクリーンショットを `docs/reference/[set-id]-lock/` に保存

### 4. 推奨設定の調査と転記 (AI)
1. スクリーンショットから主ステータス・サブステ候補・必須ステータスを読み取り、調査メモの表に記入
2. UI の文言（「いずれかN個を含む」「必須ステータスをすべて含む」）を正確に記録
3. 読み取った値を `presets/[set-id]/recommended.yml` に反映：
   - 主ステータス → `main_allowed`
   - 必須ステータス（黄色ハイライト） → `substats_required_all_of`
   - サブステ候補 → `substats_required_any_of` と `substats_required_min`
4. `presets/lock-presets.yml` の対応セクションも同じ値に更新

### 5. ドキュメント更新 (AI)
- 新しい略語やフィールドを導入した場合は `docs/ui-mapping.md` を更新
- `README.md` のスキーマ説明も必要に応じて追加

### 6. 検証 (AI)
- `yamllint presets docs` でリント
- `yq '.preset.slots | keys' presets/[set-id]/*.yml` で5スロット揃っているか確認
- `yq '.preset.slots[] | select(.substats_required_min == null)' presets/[set-id]/*.yml` が空であることを確認
- 調査メモの「反映済みファイル」チェックリストを更新
