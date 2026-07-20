# 天からの贈り物 Lock Assist 調査メモ

セット: **天からの贈り物 (Celestial Gift)**

## 1. セット識別

- `set_id`: `celestial-gift`
- 日本語名: 天からの贈り物
- 英語名: Celestial Gift
- 中国語名: 天之美赐
- 命名判断: 公式英語表記を lowercase / hyphen 形式へ変換。

## 2. Source Log

| Kind | Page title | URL | Lang | Accessed | Used for | Evidence type |
| --- | --- | --- | --- | --- | --- | --- |
| Official | New Artifacts: Celestial Gift & Disenchantment in Deep Shadow | https://www.hoyolab.com/article/45163741 | EN | 2026-07-20 | 英語名、現行セット効果 | direct |
| Guide-JA | 天からの贈り物の効果と装備おすすめキャラ | https://gamewith.jp/genshin/article/show/560356 | JA | 2026-07-20 | 日本語名、セット効果、ニコ / モナ / ドゥリン / フィッシュルの適性 | direct |
| Guide-ZH | 天之美赐 - 原神WIKI_BWIKI | https://wiki.biligame.com/ys/%E5%A4%A9%E4%B9%8B%E7%BE%8E%E8%B5%90 | ZH | 2026-07-20 | 中国語名、魔導キャラ別の装備候補 | direct |
| Guide-EN | Prune Quick Guide - KQM | https://keqingmains.com/q/prune-quickguide/ | EN | 2026-07-20 | プルーネの ATK% / ER、ATK%、ATK% 方針 | direct |
| Guide-ZH | 尼可/攻略 - 原神WIKI_BWIKI | https://wiki.biligame.com/ys/%E5%B0%BC%E5%8F%AF/%E6%94%BB%E7%95%A5 | ZH | 2026-07-20 | ニコの攻撃力依存シールド・バフと装備方針 | direct |

## 3. 推奨設定の方針

- `recommended.yml` は作成しない。
- 理由: ゲーム内 Lock Assist の静止スクリーンショットがなく、現行方針では根拠の明確な custom settings を優先する。

## 4. Custom Preset 調査

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | Hexerei ATK Support（Nicole / ニコ） | BWiki はシールドとバフが攻撃力依存であることを示す。攻撃力を優先し、爆発運用や西風秘典向けに ER / CR も候補へ残す。 |
| setting2 | Anemo ATK/ER Support（Prune / プルーネ） | KQM は ATK% または ER% / ATK% / ATK%、ER 必要量まで > ATK% > 西風時 CR を推奨する。天からの贈り物は風元素アタッカー支援時の候補。 |
| setting3 | Off-field Elemental Holder（Durin / ドゥリン、Fischl / フィッシュル、Mona / モナ） | GameWith と BWiki が装備候補として挙げる。待機中発動を活かしつつ個人火力を落としすぎない ATK / ER / EM、元素杯 / ATK 杯、会心冠とする。 |

Inference: `setting1` と `setting2` はサポート用の有効ステータスが少ないため `substats_required_min: 2` とする。`setting3` は個人火力を持つ控え装備者向けなので会心を含む5候補から3個を要求する。

Rejected: アルベドは BWiki の装備候補だが DEF スケール専用の4つ目の設定が必要になるため、今回の3設定からは除外した。ウェンティ / スクロースは風元素編成以外では翠緑の影が競合し、プルーネと主ステ方針も異なるため `setting2` に混在させない。

## 5. 作業ログ

- `recommended.yml` は証跡不足のため省略。
- ニコ、プルーネ、控え元素装備者の3アーキタイプを分離。

## 6. 反映済みファイル

- [ ] `presets/celestial-gift/recommended.yml`（省略）
- [x] `presets/celestial-gift/setting1.yml`
- [x] `presets/celestial-gift/setting2.yml`
- [x] `presets/celestial-gift/setting3.yml`
- [ ] `docs/ui-mapping.md`（新略語なし）

## 7. 備考

- 今後、ゲーム内 recommended の静止スクリーンショットが揃った場合のみ `recommended.yml` を検討する。
