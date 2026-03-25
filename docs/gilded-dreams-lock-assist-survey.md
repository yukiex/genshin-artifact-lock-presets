# 金メッキの夢 Lock Assist 調査メモ

セット: **金メッキの夢 (Gilded Dreams)**

参照日: 2026-03-25

## 1. 推奨設定の根拠
- Evidence source: [ ] 静止スクリーンショット [ ] 画面録画 [ ] 人手メモ
- Evidence level: provisional
- [ ] 静止スクリーンショットがある場合は `docs/reference/gilded-dreams-lock/` に配置（flower / plume / sands / goblet / circlet）。
- `recommended.yml` は未作成。setting 先行作成のみ実施。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 羽 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 時計 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 杯 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 冠 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |

## 2. Custom Preset 調査
- Game8 セット解説は `金メッキの夢` を元素熟知と攻撃力を同時に伸ばすセットとし、セノ / ティナリ / アルハイゼン / ナヒーダを代表例に挙げる ([game8.jp/genshin/471116](https://game8.jp/genshin/471116))。
- Inference: 実際のフィルタは「激化・超激化の会心アタッカー」と「超開花・烈開花の熟知トリガー」で完全に分けた方が使いやすい。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 激化 / 超激化の会心アタッカー（アルハイゼン、セノ、八重神子、ティナリ） | アルハイゼン記事は `金メッキ4` を基本選択肢とし、元素熟知と反応火力を同時に伸ばせる点を評価 ([game8.jp/genshin/468741](https://game8.jp/genshin/468741))。セノ記事も `金メッキ4` か `雷怒` を推奨 ([game8.jp/genshin/464157](https://game8.jp/genshin/464157))。八重神子記事は激化寄りで `金メッキ4` を推奨 ([game8.jp/genshin/395523](https://game8.jp/genshin/395523))。→ `EM / ATK%` 砂、対応元素DMG% / `EM` 杯、会心2種＋熟知＋攻撃% を主軸にする。 |
| setting2 | 反応トリガー特化の full EM（久岐忍、トーマ） | 久岐忍の超開花編成記事は `楽園4` または `金メッキ4` で **熟知/熟知/熟知** を推奨 ([game8.jp/genshin/560663](https://game8.jp/genshin/560663))。トーマ記事は烈開花で `楽園4` が最適としつつ、烈開花では熟知特化が必要な前提を示す ([game8.jp/genshin/395527](https://game8.jp/genshin/395527))。→ 追加フィルタとしては `EM` を必須にし、`ER` を補助で拾う full EM 構成に寄せる。 |

## 3. 作業ログ
- setting1 / setting2 を作成
- 推奨設定の証跡待ち
- 構造確認は `yq '.preset.slots | keys' presets/gilded-dreams/*.yml` と `yq '.preset.slots[] | select(.substats_required_min == null)' presets/gilded-dreams/*.yml` を使用

## 4. 反映済みファイル
- [ ] `presets/gilded-dreams/recommended.yml`
- [x] `presets/gilded-dreams/setting1.yml`
- [x] `presets/gilded-dreams/setting2.yml`

## 5. 備考
- setting2 は反応ダメージ役の追加フィルタなので、Goblet / Circlet は `EM` を中心にかなり厳しめにした。
- 烈開花トーマの最適は `楽園4` だが、`金メッキ4` の在庫整理用途として archetype 自体は有効と判断した。
