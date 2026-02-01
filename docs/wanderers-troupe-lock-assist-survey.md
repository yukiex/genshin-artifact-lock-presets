# Wanderer's Troupe Lock Assist 調査メモ

セット: **大地を流浪する楽団 (Wanderer's Troupe)**

## 1. 推奨設定の根拠
- [x] `docs/reference/wanderers-troupe-lock/` に部位ごとのスクリーンショットを配置（flower / plume / sands / goblet / circlet）。
- [x] 下表に、各画像から読み取った主ステータス・サブステ条件・必須ステータスを転記。

| スロット | 画像ファイル | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `スクリーンショット 2026-02-01 082521.png` | HP 固定 | HP% / 攻撃力% / 元素チャージ効率 / 元素熟知 / 会心率 / 会心ダメージ | 会心率, 会心ダメージ |
| 羽 | `スクリーンショット 2026-02-01 082524.png` | 攻撃力 固定 | HP% / 攻撃力% / 元素チャージ効率 / 元素熟知 / 会心率 / 会心ダメージ | 会心率, 会心ダメージ |
| 時計 | `スクリーンショット 2026-02-01 082528.png` | HP% / 元素熟知 / 攻撃力% | HP% / 攻撃力% / 会心率 / 会心ダメージ / 元素チャージ効率 / 元素熟知 | なし |
| 杯 | `スクリーンショット 2026-02-01 082532.png` | HP% / 攻撃力% / 炎元素ダメージ / 草元素ダメージ / 氷元素ダメージ / 元素熟知 | HP% / 攻撃力% / 会心率 / 会心ダメージ / 元素チャージ効率 / 元素熟知 | なし |
| 冠 | `スクリーンショット 2026-02-01 082537.png` | HP% / 会心率 / 元素熟知 / 会心ダメージ | HP% / 攻撃力% / 会心率 / 会心ダメージ / 元素チャージ効率 / 元素熟知 | なし |

- YAML 反映時は `presets/wanderers-troupe/recommended.yml` と `presets/lock-presets.yml` の両方を更新する。
- UI の文言は花/羽のみ「次の追加ステータスのうち、いずれか2個を含む。かつ必須ステータスをすべて含む」。時計/杯/冠は「次の追加ステータスのうち、いずれか2個を含む」。

## 2. Custom Preset 調査
- GameWith のセット解説は「弓/法器の重撃アタッカーに◎」と明記し、甘雨/ティナリ/セトス/クレー/煙緋/バーバラ/アンバー/チャスカをおすすめキャラとして列挙している。
  (https://gamewith.jp/genshin/article/show/152930)
- Game8 でもおすすめキャラにクレー/甘雨/煙緋/リネ/ティナリ/ヌヴィレット/セトス/チャスカを挙げており、重撃アタッカー向けの方向性が一致する。
  (https://game8.jp/genshin/39307)

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 重撃会心型アタッカー（甘雨/煙緋/クレー/リネ/ヌヴィレット） | GameWith の甘雨ビルドでは時の砂は ATK%（溶解なら EM）、杯は氷元素ダメージ、冠は会心系、サブは CR/CD/ATK%/ER/EM と記載。会心軸＋ATK% を中核にしつつ EM も許可する方針に反映。https://gamewith.jp/genshin/article/show/241171 |
| setting2 | 激化重撃型アタッカー（セトス/ティナリ） | GameWith のセトスビルドで時の砂 EM、杯 雷元素ダメージ、冠 会心、サブは CR/CD/EM/ER/ATK% と明記。EM 必須＋激化向けの構成に反映。https://gamewith.jp/genshin/article/show/420428 |

### 調査の観点
1. **主な対象キャラクター**: 攻略サイトの「おすすめキャラ」欄を確認。
2. **アーキタイプの違い**: 重撃会心型（ATK/会心軸）と激化型（EM軸）で分離。
3. **ステータス優先順位**: 会心/攻撃%/熟知/元チャの優先度をガイドに合わせて設定。
4. **参考 URL**: Game8 / GameWith を使用。

## 3. 作業ログ
- リント: `yamllint presets docs`
- スロット確認: `yq '.preset.slots | keys' presets/wanderers-troupe/*.yml`
- 必須サブステ確認: `yq '.preset.slots[] | select(.substats_required_min == null)' presets/wanderers-troupe/*.yml`

## 4. 反映済みファイル（作業完了後に記入）
- [x] `presets/wanderers-troupe/recommended.yml`
- [x] `presets/wanderers-troupe/setting1.yml`
- [x] `presets/wanderers-troupe/setting2.yml`
- [x] `presets/lock-presets.yml`
- [ ] `docs/ui-mapping.md`（新しい略語や条件を追加した場合）

## 5. 備考・注意事項
- 推奨設定（recommended）はスクリーンショットから反映済み。
- 必須ステータス（黄色ハイライト）と候補ステータス（いずれかN個）の区別を厳密に記録する。
