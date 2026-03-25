# Tenacity of the Millelith Lock Assist 調査メモ

セット: **千岩牢固 (Tenacity of the Millelith)**

## 0. セットID方針
- 候補 `set_id`: `tenacity-of-the-millelith`
- 理由:
  - 既存リポジトリは `wanderers-troupe` のように旧来セットで公式英語名ベースの ID も使っている。
  - `千岩牢固` は `Tenacity of the Millelith` が英語圏で十分定着しており、JP ローマ字化より誤読が少ない。
  - `millelith` 単独よりも公式セット名全体のほうが検索性と可読性が高い。
- 2026-03-26 時点で `tenacity-of-the-millelith` を採用済み。

## 1. ソースログ

| Kind | Page title | URL | Lang | Accessed | Used for | Evidence type |
| --- | --- | --- | --- | --- | --- | --- |
| Guide | Zhongli Guide: 岩王帝君 - KQM | https://keqingmains.com/zhongli/ | EN | 2026-03-24 | 千岩4がチームDPS目的で有力、Favonius 採用時に CR が実用値になる点の確認 | direct |
| Guide | Kokomi Quick Guide - KQM | https://keqingmains.com/q/kokomi-quickguide/ | EN | 2026-03-24 | オフフィールド支援型の HP/ER/Healing 軸と千岩4適性の確認 | direct |
| Guide | 千岩牢固 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E5%8D%83%E5%B2%A9%E7%89%A2%E5%9B%BA | ZH | 2026-03-24 | セット効果、代表的な継続命中キャラ、盾補助向けという位置付けの確認 | direct |
| Guide | 钟离/攻略 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E9%92%9F%E7%A6%BB/%E6%94%BB%E7%95%A5 | ZH | 2026-03-24 | HP/HP/HP、Favonius 時の CR 要件、千岩4が純盾補助の卒業セットである点の確認 | direct |
| Guide | 莱依拉/攻略 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E8%8E%B1%E4%BE%9D%E6%8B%89/%E6%94%BB%E7%95%A5 | ZH | 2026-03-24 | HP/HP/HP、ER が有効、Favonius 時に CR が必要という補助軸の確認 | direct |
| Guide | 〖原神〗千岩牢固の効果とおすすめキャラ｜ゲームエイト | https://game8.jp/genshin/383128 | JA | 2026-03-24 | 継続命中型スキル持ち全般に適性があるという日本語圏の整合確認 | supporting |

## 2. 推奨設定の根拠
- Evidence source: `(未取得)`
- Evidence level: `(未確定)`
- [ ] `docs/references/tenacity-of-the-millelith/` に部位ごとのスクリーンショットを配置（flower / plume / sands / goblet / circlet）。
- [ ] 下表に、採用した証跡から読み取った主ステータス・サブステ条件・必須ステータスを転記。
- 現時点では証跡未取得のため、`recommended` は未確定。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 | 必須ステータス | UI文言 |
| --- | --- | --- | --- | --- | --- |
| 花 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 羽 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 時計 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 杯 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 冠 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |

## 3. Custom Preset 調査

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | Shield Buffer (HP stack) - `Zhongli`, `Layla`, `Kirara` | KQM Zhongli は千岩4を「team damage in most cases」で評価し、Favonius では CR が実用値になると説明。BWiki 鍾離/攻略 は HP/HP/HP としつつ、`西风长枪` 採用時の CR を要求。BWiki 莱依拉/攻略 も HP/HP/HP を基本に ER を有効詞条、Favonius 時に CR を要求。→ `HP%` 主軸、`CR/ER` を補助にした盾サポ特化案が妥当。 |
| setting2 | Off-Field Healer Buffer - `Kokomi` | KQM Kokomi Quick Guide はオフフィールド支援で `HP% or ER / HP% / Healing Bonus`、優先度 `ER until requirement > HP%` とし、千岩4を有力候補に挙げる。Game8 でも珊瑚宮心海を千岩4適性キャラに列挙。→ `ER/HP%/Healing%` を許可し、サブステは `ER/HP%` 軸の回復支援型が差別化しやすい。 |

### setting1 草案
- 目的: シールド量と千岩4維持を優先する HP 支援
- 主ステ候補:
  - sands: `HP%`
  - goblet: `HP%`
  - circlet: `HP%`, `CR`
- サブステ候補: `HP%`, `ER`, `CR`
- Inference: Favonius 利用の現実性を残すため、冠は `CR` を許可するが、主軸は `HP%` のままにする。

### setting2 草案
- 目的: スキル設置型ヒーラーが千岩4を維持しつつ回復とバフを供給する運用
- 主ステ候補:
  - sands: `ER%`, `HP%`
  - goblet: `HP%`
  - circlet: `Healing%`, `HP%`
- サブステ候補: `ER`, `HP%`
- Inference: Kokomi は会心を持たないため、setting1 の Favonius 想定と明確に切り分けて `CR` を含めない方針が自然。

## 4. 作業ログ
- 未着手: `recommended.yml` 転記
- 作成済み: `presets/tenacity-of-the-millelith/setting1.yml`
- 作成済み: `presets/tenacity-of-the-millelith/setting2.yml`

## 5. 反映済みファイル
- [ ] `presets/tenacity-of-the-millelith/recommended.yml`
- [x] `presets/tenacity-of-the-millelith/setting1.yml`
- [x] `presets/tenacity-of-the-millelith/setting2.yml`
- [ ] `README.md`
- [ ] `docs/ui-mapping.md`
