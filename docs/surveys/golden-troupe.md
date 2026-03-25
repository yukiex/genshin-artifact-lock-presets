# 黄金の劇団 Lock Assist 調査メモ

セット: **黄金の劇団 (Golden Troupe)**

参照日: 2026-03-25

## 1. 推奨設定の根拠
- Evidence source: [ ] 静止スクリーンショット [ ] 画面録画 [ ] 人手メモ
- Evidence level: provisional
- [ ] 静止スクリーンショットがある場合は `docs/references/golden-troupe/` に配置（flower / plume / sands / goblet / circlet）。
- `recommended.yml` は未作成。setting 先行作成のみ実施。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 羽 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 時計 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 杯 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 冠 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |

## 2. Custom Preset 調査
- BWiki のセットページは `黄金剧团` を后台元素战技输出の代表セットとして整理 ([wiki.biligame.com/ys/黄金剧团](https://wiki.biligame.com/ys/%E9%BB%84%E9%87%91%E5%89%A7%E5%9B%A2))。
- Inference: 4 セットの本質は同じでも、`Electro/ATK` 系の off-field skill DPS と、`HP/Hydro` 系の Furina は main stat の分岐が大きい。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 雷寄りの控え元素スキル DPS（フィッシュル、八重神子） | Game8 のセット解説は **フィッシュル / アルベド / 八重神子 / フリーナ / 千織** などの元素スキル主体キャラを列挙 ([game8.jp/genshin/544096](https://game8.jp/genshin/544096))。BWiki の八重神子攻略も `黄金剧团4` を后台八重の通用卒業セットと評価 ([wiki.biligame.com/ys/八重神子/攻略](https://wiki.biligame.com/ys/%E5%85%AB%E9%87%8D%E7%A5%9E%E5%AD%90/%E6%94%BB%E7%95%A5))。→ `ATK% / EM` 砂、`ElectroDMG% / ATK% / EM` 杯、会心2種＋攻撃%＋熟知を優先する。 |
| setting2 | HP スケールの控え元素スキル DPS（フリーナ） | Game8 のフリーナ記事は `黄金4` を基本推奨し、元素スキルが火力源で `HP / 水ダメ / 会心` を重視すると説明 ([game8.jp/genshin/539439](https://game8.jp/genshin/539439))。BWiki の芙宁娜攻略も后台出力の大半が元素スキル由来で `黄金剧团` が最優先とする ([wiki.biligame.com/ys/芙宁娜/攻略](https://wiki.biligame.com/ys/%E8%8A%99%E5%AE%81%E5%A8%9C/%E6%94%BB%E7%95%A5))。→ `HP% / ER%` 砂、`HP% / HydroDMG%` 杯、HP%＋ER＋会心を中心に絞る。 |

## 3. 作業ログ
- setting1 / setting2 を作成
- 推奨設定の証跡待ち
- 構造確認は `yq '.preset.slots | keys' presets/golden-troupe/*.yml` と `yq '.preset.slots[] | select(.substats_required_min == null)' presets/golden-troupe/*.yml` を使用

## 4. 反映済みファイル
- [ ] `presets/golden-troupe/recommended.yml`
- [x] `presets/golden-troupe/setting1.yml`
- [x] `presets/golden-troupe/setting2.yml`

## 5. 備考
- Geo / DEF archetype（千織、アルベド）は有力だが、2 setting 制約では `Electro/ATK` と `HP/Hydro` のほうが差分が明確なため優先度を上げた。
- 3 本目以降の custom preset を増やすなら、Geo / DEF 系を最優先候補にする。
