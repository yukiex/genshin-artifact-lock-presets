# 影に沈む幻 Lock Assist 調査メモ

セット: **影に沈む幻 (Disenchantment in Deep Shadow)**

## 1. セット識別

- `set_id`: `disenchantment-in-deep-shadow`
- 日本語名: 影に沈む幻
- 英語名: Disenchantment in Deep Shadow
- 中国語名: 影中沉凝的幻灭
- 命名判断: 公式英語表記を省略せず lowercase / hyphen 形式へ変換。

## 2. Source Log

| Kind | Page title | URL | Lang | Accessed | Used for | Evidence type |
| --- | --- | --- | --- | --- | --- | --- |
| Official | New Artifacts: Celestial Gift & Disenchantment in Deep Shadow | https://www.hoyolab.com/article/45163741 | EN | 2026-07-20 | 英語名、現行セット効果 | direct |
| Guide-JA | 影に沈む幻の入手方法と装備おすすめキャラ | https://game8.jp/genshin/783865 | JA | 2026-07-20 | 日本語名、星電導向け4キャラ、現行セット効果 | direct |
| Guide-ZH | 影中沉凝的幻灭 - 原神WIKI_BWIKI | https://wiki.biligame.com/ys/%E5%BD%B1%E4%B8%AD%E6%B2%89%E5%87%9D%E7%9A%84%E5%B9%BB%E7%81%AD | ZH | 2026-07-20 | 中国語名、星超導向け4キャラ | direct |
| Guide-EN | Sandrone Quick Guide - KQM | https://keqingmains.com/q/sandrone-quickguide/ | EN | 2026-07-20 | サンドローネの ATK% / ATK% / CRIT とサブステ優先度 | direct |
| Guide-EN | Best Teams for Yae Miko - GameWith | https://gamewith.net/genshin-impact/article/show/38768 | EN | 2026-07-20 | 八重神子の星電導編成での ATK% / ATK% / CRIT | direct |
| Guide-EN | Cyno Guide and Best Builds - Icy Veins | https://www.icy-veins.com/genshin-impact/cyno-guide-best-builds | EN | 2026-07-20 | セノの星電導向け ATK% / EM と会心方針 | direct |
| Guide-EN | Wriothesley Build Guide - Mobalytics | https://mobalytics.gg/genshin-impact/characters/wriothesley-build-guide | EN | 2026-07-20 | リオセスリの星電導向け ATK% / ATK% / CRIT | direct |
| Guide-EN | Disenchantment in Deep Shadow Set Guide - GameWith | https://gamewith.net/genshin-impact/article/show/75662 | EN | 2026-07-20 | 物理超電導型のエウルア適性 | supporting |

## 3. 推奨設定の方針

- `recommended.yml` は作成しない。
- 理由: ゲーム内 Lock Assist の静止スクリーンショットがなく、星電導追加後の custom settings を直接保守する方が明確なため。

## 4. Custom Preset 調査

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | Stellar-Conduct ATK DPS（Sandrone / サンドローネ、YaeMiko / 八重神子、Wriothesley / リオセスリ） | KQM / GameWith / Mobalytics は星電導運用で ATK% / ATK% / CRIT を推奨する。直撃型の星電導ダメージでは ATK% 杯を優先しつつ、八重神子の通常雷元素直傷を拾う候補として ElectroDMG% 杯も許可する。 |
| setting2 | Stellar-Conduct EM/ATK DPS（Cyno / セノ） | Icy Veins は星電導型を最有力とし、武器・編成に応じて ATK% / EM の砂と杯、会心冠を推奨する。ER は現行星電導編成では原則不要。 |
| setting3 | Physical Superconduct DPS（Eula / エウルア） | GameWith は超電導状態への会心率+16%と攻撃力+18%を活かす物理アタッカー候補としてエウルアを挙げる。ATK% 砂、物理 / ATK% 杯、会心冠とする。 |

Inference: 星電導の直撃型3キャラは ATK% / ATK% / CRIT が共通するため `setting1` にまとめた。セノは EM を主ステに選ぶ武器・編成があるため `setting2` に分離した。旧来の超電導も4セット効果の対象なので、物理型を `setting3` として残す。

Rejected: 星電導の主力ダメージへ元素ダメージ杯が乗らないため、CryoDMG% 杯は汎用候補として混ぜない。ElectroDMG% 杯は八重神子の通常雷元素直傷に有効なので `setting1` に限って残す。通常編成向けの元素杯は他セットで管理する。

## 5. 作業ログ

- Luna VIII の星電導追加後の効果と対象キャラを基準に作成。
- ATK 直撃型、EM / ATK 型、物理超電導型の3アーキタイプを分離。

## 6. 反映済みファイル

- [ ] `presets/disenchantment-in-deep-shadow/recommended.yml`（省略）
- [x] `presets/disenchantment-in-deep-shadow/setting1.yml`
- [x] `presets/disenchantment-in-deep-shadow/setting2.yml`
- [x] `presets/disenchantment-in-deep-shadow/setting3.yml`
- [ ] `docs/ui-mapping.md`（新略語なし）

## 7. 備考

- 星電導の追加キャラや計算仕様が更新された場合は、対象キャラと ATK / EM 比重を再確認する。
