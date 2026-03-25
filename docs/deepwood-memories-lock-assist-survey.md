# 深林の記憶 Lock Assist 調査メモ

セット: **深林の記憶 (Deepwood Memories)**

参照日: 2026-03-25

## 1. 推奨設定の根拠
- Evidence source: [ ] 静止スクリーンショット [ ] 画面録画 [ ] 人手メモ
- Evidence level: provisional
- [ ] 静止スクリーンショットがある場合は `docs/reference/deepwood-memories-lock/` に配置（flower / plume / sands / goblet / circlet）。
- `recommended.yml` は未作成。setting 先行作成のみ実施。

| スロット | 証跡ファイル / メモ | 主ステータス | サブステ候補 (いずれか2個) | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 羽 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 時計 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 杯 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |
| 冠 | `(未取得)` | `(未取得)` | `(未取得)` | `(未取得)` |

## 2. Custom Preset 調査
- BWiki のセットページは深林4を草耐性デバフ役の基礎セットとして扱う ([wiki.biligame.com/ys/深林的记忆](https://wiki.biligame.com/ys/%E6%B7%B1%E6%9E%97%E7%9A%84%E8%AE%B0%E5%BF%86))。
- Inference: 実運用では「草耐性デバフを撒くサポーター」と「他に深林持ちがいないので自分で持つ草キャリー」で要求 stat が大きく異なる。

| Preset | Archetype / 対象キャラ | 参考URL・メモ |
| --- | --- | --- |
| setting1 | 草耐性デバフを撒くサポーター（白朮、ヨォーヨ、草主人公、コレイ） | Game8 のセット解説は草元素キャラに限らず使える深林枠としてサポーター採用を明言 ([game8.jp/genshin/471115](https://game8.jp/genshin/471115))。ヨォーヨ記事も `深林4` / `千岩4` を候補にし、サポート役としての運用を推奨 ([game8.jp/genshin/366248](https://game8.jp/genshin/366248))。草主人公記事も `深林4` 推奨 ([game8.jp/genshin/466495](https://game8.jp/genshin/466495))。→ `ER%` を実質必須にし、`EM / HP% / Healing% / Favonius 用 CR` を許容する。 |
| setting2 | 他に深林持ちがいない草キャリー（ナヒーダ、アルハイゼン、ティナリ） | Game8 のナヒーダ記事は編成に1人は深林を持たせたいとし、ナヒーダ本人の装備候補として深林を推奨 ([game8.jp/genshin/468757](https://game8.jp/genshin/468757))。アルハイゼン記事も深林枠がいないなら深林4と明記 ([game8.jp/genshin/468741](https://game8.jp/genshin/468741))。→ `EM / ATK%` 砂、`DendroDMG% / EM` 杯、会心2種＋熟知＋攻撃% を優先する。 |

## 3. 作業ログ
- setting1 / setting2 を作成
- 推奨設定の証跡待ち
- 構造確認は `yq '.preset.slots | keys' presets/deepwood-memories/*.yml` と `yq '.preset.slots[] | select(.substats_required_min == null)' presets/deepwood-memories/*.yml` を使用

## 4. 反映済みファイル
- [ ] `presets/deepwood-memories/recommended.yml`
- [x] `presets/deepwood-memories/setting1.yml`
- [x] `presets/deepwood-memories/setting2.yml`

## 5. 備考
- setting1 は Favonius 採用を見込んで `CR` を候補に残している。
- setting2 は他キャラが深林を持てない編成の代替案であり、通常の最適解を置き換える意図ではない。
