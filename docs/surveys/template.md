# [Set Name] Lock Assist 調査メモ

セット: **[日本語セット名] ([English Set Name])**

## 1. 推奨設定の方針
- `recommended.yml`: 作成する | 省略する
- 省略理由: [例: 静止スクリーンショットがなく、custom settings の方が保守しやすいため]

作成する場合のみ、以下を埋める。

- Evidence source: [ ] 静止スクリーンショット [ ] 画面録画 [ ] 人手メモ
- Evidence level: final | provisional
- [ ] 静止スクリーンショットがある場合は `docs/references/[set-id]/` に配置（`flower.png` / `plume.png` / `sands.png` / `goblet.png` / `circlet.png`）。
- [ ] 下表に、採用した証跡から読み取った主ステータス・サブステ条件・必須ステータスを転記。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `flower.png` | HP | [例: 攻撃力% / 会心率 / 会心ダメージ] | [例: 会心率, 会心ダメージ] |
| 羽 | `plume.png` | 攻撃力 | [同上] | [同上] |
| 時計 | `sands.png` | [例: 攻撃力%] | [例: 会心率 / 会心ダメージ] | [同上] |
| 杯 | `goblet.png` | [例: 炎元素ダメージ / 攻撃力%] | [同上] | [同上] |
| 冠 | `circlet.png` | [例: 会心率 / 会心ダメージ] | [同上] | [同上] |

- YAML 反映時は `presets/[set-id]/recommended.yml` を更新する。省略する場合はこの項目を消す。
- 静止スクリーンショット以外を使う場合は `Evidence level: provisional` を明記する。
- UI 文言をそのまま記録し、`main_allowed`、`substats_required_any_of`、`substats_required_min`、`substats_required_all_of` に正しく落とし込む。

## 2. Custom Preset 調査
- `setting1` / `setting2` は厳しさではなく異なるキャラクタータイプを表す。
- 必要なら `setting3` を使って、3つ目の実用アーキタイプを分離してよい。
- 対象キャラは `targets` と `targets_ja` の両方で記録し、順序を一致させる。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | [例: 落下攻撃メインのアタッカー（Xiao / 魈、Gaming / 嘉明）] | [URL と要約] → [主ステ・サブステの方針] |
| setting2 | [例: HP スケールの控えサポート（Furina / フリーナ）] | [URL と要約] → [主ステ・サブステの方針] |
| setting3 | [例: DEF スケールの控えサブアタッカー（Linnea / リンネア）] | [URL と要約] → [主ステ・サブステの方針] |

## 3. 作業ログ
- リント: `yamllint presets docs`
- スロット確認: `yq '.preset.slots | keys' presets/[set-id]/*.yml`
- 必須サブステ確認: `yq '.preset.slots[] | select(.substats_required_min == null)' presets/[set-id]/*.yml`
- target 対応確認: `rg -n '^\s*targets(_ja)?:' presets/[set-id]`

## 4. 反映済みファイル
- [ ] `presets/[set-id]/recommended.yml`（作成する場合）
- [ ] `presets/[set-id]/setting1.yml`
- [ ] `presets/[set-id]/setting2.yml`
- [ ] `presets/[set-id]/setting3.yml`（必要なら）
- [ ] `docs/ui-mapping.md`（必要なら）

## 5. 備考
- `recommended` は任意。作る場合は転記に徹し、custom settings は authored rule として分ける。
- 不確かな推論を入れた場合は `Inference:` として明記する。
