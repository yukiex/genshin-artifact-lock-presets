# [Set Name] Lock Assist 調査メモ

セット: **[日本語セット名] ([English Set Name])**

## 1. 推奨設定の根拠
- [ ] `docs/reference/[set-id]-lock/` に部位ごとのスクリーンショットを配置（flower / plume / sands / goblet / circlet）。
- [ ] 下表に、各画像から読み取った主ステータス・サブステ条件・必須ステータスを転記。

| スロット | 画像ファイル | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `スクリーンショット YYYY-MM-DD hhmmss.png` | HP | [例: 攻撃力% / 会心率 / 会心ダメージ] | [例: 会心率, 会心ダメージ] |
| 羽 | `スクリーンショット YYYY-MM-DD hhmmss.png` | 攻撃力 | [同上] | [同上] |
| 時計 | `スクリーンショット YYYY-MM-DD hhmmss.png` | [例: 攻撃力%] | [例: 会心率 / 会心ダメージ] | [同上] |
| 杯 | `スクリーンショット YYYY-MM-DD hhmmss.png` | [例: 炎元素ダメージ / 攻撃力%] | [同上] | [同上] |
| 冠 | `スクリーンショット YYYY-MM-DD hhmmss.png` | [例: 会心率 / 会心ダメージ] | [同上] | [同上] |

- YAML 反映時は `presets/[set-id]/recommended.yml` と `presets/lock-presets.yml` の両方を更新する。
- UI の文言（「次の追加ステータスのうち、いずれかN個を含む。かつ必須ステータスをすべて含む」など）を正確に記録し、`substats_required_any_of`、`substats_required_min`、`substats_required_all_of` に適切にマッピングする。

## 2. Custom Preset 調査
- `setting1` / `setting2` は厳しさではなく**異なるキャラクタータイプ**を表す。攻略サイト・ビルドガイドなど、根拠となる URL とポイントを以下に整理する。
- 各 setting は「このセットをどういうアーキタイプのキャラに使うか」を明確にし、対象キャラクターと主ステ・サブステの優先順位を調査結果に基づいて決定する。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | [例: 落下攻撃メインのアタッカー（魈・嘉明・ヴァレサ）] | [Game8/Gamerch/神ゲー攻略などの URL と要約] → [メイン・サブステの方針を記述] |
| setting2 | [例: 閑雲サポート込みの疑似落下アタッカー（フリーナ、ナヴィア等）] | [同上] → [メイン・サブステの方針を記述] |

### 調査の観点
1. **主な対象キャラクター**: 攻略サイトの「おすすめキャラ」「相性の良いキャラ」欄を確認。
2. **アーキタイプの違い**: セット効果を最大限活用できるビルドパターン（例: オンフィールドDPS vs サポーター、元素反応ドライバー vs サブアタッカー）。
3. **ステータス優先順位**: 各アーキタイプで重視されるメイン/サブステ（会心/攻撃%/熟知/元チャなど）。
4. **参考 URL**: Game8、GameWith、神ゲー攻略、Gamerch など日本語攻略サイトのセット解説ページ。

### 記載例（参考）
```
Game8 は「落下攻撃主体のアタッカーと相性が良い」として魈/嘉明/ヴァレサを挙げ、スタック維持の立ち回り例を掲載 ([game8.jp/genshin/676659#hl_4](https://game8.jp/genshin/676659#hl_4))。Gamerch も同3名を最適キャラに記載し、落下攻撃・重撃・元素スキルでスタックを稼ぐ運用を推奨 ([gamerch.com/genshinwiki/910745](https://gamerch.com/genshinwiki/910745))。→ 会心2種＋攻撃%を軸に、砂はATK%固定、杯は対応元素/ATK%。
```

## 3. 作業ログ
- リント: `yamllint presets docs`
- スロット確認: `yq '.preset.slots | keys' presets/[set-id]/*.yml`
- 必須サブステ確認: `yq '.preset.slots[] | select(.substats_required_min == null)' presets/[set-id]/*.yml`

## 4. 反映済みファイル（作業完了後に記入）
- [ ] `presets/[set-id]/recommended.yml`
- [ ] `presets/[set-id]/setting1.yml`
- [ ] `presets/[set-id]/setting2.yml`
- [ ] `presets/lock-presets.yml`
- [ ] `docs/ui-mapping.md`（新しい略語や条件を追加した場合）

## 5. 備考・注意事項
- スクリーンショットからステータス名を転記する際は、ゲーム内表記と `docs/ui-mapping.md` の略語を正確に対応させる。
- 必須ステータス（黄色ハイライト）と候補ステータス（いずれかN個）の区別を明確にする。
- Custom Preset (setting1/2) は推奨設定と併用することを前提とし、特定のアーキタイプに特化した追加フィルターとして設計する。
