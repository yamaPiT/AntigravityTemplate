# Google Antigravity 向け DADA (Document and Agent Driven Agile) 開発プロセステンプレート

本リポジトリは、Google Antigravity 向けに最適化された、AIエージェントと人間が高度に協調し、高品質なソフトウェアを高速に構築するための 「DADA開発プロセステンプレート」です。

従来のagent codingでは、次の2点の弱点がありました。
#### (1)「一時メモリ」で消えてしまう性質（揮発性）
会話により生成した要求仕様や設計などは、「コンテキストウィンドウ」と呼ばれる一時メモリ上に置かれるので、対話が進んだり新しいタスクに移ったりすると、古い情報から押し出されて消えます。だから、整合性を保つシステム開発が困難でした。
#### (2)システム側の「ハードコーディング」
一時メモリから消えることを防止するために、システムは、「実装計画（Implementation_plan.md）」と「手順書（walkthrough.md）」を作り、ファイルとして記録します。しかし、システム側の都合で作られる内容に過ぎず、ユーザの制御ができません。

**そこで、DADA (Document and Agent Driven Agile) 開発プロセスを提案します。DADAプロセスは、ドキュメント中心主義をとります。**
- ユーザの要求を逐次、要求仕様書に反映する。
- 更新された要求仕様書に基づき、ソフトウェアアーキテクチャ設計書を作成する。これにより、アーキテクチャは、常に最適化されている。
- ソフトウェアアーキテクチャ設計書に基づいて、プログラムを作成する。デバッグは自動で行われるが、設計変更が必要な場合は、ソフトウェアアーキテクチャ設計書が更新される。
- テスト仕様とテスト実行結果は、総合テスト仕様書・報告書にまとめられる。

ドキュメント中心主義で開発を進めることで、agent codingの質が高まることが期待できます。

---

## 1. コンセプト：DADA プロセス

```mermaid
graph TD
    Start(["開始"]) --> UserReq["人間からの要求"]
    UserReq["人間からの要求"] --> Req["ステップ1: 要求定義<br>(Requirements Engineer)"]
    Req --- ReqDoc[("要求仕様書")]
    Req -->|要求仕様書| UserReq
    Req --> ReqRev["要求レビュー<br>(Requirements Reviewer)"]
    ReqRev -- 修正・洗練 --> Req
    ReqRev --> ReqHum["人間によるレビュー<br>(User Review)"]
    ReqHum -- 修正依頼 --> Req
    ReqHum --> Arch["ステップ2: アーキテクチャ設計<br>(Architect)"]
    
    Arch --- ArchDoc[("ソフトウェアアーキテクチャ設計書")]
    Arch --> ArchRev["設計レビュー<br>(Architecture Reviewer)"]
    ArchRev -- 修正・洗練 --> Arch
    ArchRev --> ArchHum["人間によるレビュー<br>(User Review)"]
    ArchHum -- 修正依頼 --> Arch
    ArchHum --> Impl["ステップ3: 実装<br>(Programmer)"]
    
    Impl --- ProgDoc[("プログラム")]
    Impl --> ImplRev["実装レビュー<br>(Code Reviewer)"]
    ImplRev -- 修正・洗練 --> Impl
    Impl --> Arch
    ImplRev --> Test["ステップ4: テスト<br>(Test Engineer)"]
    
    Test --- TestDoc[("総合テスト仕様書・報告書")]
    Test --> TestRev["テストレビュー<br>(Test Reviewer)"]
    TestRev -- 修正・洗練 --> Test
    Test -- 修正依頼 --> Impl
    Test -- 設計変更依頼 --> Arch
    
    TestRev --> Approve["人間による最終評価・終了"]
    Approve -->|フィードバック| Req
    Approve --> End(["終了"])

    %% スタイル定義 (背景色を尊重し、枠線で役割を完結)
    classDef human fill:#333333,stroke:#ff0000,stroke-width:4px,color:#ffffff;
    classDef agent fill:#333333,stroke:#FFFFFF,stroke-width:1px,color:#ffffff;
    classDef doc fill:#333333,stroke:#2e7d32,stroke-width:2px,color:#ffffff;
    classDef startEnd fill:#333333,stroke:#ffffff,stroke-width:2px,color:#ffffff;
    
    class UserReq,ReqHum,ArchHum,Approve human;
    class Req,ReqRev,Arch,ArchRev,Impl,ImplRev,Test,TestRev agent;
    class ReqDoc,ArchDoc,ProgDoc,TestDoc doc;
    class Start,End startEnd;

    %% 凡例 (小型化)
    subgraph Legend ["凡例"]
        direction TB
        L1["AI"]:::agent
        L2["人"]:::human
        L3[("成果物")]:::doc
    end

```

