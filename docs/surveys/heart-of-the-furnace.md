# 炉炎溶錬の心 Lock Assist 調査メモ

セット: **炉炎溶錬の心 (Heart of the Furnace)**

参照日: 2026-10-18。調査範囲: Ver.7.1 までの公開ビルド。
`set_id`: `heart-of-the-furnace`（公式英語名全体を採用）。

## 1. 推奨設定の根拠

- Evidence source: ユーザー提供のセット選択画面。セット名・効果は確認できるが、ロック条件は写っていない。
- Evidence level: provisional（ロック条件の証跡未取得）。
- `recommended.yml` は未作成。独自設定をゲーム内推奨として代用しない。
- 部位別の証跡は `docs/references/heart-of-the-furnace/` に収集する。
- 添付画像は UID を含むためリポジトリには保存しない。

| スロット | 証跡 | 主ステータス | サブステ候補・個数 | 必須ステータス |
| --- | --- | --- | --- | --- |
| 花 | 未取得 | 未取得 | 未取得 | 未取得 |
| 羽 | 未取得 | 未取得 | 未取得 | 未取得 |
| 時計 | 未取得 | 未取得 | 未取得 | 未取得 |
| 杯 | 未取得 | 未取得 | 未取得 | 未取得 |
| 冠 | 未取得 | 未取得 | 未取得 | 未取得 |

## 2. ソースログ

以下はロック条件の転記元ではなく、独自設定の根拠。

