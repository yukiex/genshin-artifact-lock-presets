# Lock Assist 情報取り込みワークフロー

公式ロックアシスト推奨設定をリポジトリに反映する際の手順メモ。Tsukuyo（月を紡ぐ夜の歌）で実施した手順をベースにしており、Tenkyu など他セットでも同じ流れで作業できる。

## 1. スクリーンショットの配置
1. `docs/reference/<set>-lock/` を作成（例: Tsukuyo → `docs/reference/tsukuyo-lock/`、Tenkyu → `docs/reference/tenkyu-lock/`）。
2. ゲーム内「セットロック設定」画面の推奨設定を、各部位（flower/plume/sands/goblet/circlet）ごとに撮影して同フォルダに保存。
   - ファイル名は OS 既定でも問題ないが、後で対応づけやすいようにタイムスタンプなどを残すと便利。
3. 今後 Tenkyu 用に `docs/reference/tenkyu-lock/` を利用予定。

## 2. YAML への反映
1. スクリーンショットから読み取った主ステータス候補を `main_allowed` に転記。
2. 黄色でハイライトされる「必須ステータス」は `substats_required_all_of` に列挙する。  
   - 例: Tsukuyo 推奨設定は全スロットで ER と EM の両方が必須 → `substats_required_all_of: [ER, EM]`
3. 「次の追加ステータスのうち、いずれか N 個以上」表示に対応する `substats_required_any_of` / `substats_required_min` も忘れずに。
4. 個別ファイル（`presets/<set>/recommended.yml`）と配布用カタログ（`presets/lock-presets.yml`）を同じ値にそろえる。

## 3. 証跡ドキュメント
1. `docs/<set>-lock-assist-survey.md` に以下をまとめる:
   - 外部サイトで情報が見つからなかった旨（ある場合は URL）
   - スクリーンショットの格納場所
   - どの画像から何を読み取ったか（主ステータス／サブステ候補／必須ステータスなど）
2. これにより後追いで値の根拠を確認できる。

## 4. README / UI マッピング
新しいフィールドを導入した際は `README.md` と `docs/ui-mapping.md` のスキーマ説明も更新する。`substats_required_all_of` は Tsukuyo 対応時に追加済み。
