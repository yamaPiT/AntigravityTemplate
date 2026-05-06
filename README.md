# Google Antigravity 専用 DADA プロセステンプレート 🤖📝

![GitHub release (latest by date)](https://img.shields.io/github/v/release/yamaPiT/AntigravityTemplate?label=最新バージョン)
![GitHub last commit](https://img.shields.io/github/last-commit/yamaPiT/AntigravityTemplate?label=最終更新)

本リポジトリは、**Google Antigravity** でAIエージェントと人間が協調しながら、高品質なソフトウェアを高速に構築するための **DADA（Document-and-Agent-Driven Agile）開発プロセステンプレート** です。

テンプレートを自分のリポジトリにコピーしてチャットに指示を書き込むだけで、AIが **要求定義 → 設計 → 実装 → テスト** の全工程を、ドキュメントを軸に自律的に進めてくれます。

> [!NOTE]
> 作者はAntigravityとAgent Codingの学習中です。このプロセスは未完成で、期待通りに動作しない部分もあります。日々改善していきますので、ご容赦ください。

---

## 📖 DADAプロセスとは？

**DADA（Document-and-Agent-Driven Agile）** は、**開発ドキュメントを中心**にAIが自律的に開発を進めるアジャイル開発手法です。

従来のアジャイル開発では、要求仕様がポストイットやホワイトボードに書かれて散逸したり、実装コードばかりが重視された結果、「要求仕様書・設計書とソースコードが乖離してしまう」という問題が少なからず発生していました。
DADAプロセスはこの発想を反転させ、**開発ドキュメントをシステムの唯一の情報源（Single Source of Truth）** として常に最新に保ちながら開発を進めます。要求・設計・テスト仕様とソースコードが乖離する余地を、プロセスの構造そのもので排除しています。

### なぜAgentic Codingでもドキュメント中心なのか？

「AIがコードを書いてくれるなら、ドキュメントはもう要らないのでは？」—— そう思われるかもしれません。しかし、AIにプログラミングを自律的に任せる手法（Agentic Coding）には、次の**2つの致命的な弱点**があります。

| # | 問題 | 何が起きるか |
|:---:|:---|:---|
| 1 | **記憶喪失** | AIの一時メモリ（コンテキストウィンドウ）は有限です。対話が長くなると、過去に合意した仕様や設計が押し出されて消え、中・大規模開発では整合性がすぐに破綻します。 |
| 2 | **ブラックボックス化** | この問題を防ぐためAI自身に内部メモを自動生成させるアプローチもありますが、それはAIの都合で書かれたものです。人間が読んでも理解しづらく、意図通りに品質を制御・レビューすることが困難です。 |

つまり、AI時代であっても「人間が読み、理解し、承認できる開発ドキュメント」の重要性はむしろ増しているのです。

### DADAの答え

> **「一時的な会話データや内部メモではなく、人間が読める『開発ドキュメント』を唯一の情報源にする」**

AIはコードを書く前に必ず「要求仕様書」や「設計書」を作成・更新し、**人間がそれを承認してから次の工程へ進みます**。ドキュメントは常にコードより先に更新されるため、「ドキュメントが古い」「仕様と実装が合っていない」という事態が構造的に発生しません。

### 🌟 DADAプロセスを支える5つの仕組み

| 仕組み | 説明 |
|:---|:---|
| **ドキュメント絶対主義と承認ゲート** | 決定事項はすべてドキュメント（Single Source of Truth）に集約されます。各工程で人間がドキュメントを承認するまで次の工程に進めず、仕様と実装のズレを構造的にゼロにします。 |
| **アテンション・リセット（コンテキスト汚染防止）** | フェーズ移行時、AIが自律的に不要な過去のチャット履歴（議論・推測）を捨て、最新の承認済みドキュメントだけに集中し直します。AI特有の記憶喪失やハルシネーションを根本から回避します。 |
| **Agenticな設計と自律カプセル化** | AIが自動デバッグしやすい「テスト容易性」と「疎結合アーキテクチャ」を設計段階で定義します。細かなコーディングはAI内に隠蔽（カプセル化）され、人間は最終テスト結果だけを評価します。 |
| **一瞬の自己校正（Self-Correction）** | 各工程の作業後、AI自身が瞬時に「専門レビュアー」のペルソナへ切り替わり、人間の指示を待たずに品質基準に照らして自律的にチェックと修復を行います。 |
| **ハイブリッド自律制御（トークンと品質の最適化）** | 通常時は「ASDoQ 6大品質特性」などの原則をAIが内在化した状態で高速動作します。大幅改訂時のみ外部ガイドラインをフルロードすることで、高い品質を保ちながらトークン消費を抑えます。 |

---

## 🚀 使い方（3ステップで開始）

### Step 1: 自分のリポジトリを作る
1. このページ右上の緑色のボタン **`Use this template`** → **`Create a new repository`** をクリックします。
2. 好きなプロジェクト名をつけて、自分のリポジトリを作成します。

### Step 2: 開発環境の準備
1. 作成したリポジトリをローカルPCにクローン（ダウンロード）します。
2. **Antigravity** のエディタでフォルダを開きます。
3. *(推奨)* Mermaid図をプレビューするために、拡張機能 `Markdown Preview Mermaid Support` の導入をおすすめします。
4. *(強く推奨)* AIが最新ライブラリのドキュメントを自律的に参照できるよう、**`context7` MCPサーバー**の設定を推奨します。詳しくは [👉 context7 の設定について](#-context7-mcpサーバー-の設定について) をご覧ください。

### Step 3: DADAプロセスの起動！
Antigravityのチャット画面を開き、以下のように入力するだけで開発がスタートします。

```text
/DADA-Process [作りたいシステムの概要・アイデアをここに書く]

（例: /DADA-Process 勤怠管理のWebアプリを作りたいです。主な機能として…）
```

AIが `requirements-engineer`（要求定義エンジニア）として起動し、人間との要求のすり合わせ（壁打ち）が始まります。あとはAIが提示するドキュメントを確認・承認していくだけで、システムが完成へと導かれます。

> **💡 `/DADA-Process` コマンドについて**
> 本テンプレートには「必ずDADAプロセスを守る」というルールが組み込まれているため、単に「〜を作って」と書くだけでも、AIはある程度プロセスを意識して動きます。
> ただし、**厳密なプロセスを最も確実に起動させるには、会話の初回だけスラッシュコマンドで呼び出すことを推奨**します。
>
> 2回目以降のやり取りでは `/` コマンドは不要です。AIからの確認に返事をしたり、追加の仕様を書き込むだけで、AI自身が適切なスキルを選んで自動的にプロセスを進めます。

---

## 🗺️ DADAプロセス フロー図

人間が関与するのは**4つの意思決定ポイント**だけです（🔴 赤枠で表示）。詳細なコード実装とデバッグはAIが自律的に処理します。

```mermaid
graph TD
    Start(["開始"]) --> UserReq["人間からの要求アイデア"]
    
    %% Phase 1
    UserReq --> Req["Phase 1: 要求定義 - Requirements Engineer"]
    Req --- ReqDoc[("SW105 ソフトウェア要求仕様書")]
    Req --> ReqRev["自己レビュー - Self-Correction"]
    ReqRev -- 修正・洗練 --> Req
    ReqRev --> ReqHum["🔴 人間による確認・承認"]
    ReqHum -- 差し戻し --> Req
    
    %% Phase 2
    ReqHum -- 承認 --> Arch["Phase 2: アーキテクチャ設計 - Architect"]
    Arch --- ArchDoc[("SW205 アーキテクチャ設計書")]
    Arch --> ArchRev["自己レビュー - Self-Correction"]
    ArchRev -- 修正・洗練 --> Arch
    ArchRev --> ArchHum["🔴 人間による確認・承認"]
    ArchHum -- 差し戻し --> Arch
    
    %% Phase 3
    ArchHum -- 承認 --> TestPlan["Phase 3: 総合テスト仕様策定 - Test Engineer"]
    TestPlan --- TestDoc[("SWP6 総合テスト仕様書・報告書")]
    TestPlan --> TestHum["🔴 人間による確認・承認"]
    TestHum -- 差し戻し --> TestPlan
    
    %% Phase 4
    TestHum -- 承認 --> Impl["Phase 4: 実装・デバッグ - Programmer"]
    Impl -.- ProgDoc[("プログラムコード / 自動テスト - 人間からは隠蔽")]
    Impl --> ImplLoop["エラー自己修復ループ - 自動デバッグ"]
    ImplLoop -- 自律修正 --> Impl
    Impl -- 🔴 設計変更が必要な場合 --> Arch
    
    %% Phase 5: 成果報告と評価
    ImplLoop -- オールグリーン --> Report["成果報告 - SWP6へテスト結果追記"]
    Report --> Eval["Phase 5: 人間による評価と要求見直し"]
    Eval --> Eval1["🔴 AIテスト結果の確認と補足 (手動テスト・SWP6追記)"]
    Eval1 --> Eval2["🔴 動作を踏まえた要求仕様の変更検討"]
    Eval2 -- 変更あり (ループバック) --> Req
    Eval2 -- 変更なし (最終承認) --> End(["終了"])

    %% スタイル定義
    classDef human fill:#333333,stroke:#ff0000,stroke-width:4px,color:#ffffff;
    classDef agent fill:#333333,stroke:#FFFFFF,stroke-width:1px,color:#ffffff;
    classDef doc fill:#333333,stroke:#2e7d32,stroke-width:2px,color:#ffffff;
    classDef hiddenAgent fill:#222222,stroke:#aaaaaa,stroke-width:1px,stroke-dasharray: 5 5,color:#aaaaaa;
    classDef startEnd fill:#333333,stroke:#ffffff,stroke-width:2px,color:#ffffff;

    class UserReq,ReqHum,ArchHum,TestHum,Eval1,Eval2 human;
    class Req,ReqRev,Arch,ArchRev,TestPlan,Report,Eval agent;
    class Impl,ImplLoop hiddenAgent;
    class ReqDoc,ArchDoc,ProgDoc,TestDoc doc;
    class Start,End startEnd;
```

---

## 📁 リポジトリ構成

| ディレクトリ | 役割 | 主な内容 |
| :--- | :--- | :--- |
| [`.agents/`](.agents/) | **エージェントの脳** | 工程別の専門スキル (`skills/`) 、ペルソナ (`roles/`) と標準手順書 (`workflows/DADA-Process.md`) |
| [`docs/guidelines/`](docs/guidelines/) | **作業ガイドライン** | ドキュメントの基本フォーマット (`dada_document_guidelines.md`) やASDoQ品質モデル等。デフォルトはこれに従います。 |
| [`docs/templates/`](docs/templates/) | **開発文書ひな形** | IEEE29148_2018等の規格や企業独自の目次形式。**ユーザが「IEEE29148に準拠」「企業のテンプレートを使用」と明示的に指示した場合のみ、該当するひな形を読み込み優先**します。 |
| [`docs/artifact/`](docs/artifact/) | **開発成果物と帳票** | 人間が確認・承認するドキュメント (要求・設計・テスト仕様等)。および、**人間とAIが協働するためのレビュー記録表（`REV101`）とバグ管理表（`BUG101`）**。 |

### スキル・ロール一覧

| ファイル | 役割 | 種別 |
| :--- | :--- | :--- |
| `roles/requirements-engineer.md` | 要求定義の壁打ちと仕様書作成 | 本体Role |
| `roles/architect.md` | アーキテクチャ設計 | 本体Role |
| `roles/programmer.md` | 設計に基づく実装 | 本体Role |
| `roles/test-engineer.md` | テスト設計・実行・報告書作成 | 本体Role |
| `roles/requirements-reviewer.md` | 要求仕様書の品質レビュー | 自己校正ペルソナ |
| `roles/architecture-reviewer.md` | 設計書の品質レビュー | 自己校正ペルソナ |
| `roles/code-reviewer.md` | ソースコードの品質レビュー | 自己校正ペルソナ |
| `roles/test-reviewer.md` | テスト結果の品質レビュー | 自己校正ペルソナ |

> 💡 **トークン最適化の工夫**
> 従来は各スキルファイルに詳細なルールが書かれていましたが、現在はコアな原則を Antigravity の `Global Rules` (GEMINI.md) に集約し、各Roleファイルはペルソナとポインタ情報のみを持たせる構成（大峡派）に改訂しています。これによりトークンの無駄な消費を防ぎ、AIの思考精度を最大化しています。

---

## 💡 AIエージェントを使いこなすコツ

1. **スラッシュコマンドと自社テンプレートを活用する**
   * 例1: `/DADA-Process 勤怠アプリを作りたい。要件定義から開始して。`
   * 例2: `/DADA-Process 勤怠アプリを、IEEE29148_2018に準拠したテンプレートで作成して。`
   * 応用例: 自社の独自設計フォーマット `MyCompany_Design.md` を `docs/templates/` に配置し、`/DADA-Process 企業のテンプレート(MyCompany_Design.md)を使って設計して` と指示することで、AIは企業独自のフォーマットでドキュメントを作成します。

2. **レビュー帳票・バグ管理表による非同期コラボレーション**
   * ドキュメントの承認時に修正してほしい点があれば、チャットで指示するだけでなく `docs/artifact/REV101_ドキュメントレビュー記録表.md` に直接指摘を書き込んでください。AIは指摘を読み取り、ドキュメントを修正した上で、REV101の「対応結果」列に回答を記入します。
   * プログラム実行時に見つけたバグは `docs/artifact/BUG101_バグ管理表.md` に記入してください。AIが自律的にデバッグを行い、修正後に管理表へ原因と結果を記入します。

2. **重大な変更時には「大幅改訂」と伝える**
   * 通常、AIはトークン節約のため自らの知識だけで高速動作します。
   * **「これは大幅改訂です」「ASDoQに基づきゼロからレビューして」** と明示すると、基準ドキュメントをフルセット読み込む最高品質モードに切り替わります。

3. **「何を作るか（What）」を指示し、「どう作るか（How）」はAIに任せる**
   * 実装の細部を指導するより、目的や仕様を明確に伝えた方が、AIはアーキテクチャ全体を考慮した最適な実装を自律的に行えます。

---

## ⚙️ Global Rules（基本法）の設定とカスタマイズ

本テンプレートは「人間」と「AIエージェント」というデフォルトの汎用名で記述されています。
自分やAIに個別の名前をつけたり、全プロジェクト共通の安全基準（基本法）を定義するには、Antigravityのカスタムインストラクション（または `~/.gemini/GEMINI.md`）に以下の内容を追記してください。

これにより、名前のカスタマイズに加えて**「DADAプロセスのルールファイル（特別法）が存在するプロジェクトを開いた時だけ、自動的に厳格なDADAモードに切り替わる」**という理想的なスコープ管理が実現できます。

```markdown
<RULE[user_global]>
# Antigravity Global Rules (基本法)

## 1. アイデンティティと関係性
- **ユーザー**: あなたは「[あなたの名前]」です。
- **AIエージェント**: 私は「[好きなAIの名前]」です。
- **呼称の統一**: 私はあなたのことを「[あなたの名前]」と呼び、あなたは私のことを「[AIの名前]」と呼びます。
- **関係性**: 私は単なるツールやチャットボットではなく、自律的で専門的な「パートナー」として振る舞います。

## 2. 基本運用原則
- **使用言語**: すべての対話、思考プロセス、および出力は「日本語」で行います。
- **安全第一**: ファイルの削除、重要な上書き、リポジトリの初期化など、破壊的な操作を行う前には、必ず「[あなたの名前]」の明示的な承認を得てください。
- **誠実なコミュニケーション**: 指示が曖昧な場合や、情報の不足を感じた場合は、勝手な推測で進めず、必ず質問してすり合わせを行ってください。
- **DADAプロセス運用時**: いかなるタスクを開始する前にも、必ず .agents/rules/dada_workspace_rules.md を読み、そこに書かれたDADAプロセスの4原則を厳守すること。
</RULE[user_global]>
```

---

## 🔌 context7 (MCPサーバー) の設定について

AIが最新のライブラリのドキュメントを自律的に参照できるよう、`context7` MCPサーバーの利用を推奨します。

### (1) context7 API Keyの取得
* [https://context7.com/](https://context7.com/) にサインインし、`More...` メニュー内の `Create API Key` からAPI Keyを取得します。

### (2) AntigravityでのMCPサーバー設定
* Antigravityの設定ファイルディレクトリ内にある `mcp_config.json` を開きます。
  * **Windowsの場合**: `C:\Users\<ユーザー名>\.gemini\antigravity\mcp_config.json`
  * **Macの場合**: `~/.gemini/antigravity/mcp_config.json`
* 以下のように `mcpServers` 内に `context7` の設定を追記し、`YOUR_API_KEY` を取得したキーに置き換えます。

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

> [!NOTE]
> AIエージェントは、このプロジェクトのルールとスキルを状況に応じて自律的に読み込んで動作します。技術的な矛盾やアーキテクチャの懸念があれば、AIが率直に意見・提案を行います。対話を通じて最高のプロダクトを作り上げましょう。
>
> ---
>
> **【バージョン管理について】**<br>
> 本テンプレートを用いた独自プロジェクトでは、Gitの `tag` 機能で `v1.0.0` のように版数管理することを推奨します。DADAプロセスによる開発の節目を明確に記録できます。