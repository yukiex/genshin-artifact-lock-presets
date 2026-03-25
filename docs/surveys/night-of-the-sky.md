# Night of the Sky Lock Assist 調査メモ

ゲーム内ロックアシスト推奨設定（スクリーンショットは `docs/references/night-of-the-sky/`）を元に、`presets/night-of-the-sky/recommended.yml` を更新した内容を記録する。

| スロット | 画像ファイル | 主ステータス | サブステ候補 | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | `flower.png` | HP 固定 | 元素熟知 / 攻撃力% / 会心率 / 会心ダメージ | 会心率, 会心ダメージ |
| 羽 | `plume.png` | 攻撃力固定 | 同上 | 会心率, 会心ダメージ |
| 時計 | `sands.png` | 元素熟知 / 攻撃力% | 会心率 / 元素熟知 / 会心ダメージ / 攻撃力% | 会心率, 会心ダメージ |
| 杯 | `goblet.png` | 元素熟知 / 攻撃力% | 同上 | 会心率, 会心ダメージ |
| 冠 | `circlet.png` | 会心率 / 元素熟知 / 会心ダメージ | 同上 | 会心率, 会心ダメージ |

- UI の文言は「次の追加ステータスのうち、いずれか2個を含む。かつ必須ステータスをすべて含む」。  
- そのため YAML では `substats_required_any_of` に列挙（[CR, CD, ER, EM]）し、`substats_required_min: 2`、さらに `substats_required_all_of: [CR, CD]` をセットしている。

## 反映済みファイル
- `presets/night-of-the-sky/recommended.yml`

## Custom Preset 調査メモ
`setting1/setting2` は「異なるキャラクタータイプを 2 件まで保存できる」ゲーム内仕様に揃えるため、攻略サイトの記述を根拠にビルドごとに分岐させた。

### Setting1 – Quickbloom Driver (Electro)
- [GameWith: 天穹の顕現せし夜の効果と装備おすすめキャラ (2025/11/05)](https://gamewith.jp/genshin/article/show/516495) のおすすめ表にて、`セノ/アルハイゼン/ティナリ/ネフェル/フリンズ` など月反応を軸にしたメインアタッカーが明記されている。また本文で「例えばセノに天穹4セットを装備させ…」と月感電ドライバー事例が紹介されている。
- [Gamerch 同記事](https://gamerch.com/genshinwiki/940069) ではナドクライ出身キャラに加えて `クロリンデ / 八重神子 / ウェンティ / 魈 / 楓原万葉` など雷・風のドライバー候補が列挙され、月感電を自前で起こせるキャラ向けと明示。
- [神ゲー攻略 (2025/08/30)](https://kamigame.jp/genshin/page/384956109032531369.html) は「月反応に必要な熟知と会心をバフ」と強調しつつ `フリンズ / イネファ` を例に挙げ、会心+熟知を両立するビルドを推奨。
- 以上より、`setting1` は月感電や超激化を自力で回せるオンフィールド雷アタッカー（`Cyno, Clorinde, YaeMiko, Keqing` など）を対象にし、サブステは `CR/CD/EM` を軸に `ER` を追加要求、砂は `EM/ATK%/ER%`、杯は `ElectroDMG%` を許可にした。

### Setting2 – Lunar Crystallize Driver (Geo DEF)
- [GameWith: しはくのおすすめ聖遺物と性能評価 (2025/11/10)](https://gamewith.jp/genshin/article/show/516541) では、`天穹4` を最適候補として掲示しつつ、メインステータスを `防御% / 防御% / 会心`、サブステータスを `会心率 / 会心ダメージ / 防御力%` 優先で提示している。
- [Game8: しはくのおすすめビルド｜聖遺物と武器 (2025/11/17)](https://game8.jp/genshin/712405) でも、聖遺物のメインは `防御力% / 防御力% / 会心系`、サブは `会心系 > 防御力% > 元素熟知` を推奨している。
- [Gamerch: しはくのおすすめ聖遺物・武器まとめ (2025/11/13)](https://gamerch.com/genshinwiki/972609) は、`天穹4` の厳選目安を `防御力 / 防御力 / 会心` とし、月結晶ダメージ運用で `防御力` を主軸に置く方針を明記している。
- 以上より `setting2` は兹白（`Shihaku`）向けに、砂/杯を `DEF%` 主軸（`EM` 代替）へ変更し、サブステは `CR/CD/DEF%/EM` を中心に `substats_required_min: 3` で厳しめに設定した。杯は元素ダメージ%ではなく `DEF%` を許可している。
