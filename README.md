# Antigravity 開発用ワークスペーステンプレート

このリポジトリ（フォルダ）は、Antigravity（愛称：ハル）を用いたAI主導のプログラム開発における標準的なワークスペーステンプレートです。

## 特徴

このテンプレートには、開発をスムーズに進め、品質を担保するための**AI開発基盤**と**参照資料**があらかじめセットアップされています。特に、最新の「V字モデル化 ADAプロセス」に対応したエージェントの専門スキルが組み込まれています。

*   **Antigravity設定 (`.agents/`)**: 
    *   **ワークフロー (`workflows/`)**: ADA（Agent-Driven Agile）プロセスのV字モデル標準開発手順が定義されています。
    *   **スキル (`skills/`)**: 各開発工程を担当する専門エージェントと、ASDoQ文書品質モデルに基づき品質を保証する高次レビュアーエージェントのスキル（計8つ）が含まれます。
        *   **Implementers**: `requirements-engineer`, `architect`, `programmer`, `test-engineer`
        *   **Reviewers**: `requirements-reviewer`, `architecture-reviewer`, `code-reviewer`, `test-reviewer`
*   **ドキュメント (`docs/`)**: 
    *   ASDoQ文書品質モデルなど、開発・ドキュメント作成時に参照すべき資料が配置されています。
*   **仕様書・設計書 (`doc/`)**:
    *   要求仕様書（SW105）やアーキテクチャ設計書（SW205）などの作成成果物はこちらのフォルダ下に保存・管理されます。
*   ** Cursor ルール (`.cursor/rules/`)**:
    *   `project-rules.mdc` にて、コード先行の禁止や、人間とAIエージェントの明確な役割分担（V字モデルの実践）が定義されています。
*   **バージョン管理 (`.gitignore`)**:
    *   OSの一時ファイルやエディタ設定など、言語に依存しない汎用的な無視設定が含まれています。

## 使い方

新しいプロジェクトを開始する際は、以下の手順でこのテンプレートを利用してください。

1.  **フォルダのコピー**: このテンプレートフォルダをコピーし、新しいプロジェクト名に変更します。
2.  **ワークスペースを開く**: VS Code等のエディタで新しいフォルダを開き、Antigravityとのセッションを開始します。
3.  **環境の初期化**: 開発するアプリケーションの要件（使用言語、フレームワークなど）をAntigravityに伝え、必要なディレクトリ（例：`src/`、パッケージ初期化等）の作成と環境構築を依頼してください。（例：「ReactとTypeScriptで新しいWebアプリを作るための初期設定をして」など）
4.  **.gitignore の更新**: 初期化された環境に合わせて、必要であればAntigravityに `.gitignore` へ言語やフレームワーク固有の設定を追加するよう依頼してください。


##  context7 (MCPサーバー) の設定について

このリポジトリでは、`context7` というAIがライブラリを使うときに最新のドキュメントを参照できるようにするMCPサーバーを用いています。具体的には、次の設定をしています。設定が難しい場合は、`.\.cursor\rules\use-context7-for-docs.mdc` ファイルを削除してください。

### (1) context7 API Keyの取得
* [https://context7.com/](https://context7.com/) にGoogleアカウントなどでサインインする。
* 上部の `More...` メニュー内に `Create API Key` があるので、そこでAPI Keyを作成してコピーする。

### (2) AntigravityでのMCPサーバー設定
* Antigravity画面右上の三点ドットから `MCP Servers` を選択し、`View raw config` を選択する。
* 以下のように作成または追記する。`YOUR_API_KEY` に、先ほど取得したキーを入力する。

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp", "--api-key", "YOUR_API_KEY"]
    }
  }
}
```

---
*Created and Maintained by Masa & Hal*