# 暁の星と月の歌 Lock Assist 調査メモ

セット: **暁の星と月の歌 (Aubade of Morningstar and Moon)**

参照日: 2026-03-25

## 1. 推奨設定の根拠
- Evidence source: [ ] 静止スクリーンショット [ ] 画面録画 [ ] 人手メモ
- Evidence level: provisional
- [ ] 静止スクリーンショットがある場合は `docs/references/aubade-of-morningstar-and-moon/` に配置（flower / plume / sands / goblet / circlet）。
- `recommended.yml` は未作成。setting 先行作成のみ実施。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 羽 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 時計 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 杯 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 冠 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |

## 2. Custom Preset 調査
- EN/CN の詳細ビルド記事はまだ薄く、今回は JP のセット解説とキャラ別ビルドを主根拠にした。
- Inference: このセットは待機中の月反応ダメージ強化が核なので、同じセット内でも `ATK/EM` 寄りのサブアタッカーと `HP/ER` 寄りの支援サブアタッカーで main / substat の要求が分かれる。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 月反応サブアタッカー（イネファ） | Game8 セット解説が「待機時間が長いサブアタッカー向け」でおすすめキャラを **コロンビーナ / イネファ** と整理 ([game8.jp/genshin/754098](https://game8.jp/genshin/754098))。Game8 のイネファ記事は、他キャラが `月を紡ぐ夜の歌` を持つ前提なら `暁4` も候補になり、元素スキル起点で攻撃力と月感電ダメージを伸ばす構成を推奨 ([game8.jp/genshin/700093](https://game8.jp/genshin/700093))。→ `ATK% / EM` 砂、`ElectroDMG% / ATK%` 杯、会心2種＋攻撃%＋熟知を優先。 |
| setting2 | HP/ER 寄りの月反応支援サブアタッカー（コロンビーナ） | GameWith も `暁の星と月の歌` を「待機中の月反応ダメージ強化セット」と説明 ([gamewith.jp/genshin/article/show/538016](https://gamewith.jp/genshin/article/show/538016))。Game8 のコロンビーナ記事は `HP / 会心 / チャージ効率` を主軸に挙げている ([game8.jp/genshin/466953](https://game8.jp/genshin/466953))。→ `HP% / ER%` 砂、`HydroDMG% / HP%` 杯、HP%＋ER＋会心を追加フィルタにする。 |

## 3. 作業ログ
- setting1 / setting2 を作成
- 推奨設定の証跡待ち
- 構造確認は `yq '.preset.slots | keys' presets/aubade-of-morningstar-and-moon/*.yml` と `yq '.preset.slots[] | select(.substats_required_min == null)' presets/aubade-of-morningstar-and-moon/*.yml` を使用

## 4. 反映済みファイル
- [ ] `presets/aubade-of-morningstar-and-moon/recommended.yml`
- [x] `presets/aubade-of-morningstar-and-moon/setting1.yml`
- [x] `presets/aubade-of-morningstar-and-moon/setting2.yml`

## 5. 備考
- `recommended.yml` は静止画 / 録画 / 人手メモのいずれかが来てから作成する。
- 現行の setting は「推奨を常時オンにしたうえで追加する補助フィルタ」を前提とする。
