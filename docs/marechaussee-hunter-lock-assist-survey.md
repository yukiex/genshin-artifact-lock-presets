# ファントムハンター Lock Assist 調査メモ

セット: **ファントムハンター (Marechaussee Hunter)**

参照日: 2026-03-25

## 1. 推奨設定の根拠
- Evidence source: [ ] 静止スクリーンショット [ ] 画面録画 [ ] 人手メモ
- Evidence level: provisional
- [ ] 静止スクリーンショットがある場合は `docs/reference/marechaussee-hunter-lock/` に配置（flower / plume / sands / goblet / circlet）。
- `recommended.yml` は未作成。setting 先行作成のみ実施。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 羽 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 時計 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 杯 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 冠 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |

## 2. Custom Preset 調査
- BWiki のセットページは、HP 増減を自前で回せる通常 / 重撃キャラに加えて、フリーナ併用時の汎用アタッカー運用も整理している ([wiki.biligame.com/ys/逐影猎人](https://wiki.biligame.com/ys/%E9%80%90%E5%BD%B1%E7%8C%8E%E4%BA%BA))。
- Inference: 追加フィルタとしては `HP` スケール勢と `ATK` スケール勢に分けたほうが、Goblet / Sands の許容範囲を明確にできる。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | HP 増減を自前で回す HP キャリー（ヌヴィレット） | Game8 のファントム解説は、アタッカー + フリーナ + ヒーラーでの汎用利用まで触れるが、代表例として HP 増減キャラとの相性が強い ([game8.jp/genshin/544097](https://game8.jp/genshin/544097))。Game8 のヌヴィレット記事は `ファントム4` を基本推奨し、重撃火力と HP 推移の噛み合いを解説 ([game8.jp/genshin/539447](https://game8.jp/genshin/539447))。→ `HP% / ER%` 砂、`HydroDMG% / HP%` 杯、会心＋HP%＋ER を優先。 |
| setting2 | ATK スケールの HP 変動キャリー（リネ、リオセスリ） | Game8 のリネ記事は `ファントム4` を基本推奨し、重撃火力と会心率上昇の相性を説明 ([game8.jp/genshin/464305](https://game8.jp/genshin/464305))。リオセスリ記事も `ファントム4` を基本選択肢としている ([game8.jp/genshin/539460](https://game8.jp/genshin/539460))。→ `ATK%` 砂、`PyroDMG% / CryoDMG% / ATK%` 杯、会心2種＋攻撃%＋ER の通常アタッカー型に寄せる。 |

## 3. 作業ログ
- setting1 / setting2 を作成
- 推奨設定の証跡待ち
- 構造確認は `yq '.preset.slots | keys' presets/marechaussee-hunter/*.yml` と `yq '.preset.slots[] | select(.substats_required_min == null)' presets/marechaussee-hunter/*.yml` を使用

## 4. 反映済みファイル
- [ ] `presets/marechaussee-hunter/recommended.yml`
- [x] `presets/marechaussee-hunter/setting1.yml`
- [x] `presets/marechaussee-hunter/setting2.yml`

## 5. 備考
- フリーナ併用の汎用ファントム運用は広すぎるため、custom preset では代表的な 2 archetype に絞った。
- `recommended.yml` はゲーム内証跡が来たら転記する。
