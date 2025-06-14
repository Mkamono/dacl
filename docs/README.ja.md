# DACL: Data And Configuration Language

## 概要

DACL (Data And Configuration Language) は、シンプルさと堅牢性を追求した、人間にとっても機械にとっても読みやすい設定ファイルフォーマットです。YAMLの簡潔さと表現力を参考にしつつ、曖昧さを排除し、エラーの発生しにくい構造を目指して設計されました。
設計思想

DACLは、以下の原則に基づいて設計されています。

- シンプルさと堅牢性: 必要最低限の機能に絞り込み、曖昧さを排除することで、予期せぬエラーの発生を防ぎます。
- 視覚的明瞭性: 厳格な2スペースインデントルールにより、設定の階層構造が一目で把握できます。
- 機械可読性: 厳密な構文と型定義により、パース（解析）が容易で、アプリケーションへの統合がスムーズです。
- 人間可読性: 直感的で理解しやすい記述を心がけ、設定の保守性を高めます。
- モジュール性: 外部ファイルのインポート機能と強力な参照メカニズムにより、設定の分割と再利用を促進します。

## 特徴

DACLは、以下の主要な特徴を備えています。

- 厳格なインデント
    - インデントは半角スペース2文字のみを使用し、タブは禁止です。不適切なインデントはパースエラーとなります。
- 明確なデータ型
    - 文字列は常にダブルクォーテーション ("") で囲むことを必須とします。これにより、型推論による曖昧さを排除します。
    - 整数、浮動小数点数、真偽値 (true, false)、Null値 (null) は厳密に区別されます。
- データ構造
    - マップ（キー-値ペア）とリスト（配列）をサポートします。
- コメント
    - 行コメント (#) をサポートし、設定内容の説明を記述できます。
- 強力な参照機能
    - ${path.to.value} の形式で、設定ファイル内の他の値を参照できます。参照された値はディープコピーとして扱われるため、安全です。
    - ${env:VAR_NAME} の形式で、環境変数を参照できます。${env:VAR_NAME:-default_value} の形式でデフォルト値を指定することも可能です。
    - import "file.dacl" as "namespace" 構文により、別のDACLファイルを指定した名前空間の下に読み込み、設定をモジュール化できます。

DACLファイルの例

```
import "database.dacl" as "db" # データベース設定をインポート

service:
  name: "my-awesome-app"
  port: ${env:APP_PORT:-8080} # 環境変数APP_PORTを参照、未設定なら8080

logging:
  level: "info"
  # log_file: "/var/log/${service.name}.log" # 内部パス参照の例 (コメントアウト)
  log_output:
    - "console"
    - "file"

database_connection:
  type: ${db.type} # インポートしたdb名前空間から参照
  host: ${db.host}
  user: ${env:DB_USER} # 必須の環境変数参照
  password: "${env:DB_PASSWORD}" # 文字列として環境変数参照

metrics:
  enabled: true
  interval_seconds: 60

# database.dacl の内容の例
# type: "postgresql"
# host: "localhost"
# port: 5432
```

開発状況

このリポジトリは現在開発中です。DACLパーサー、バリデーター、そして関連ツールの実装を進めています。
貢献について

DACLプロジェクトへの貢献を歓迎します！
バグ報告、機能提案、プルリクエストなど、GitHubのIssueとPull Requestを通じてご参加ください。
