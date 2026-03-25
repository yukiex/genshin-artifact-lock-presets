# 風立ちの日 Lock Assist 調査メモ

セット: **風立ちの日 (A Day Carved From Rising Winds)**

参照日: 2026-03-25

## 1. 推奨設定の根拠
- Evidence source: [ ] 静止スクリーンショット [ ] 画面録画 [ ] 人手メモ
- Evidence level: provisional
- [ ] 静止スクリーンショットがある場合は `docs/references/a-day-carved-from-rising-winds/` に配置（flower / plume / sands / goblet / circlet）。
- `recommended.yml` は未作成。setting 先行作成のみ実施。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 羽 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 時計 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 杯 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 冠 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |

## 2. Custom Preset 調査
- EN/CN での詳細ビルド整理はまだ薄く、JP のセット解説とキャラ別ビルドを優先した。
- Inference: ファルカ系の表運用と、フィッシュル / ウェンティ系の控え運用では、同じセットでも `ATK%` 固定度と `ER%` の必要量が分かれる。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 表に立つ攻撃型メインアタッカー（ファルカ、クレー） | Game8 のセット解説はおすすめキャラとして **フィッシュル / クレー / ウェンティ / レザー** を掲載し、ATK 系バフを乗せやすいセットと説明 ([game8.jp/genshin/754099](https://game8.jp/genshin/754099))。Game8 のファルカ記事は「基本的に風立ちの日4セット」を推奨し、攻撃力2500目標と、編成に応じて元素が変化する運用を解説 ([game8.jp/genshin/366252](https://game8.jp/genshin/366252))。クレー記事も会心系と攻撃寄りビルドを推奨 ([game8.jp/genshin/352608](https://game8.jp/genshin/352608))。→ `ATK%` 砂、対応元素DMG% / `ATK%` 杯、会心2種＋攻撃% を主軸に設定。 |
| setting2 | 控え寄りの ATK サブ DPS（フィッシュル、ウェンティ） | 同じく Game8 セット解説がフィッシュル / ウェンティを明示 ([game8.jp/genshin/754099](https://game8.jp/genshin/754099))。フィッシュル記事はオズ主体のサブアタッカー運用、ウェンティ記事はサポートとアタッカーで武器 / ビルドが分かれる点を整理している ([game8.jp/genshin/352612](https://game8.jp/genshin/352612), [game8.jp/genshin/352607](https://game8.jp/genshin/352607))。→ `ER%` 砂を許容しつつ、`ElectroDMG% / AnemoDMG% / ATK%` 杯、会心2種＋攻撃%＋ER を追加フィルタにする。 |

## 3. 作業ログ
- setting1 / setting2 を作成
- 推奨設定の証跡待ち
- 構造確認は `yq '.preset.slots | keys' presets/a-day-carved-from-rising-winds/*.yml` と `yq '.preset.slots[] | select(.substats_required_min == null)' presets/a-day-carved-from-rising-winds/*.yml` を使用

## 4. 反映済みファイル
- [ ] `presets/a-day-carved-from-rising-winds/recommended.yml`
- [x] `presets/a-day-carved-from-rising-winds/setting1.yml`
- [x] `presets/a-day-carved-from-rising-winds/setting2.yml`

## 5. 備考
- set 効果自体が ATK 系なので、追加フィルタ側では会心と ER の差分を強めに出した。
- `recommended.yml` は証跡到着後に転記する。
