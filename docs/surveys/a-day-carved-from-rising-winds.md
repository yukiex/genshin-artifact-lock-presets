# 風立ちの日 Lock Assist 調査メモ

セット: **風立ちの日 (A Day Carved From Rising Winds)**

## 1. セット識別

- `set_id`: `a-day-carved-from-rising-winds`
- 日本語名: 風立ちの日
- 英語名: A Day Carved From Rising Winds
- 中国語名: 风起之日
- 命名判断: README の既存カタログにある英語名ベースの lowercase / hyphen 形式を維持。

## 2. Source Log

| Kind | Page title | URL | Lang | Accessed | Used for | Evidence type |
| --- | --- | --- | --- | --- | --- | --- |
| Set data | A Day Carved From Rising Winds | https://genshin-impact.fandom.com/wiki/A_Day_Carved_From_Rising_Winds | EN | 2026-05-04 | 英語名、セット効果、部位名の確認 | supporting |
| Guide-ZH | 风起之日 - 原神WIKI_BWIKI_哔哩哔哩 | https://wiki.biligame.com/ys/%E9%A3%8E%E8%B5%B7%E4%B9%8B%E6%97%A5 | ZH | 2026-05-04 | 中国語名、セット効果、推奨キャラ候補 | direct |
| Guide-EN | Varka Quick Guide - KQM | https://keqingmains.com/q/varka-quickguide/ | EN | 2026-05-04 | Varka の最適セット、主ステ、ER 不要寄りの判断 | direct |
| Guide-EN | Venti Quick Guide - KQM | https://keqingmains.com/q/venti-quickguide/ | EN | 2026-05-04 | Venti の表運用、ER until requirement、風杯/会心方針 | direct |
| Guide-EN | Klee Quick Guide - KQM | https://keqingmains.com/q/klee-quickguide/ | EN | 2026-05-04 | Klee の A Day 採用と攻撃/会心方針 | supporting |
| Guide-EN | Durin Quick Guide - KQM | https://keqingmains.com/q/durin-quickguide/ | EN | 2026-05-04 | Durin の ER 要求、ATK% / EM / PyroDMG% / ATK% 方針 | direct |

## 3. 推奨設定の方針

- `recommended.yml` は作成しない。
- 理由: 静止スクリーンショットがなく、人手メモから暫定転記するとメンテナンス負荷に対して信頼度が低い。現方針では custom settings を主データとして保守する。

## 4. Custom Preset 調査

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | Hexerei On-field DPS（Varka / Venti / Klee / Razor） | KQM Varka は 4pc A Day を BiS とし、主ステを ATK% / PHEC DMG% または ATK% / CRIT、サブを CRIT > ATK% とする。KQM Venti も表 DPS で 4pc A Day を BiS とし、ER は必要量まで、CRIT と ATK% を優先。BWiki も Venti / Varka / Klee / Razor を直傷向け候補として挙げる。 |
| setting2 | Off-field ATK Sub DPS（Fischl / Mona） | BWiki は装備者が待機中でも 4 セット効果を発動できる点と Fischl / Mona の候補を示す。KQM Durin と異なり、ここでは元素スキル/通常の控え直傷を拾うため、元素杯を Electro/Hydro に絞る。 |
| setting3 | Burst DPS（Durin） | BWiki は Durin の黒龍形態出力向けに 4pc A Day を候補に挙げる。KQM Durin は爆発が主火力で、主ステは ATK% 以上 EM / PyroDMG% または ATK% / 会心、サブは ER 必要量まで、会心、ATK%、EM とする。 |

Inference: `setting1` は表運用の直傷キャラ向けに `substats_required_min: 3` とし、杯は元素/物理/ATK% を許可する。`setting2` は待機中発動を活かす Fischl / Mona 向けで、杯を `ElectroDMG% / HydroDMG% / ATK% / EM` に絞る。`setting3` は Durin の爆発火力向けに `ATK% / EM / ER%` 砂、`PyroDMG% / ATK%` 杯へ分離する。

Rejected: 旧 `setting2` の Venti は KQM の現行整理では表 DPS として A Day を使う意義が強いため、`setting1` 側へ移した。補助 Venti は基本的に翠緑が競合するため対象から外した。Durin は ER・爆発火力・Pyro/ATK 杯の要求が Fischl / Mona と違うため、`setting2` から分離した。

## 5. 作業ログ

- `recommended.yml` を省略する方針に変更。
- `setting1.yml` / `setting2.yml` を現行 KQM/BWiki の対象キャラと主ステ方針に合わせて更新。
- `setting3.yml` を追加し、Durin の爆発火力型を分離。

## 6. 反映済みファイル

- [ ] `presets/a-day-carved-from-rising-winds/recommended.yml`（省略）
- [x] `presets/a-day-carved-from-rising-winds/setting1.yml`
- [x] `presets/a-day-carved-from-rising-winds/setting2.yml`
- [x] `presets/a-day-carved-from-rising-winds/setting3.yml`
- [ ] `docs/ui-mapping.md`（新略語なし）

## 7. 備考

- 今後、ゲーム内 recommended の静止スクリーンショットが揃った場合のみ `recommended.yml` を作成する。