-   **コード先行の絶対禁止**: まず「要求」と「設計」をドキュメントで合意し、その後にコードを実装します。
-   **エージェントによる自律的な改善**: 実装やテストの工程において、エージェントは自律的にプログラムの改訂やデバッグを行います。この際、根本的な解決のために設計の見直しが必要と判断した場合、エージェントは自律的にアーキテクチャ設計工程（ステップ2）へ戻り、設計書を更新した上で、再び実装・テストを進めます。
-   **自律的かつ統合された自己品質担保 (Self-Correction)**: トークン消費と処理時間を最小化するため、明示的な別エージェント（Reviewers）を都度呼び出すのではなく、作業エージェント自身が瞬時に「専門レビュアー」のペルソナへ切り替わり、ASDoQ文書品質モデルに基づく自己校正を自律的・高速に行います。図上のレビュアーは、このシステム内の「自己レビュープロセス」を表現しています。

---

## 2. リポジトリ構成（エコシステム）
各ディレクトリには、AIが迷いなく自律的に動作するための「知識」と「ツール」が配置されています。

| ディレクトリ | 役割 | 主要な内容 |
| :--- | :--- | :--- |
| [`.agents/`](.agents/) | **エージェントの脳** | 工程別の専門スキル (`skills/`) と標準手順書 (`workflows/`) |
| [`docs/`](docs/) | **ナレッジ・ベース** | ドキュメント作成ガイドライン、ASDoQ品質モデル、開発ガイド |
| [`doc/`](doc/) | **開発成果物** | 要求仕様書(SW105)、ソフトウェアアーキテクチャ設計書(SW205)、テスト報告書(SWP6) 等 |
| [`.cursor/`](.cursor/) | **エディタ制御** | エージェントが常に守るべき共通ルール (`project-rules.mdc`) |

---

## 3. クイックスタート：開発の始め方
新機能の追加や修正を行う際は、以下の流れでコマンドを起動してください。

1. **ワークフローの起動**: 
   チャット欄で `/DADA-Process` を入力・実行します。
2. **要求の提示**: 
   `requirements-engineer` と対話し、要求仕様書をドラフトします。
3. **自律的進行**: 
   AIが各ステップのスキルを読み込み、設計・実装・テストを順次進めます。
4. **評価と承認**: 
   最終的な「ソフトウェア総合テスト報告書」を確認し、開発完了を承認します。

---

## 4. 高度な運用シナリオ
### トークン最適化と規格準拠のハイブリッド
AIエージェントは通常、軽量な [ドキュメント構成ガイドライン](docs/process/dada_document_guidelines.md) に基づきスピーディーに動作します。ただし、「根本的なレビューをお願いします」という指示があった場合に限り、規格資料（ESPR, IEEE）のエッセンスを要約したマークダウン形式のドキュメントや、開発文書のサンプルを`docs/process/` フォルダから読み込み、品質基準を高めて、開発文書を校正します。

### 既存資産の移行
既存の仕様書やコードがある場合は、`doc/` および `src/` フォルダへ配置し、エージェントに「既存資産を理解して差分開発を開始して」と指示してください。

---

## 6. カスタマイズ：名称と役割の設定
本テンプレートでは、便宜上、人間に **「マサ（Product Owner）」**、AIエージェントに **「ハル（Technical Partner）」** という名称を付与しています。

他プロジェクトや組織で本テンプレートを使用する際は、以下のいずれかの対応を推奨します。

-   **(1) 名称の変更**: 
    以下のファイルに記述されている「マサ」「ハル」を、実際のプロジェクトメンバー名や任意の愛称に一括置換してください。
    - [`.cursor/rules/project-rules.mdc`](.cursor/rules/project-rules.mdc)
    - [`.agents/skills/`](.agents/skills/) 配下の各 `SKILL.md`
    - [`docs/process/dada_document_guidelines.md`](docs/process/dada_document_guidelines.md)
    - [`docs/asdoq_model_markdown.md`](docs/asdoq_model_markdown.md)
    - [`docs/agent_development_guide.md`](docs/agent_development_guide.md)
    - [`README.md`](README.md)
-   **(2) 固有名詞の排除**: 
    「マサ」を「Product Owner / User」に、「ハル」を「AI Assistant / Agent」に置き換えることで、よりニュートラルな運用が可能です。

---

## 7. 開発環境とツール
-   **Mermaid図の表示**: VS CodeやCursorで図表を美しく表示するために [Markdown Preview Mermaid Support](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced) の導入を推奨します。
-   **相対パスの徹底**: 本テンプレート内の全ての参照は相対パス化されており、どのディレクトリに配置しても、フォルダ名を変更しても、即座に動作可能です。

---

> [!NOTE]
> あなたのパートナーであるAIエージェントは、このプロジェクトのルールとスキルを常に読み込んでいます。技術的な矛盾があれば率直に提案しますので、対話を通じて最高のプロダクトを作り上げましょう。