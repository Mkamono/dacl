├── .vscode/               # VS Code ワークスペース設定、推奨拡張機能など
│   └── extensions.json
│   └── settings.json
│
├── cmd/                   # 実行可能コマンド（CLIツール、LSPサーバーなど）
│   ├── dacl/              # DACL CLIツール (`dacl` コマンド)
│   │   └── main.go
│   │
│   └── dacl-ls/           # DACL Language Server (`dacl-ls` コマンド)
│       └── main.go
│
├── docs/                  # ドキュメント（仕様書、使い方ガイドなど）
│   ├── spec.md            # DACLの仕様書
│   └── usage.md           # DACLの使用方法
│   └── ...
│
├── internal/              # 内部パッケージ（外部に公開しない、リポジトリ内で閉じるロジック）
│   ├── parser/            # パーサーの実装 (lexer, parser, ast)
│   │   ├── lexer.go
│   │   ├── parser.go
│   │   └── ast.go         # 抽象構文木 (AST) の定義
│   │
│   ├── resolver/          # 参照解決 (パス、環境変数) ロジック
│   │   └── resolver.go
│   │
│   ├── loader/            # ファイルローダーとインポートロジック
│   │   └── loader.go
│   │
│   ├── types/             # DACLのデータ型定義 (マップ、リスト、スカラー値のGo表現)
│   │   └── value.go       # Valueインターフェース、StringValue, IntValueなどの実装
│   │
│   ├── errors/            # カスタムエラー定義
│   │   └── errors.go
│   │
│   └── config/            # 設定ファイルのロードと処理のメインロジック (internalでまとめたい場合)
│       └── config.go      # DACLファイル全体のパース、解決、インポート処理をまとめる
│
├── pkg/                   # 外部に公開する共有パッケージ（ライブラリとして利用可能にする場合）
│   └── dacl/              # DACLをGoのライブラリとして利用するためのAPI
│       └── parse.go       # `dacl.Parse()` や `dacl.Load()` などの公開API
│       └── model.go       # DACLデータモデルの公開用型定義 (例: Map, List)
│       └── (core logic will be imported from internal/)
│
├── editors/               # エディタ向け拡張機能
│   └── vscode-dacl/       # VS Code 拡張機能のプロジェクトルート (TypeScript)
│       ├── syntaxes/      # シンタックスハイライト定義
│       │   └── dacl.tmLanguage.json
│       ├── package.json   # 拡張機能のマニフェスト
│       ├── src/           # 拡張機能のソースコード
│       │   ├── extension.ts # 拡張機能のエントリーポイント
│       │   └── client.ts  # LSPクライアント側のロジック
│       │   └── test/
│       ├── out/
│       ├── .vscodeignore
│       └── tsconfig.json
│       └── README.md
│
├── examples/              # DACL設定ファイルのサンプル集
│   ├── basic_config.dacl
│   ├── advanced_references.dacl
│   ├── import_example/
│   │   ├── app_config.dacl
│   │   └── db_settings.dacl
│   └── ...
│
├── testdata/              # テスト用のDACLファイルや関連データ
│   ├── parser/
│   │   ├── valid/
│   │   │   └── sample.dacl
│   │   ├── invalid/
│   │   │   └── error.dacl
│   │   └── ...
│   └── resolver/
│   └── ...
│
├── .gitignore             # Git無視ファイル
├── LICENSE                # ライセンスファイル
├── README.md              # プロジェクト全体のREADME
├── go.mod                 # Goモジュール定義ファイル
├── go.sum                 # Goモジュールチェックサムファイル