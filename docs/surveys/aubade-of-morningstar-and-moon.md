# 暁の星と月の歌 Lock Assist 調査メモ

セット: **暁の星と月の歌 (Aubade of Morningstar and Moon)**

## 1. セット識別

- `set_id`: `aubade-of-morningstar-and-moon`
- 日本語名: 暁の星と月の歌
- 英語名: Aubade of Morningstar and Moon
- 中国語名: 晨星与月的晓歌
- 命名判断: README の既存カタログにある英語名ベースの lowercase / hyphen 形式を維持。

## 2. Source Log

| Kind | Page title | URL | Lang | Accessed | Used for | Evidence type |
| --- | --- | --- | --- | --- | --- | --- |
| Set data | Aubade of Morningstar and Moon | https://genshin-impact.fandom.com/wiki/Aubade_of_Morningstar_and_Moon | EN | 2026-05-04 | 英語名、セット効果、部位名の確認 | supporting |
| Guide-ZH | 晨星与月的晓歌 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E6%99%A8%E6%98%9F%E4%B8%8E%E6%9C%88%E7%9A%84%E6%99%93%E6%AD%8C | ZH | 2026-05-04 | 中国語名、セット効果、月反応向け用途 | direct |
| Guide-EN | Columbina Quick Guide - KQM | https://keqingmains.com/q/columbina-quickguide/ | EN | 2026-05-04 | Columbina の HP/ER/会心方針、4pc Aubade の採用理由 | direct |
| Guide-EN | Linnea Quick Guide - KQM | https://keqingmains.com/q/linnea-quickguide/ | EN | 2026-05-04 | Linnea の DEF/会心方針、4pc Aubade の採用理由、ER 要求 | direct |
| Guide-ZH | 哥伦比娅/攻略 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E5%93%A5%E4%BC%A6%E6%AF%94%E5%A8%85/%E6%94%BB%E7%95%A5 | ZH | 2026-05-04 | HP% / ER% / 会心 / HP 実数 / EM の優先度 | direct |
| Guide-ZH | 伊涅芙/攻略 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E4%BC%8A%E6%B6%85%E8%8A%99/%E6%94%BB%E7%95%A5 | ZH | 2026-05-04 | Ineffa の ATK% / EM / 会心方針と 4pc Aubade 採用 | direct |
| Guide-ZH | 莉奈娅 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E8%8E%89%E5%A5%88%E5%A8%85 | ZH | 2026-05-04 | Linnea の中国語名、岩元素、月兆、実装日、DEF 基礎値確認 | supporting |

## 3. 推奨設定の方針

- `recommended.yml` は作成しない。
- 理由: 静止スクリーンショットがなく、人手メモから暫定転記するとメンテナンス負荷に対して信頼度が低い。現方針では custom settings を主データとして保守する。

## 4. Custom Preset 調査

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | Lunar-Charged Sub DPS（Ineffa） | BWiki Ineffa は 4pc Aubade を控え火力向けの卒業聖遺物とし、主ステを ATK% / EM、杯を ATK% / EM、冠を会心、サブを会心・ATK%・EM 優先とする。Aubade の 2 セット EM と 4 セット月反応ダメージ強化が噛み合う。 |
| setting2 | Lunar Reaction Sub DPS（Columbina） | KQM Columbina は Ascendant Gleam チームで 4pc Aubade を off-field personal damage の最良候補とし、HP% / HP% / CRIT が基本、ER 要求が高いと説明する。BWiki Columbina も HP% / ER%、会心、HP 実数、EM を候補に入れる。 |
| setting3 | Lunar-Crystallize Sub DPS（Linnea） | KQM Linnea は Lunar-Crystallize 向けの控え火力/回復/支援キャラとして 4pc Aubade を有効候補に挙げ、主ステは DEF% / DEF% / CRIT 以上 DEF%、サブは ER 必要量まで、会心、DEF%、EM の順に整理する。BWiki Linnea は岩元素・月兆キャラで、DEF 基礎値が高いことを確認できる。 |

Inference: `setting1` は Ineffa の ATK/EM スケールに寄せ、`ElectroDMG%` に加えて `ATK%` と `EM` 杯を許可する。`setting2` は Columbina の HP/ER 要求を優先し、HydroDMG% と EM は実物比較用の代替として許可する。`setting3` は Linnea 専用に DEF% 砂/杯、会心または DEF% 冠へ絞り、サブステは `CR/CD/DEF%/ER/EM` とする。

Rejected: Linnea 向けに `GeoDMG%` 杯は採用しない。KQM が DEF% 杯を強く推奨し、回復・EM バフ・月結晶基礎ダメージ補正も DEF 依存と説明しているため。

## 5. 作業ログ

- `recommended.yml` を省略する方針に変更。
- `setting1.yml` / `setting2.yml` を現行 KQM/BWiki の対象キャラと主ステ方針に合わせて更新。
- `setting3.yml` を追加し、リンネア専用の DEF/会心型 preset とした。

## 6. 反映済みファイル

- [ ] `presets/aubade-of-morningstar-and-moon/recommended.yml`（省略）
- [x] `presets/aubade-of-morningstar-and-moon/setting1.yml`
- [x] `presets/aubade-of-morningstar-and-moon/setting2.yml`
- [x] `presets/aubade-of-morningstar-and-moon/setting3.yml`
- [ ] `docs/ui-mapping.md`（新略語なし）

## 7. 備考

- 今後、ゲーム内 recommended の静止スクリーンショットが揃った場合のみ `recommended.yml` を復活させる。