| 出典・URL | 確認した内容 |
| --- | --- |
| [HoYoWiki: Artifacts](https://wiki.hoyolab.com/pc/genshin/aggregate/5?lang=en-us) | 英語名・攻撃力増加・星反応のチームバフ。控えから発動可能、同名バフは重複しない |
| [KQM: Odette Quick Guide](https://keqingmains.com/q/odette-quickguide/) | 攻撃 / 攻撃 / 会心。星反応火力には元素ダメージ杯を使わない。爆発目的の ER 積みは通常不要 |
| [KQM: Cryo Traveler Stellar Swirl Infographic](https://keqingmains.com/i/cryo-traveler-stellar-swirl/) | 攻撃主体・熟知代替・会心。炉炎は他の装備者がいない場合の選択肢。C1＋星鋒の剣なら ER 不要 |
| [KQM: Yae Miko Quick Guide](https://keqingmains.com/q/yae-quickguide/) | 星電導では攻撃 / 熟知と会心を重視。他に炉炎担当がいない場合に採用。熟知の時計と杯の同時採用は避ける |
| [KQM: Alyosha Quick Guide](https://keqingmains.com/q/alyosha-quickguide/) | ER または攻撃時計、攻撃杯、治療 / 攻撃 / 会心冠。氷下地があり自身が星電導を起こせる編成で炉炎を採用 |
| [KQM: Qiqi Quick Guide](https://keqingmains.com/q/qiqi-quickguide/) | 回復と C6 バフは攻撃参照。西風なら会心率、必要に応じ ER。通常は千岩等を優先 |
| [GameWith: 炉炎溶錬の心](https://gamewith.jp/genshin/article/show/570880) | 日本語表記と適性候補を照合。七七を装備候補に含む |
| [KQM: Sandrone Quick Guide](https://keqingmains.com/q/sandrone-quickguide/) | 編成例で炉炎をオデット、旧貴族をアリョーシャに分担 |
| [KQM: Vodyanitsa Quick Guide](https://keqingmains.com/q/vodyanitsa-quickguide/) | HP 型サポート。星拡散編成でも自身は反応を有効化せず、炉炎は他の担当に分担 |

EN の理論ガイドを主根拠にし、JP で表記と候補を照合した。
KQM の旅人インフォグラフィックは画像も直接確認した。

## 3. Custom Preset 調査

| 設定 | 対象 | 時計 | 杯 | 冠 |
| --- | --- | --- | --- | --- |
| setting1: 星反応火力型 | オデット、旅人(氷)、八重神子 | 攻撃% / 熟知 | 攻撃% / 熟知 | 会心率 / 会心ダメージ |
| setting2: 攻撃参照の回復支援型 | アリョーシャ、七七 | ER% / 攻撃% | 攻撃% | 治療 / 攻撃% / 会心率 |

花は HP、羽は攻撃力の固定メイン。設定1・2は役割と必要ステータスを分けた。

### Setting1 の設計

- 候補は `CR / CD / ATK% / EM`。花・羽は3個以上、時計・杯・冠は2個以上。必須指定はなし。
- Inference: 時計・杯の熟知許可は旅人 / 八重の代替候補を拾うための和集合。オデットは攻撃時計・攻撃杯を基本とする。
- Inference: ER を共通候補に含めず、通常のスキル・星反応火力を優先する。爆発を多用する凸・武器・編成では ER 品も個別に確認する。
- 八重は熟知時計＋熟知杯を同時採用しない。部位をまたぐ条件はこの YAML では表せない。

### Setting2 の設計

- 候補は `ER / CR / ATK% / ATK` の2個以上。必須指定はなし。
- Inference: 回復に有効な攻撃実数も残す。羽には攻撃実数サブが付かないため、ER / 会心率 / 攻撃% のうち2個が必要になる。
- Inference: 西風の会心率と ER は武器・凸・回し方次第。共通の必須条件にせず、ER メイン時計や会心率メイン冠も成立させる。
- 七七の ER 時計は爆発を使う運用向けの追加許可。通常の攻撃時計を置き換える推奨ではない。
- 七七の炉炎採用は JP の候補と発動条件に基づく代替案。千岩等を使い、オデットに炉炎を任せる編成も多い。
- アリョーシャは星反応の有効化役ではない。氷下地と、自身による反応発動を確保する。

### 最新キャラ・関連候補の確認

| キャラ | 今回の扱い |
| --- | --- |
| オデット / アリョーシャ / 氷主人公 | 設定1 / 2に反映。武器・凸の条件は上記参照 |
| サンドローネ | 星電導編成を確認。自身の火力用セットと分担し、炉炎担当の targets には追加しない |
| ヴェスナ | 紅血の証の設定1で扱う |
| ヴォジャニーツァ | HP 支援・千岩 / HP 2セット等を優先。水付着だけでは炉炎担当にできないため追加しない |
| ファルザン / スクロース | 星拡散編成の支援候補。翠緑との分担が必要で、今回の攻撃参照型には混ぜない。熟知型の炉炎品は個別確認 |
| ディオナ | HP 支援型のため今回の2型には含めない。HP 品はこの設定だけで不要判定しない |

Inference: targets はこの設定の対象であり、装備可能キャラの全一覧ではない。
未実装キャラの予想性能はルールの根拠にしない。新しい公開ビルドが出たら再確認する。

## 4. 適用と限界

- 設定1・2は保持候補を追加する用途。両方の型を残す場合は両方を有効化する。
- 推奨が使える場合は既存方針どおりゲーム内推奨も有効化するが、その内容は今回は未転記。
- `main_allowed` は主ステを照合するヒント。UI で必須にできると仮定しない。
- 主ステと同名のサブステは付かない。必須指定を避け、各メインでも閾値を満たせるよう検証する。
- Inference: 個数の閾値は在庫整理用の独自判断で、各ガイドの指定値ではない。
- 未ロックは自動的な処分判定ではない。強化済み品、他セットの自由枠、HP / 熟知支援型は別途確認する。

## 5. 作業ログと反映済みファイル

- [x] `presets/heart-of-the-furnace/setting1.yml`
- [x] `presets/heart-of-the-furnace/setting2.yml`
- [x] `docs/surveys/heart-of-the-furnace.md`
- [x] `docs/references/heart-of-the-furnace/`（証跡待ちの空ディレクトリ）
- [x] `README.md` / `docs/target-sets.md`
- [ ] `presets/heart-of-the-furnace/recommended.yml`（5部位のロック画面待ち）

検証結果（2026-10-18）:

- `yamllint presets docs`: 終了コード0。既存形式に合わせた `---` 省略の警告のみ。
- PyYAML で5部位・全必須キー・閾値・targets の日英対応を確認。
- 各許可メインについて、同名サブを除いても最大4枠で条件が成立することを確認。
- `yq` 相当の構造確認は Python で実施（jq 実行環境なし）。
- `rg` で targets / targets_ja を確認。`git diff --check` は問題なし。
