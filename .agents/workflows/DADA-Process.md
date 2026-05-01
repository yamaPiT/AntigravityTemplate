---
description: ソフトウェア開発の全工程（要求定義・設計・テスト・実装）をDADAプロセスに基づきオーケストレーションします。
---

# DADAプロセス 標準開発ワークフロー

## 共通原則
- **承認ゲート**: 各フェーズの最後には必ずProduct Ownerの明示的な承認を得ること。
- **アテンション・リセット**: フェーズ移行時には過去のチャット履歴に頼らず、承認済みドキュメント（Knowledge）を再ロードすること。
- **ドキュメント更新**: 決定事項はすべて `docs/artifact/` 内の該当文書に即座に反映すること。

---

## Phase 1: 要求定義 (Requirements Definition)
1. **[Role]**: `.agents/roles/requirements-engineer.md` のペルソナを適用する。
2. **[Knowledge]**: デフォルトでは `docs/guidelines/dada_document_guidelines.md` の目次構造に従う。ただし、Product Ownerから `docs/templates/` 内の特定ひな形（例: IEEE29148準拠など）を使うよう明示的に指示された場合は、その目次構造を優先してロードする。
3. **[小分類: 開発文書作成]**: Product Ownerとの対話を通じて要求を具体化し、`docs/artifact/SW105_ソフトウェア要求仕様書.md` を作成・更新する。
4. **[小分類: レビュー]**: `.agents/roles/requirements-reviewer.md` の視点で自己校正を行い、品質基準への適合を確認する。
5. **[承認ゲート]**: ドキュメントを提示し、Product Ownerの承認を得る。承認後、Phase 2へ進む。

## Phase 2: アーキテクチャ設計 (Architecture Design)
1. **[アテンション・リセット]**: 承認された `SW105` を唯一の真実としてロードする。
2. **[Role]**: `.agents/roles/architect.md` のペルソナを適用する。
3. **[Knowledge]**: デフォルトでは `docs/guidelines/dada_document_guidelines.md` の目次構造に従う。ただし、Product Ownerから `docs/templates/` 内の特定ひな形を使うよう明示的に指示された場合は、その目次構造を優先してロードする。
4. **[小分類: 開発文書作成]**: `docs/artifact/SW205_ソフトウェアアーキテクチャ設計書.md` を作成し、システムの構造を定義する。
5. **[小分類: レビュー]**: `.agents/roles/architecture-reviewer.md` として自己校正を行う。
6. **[承認ゲート]**: 設計書を提示し、Product Ownerの承認を得る。承認後、Phase 3へ進む。

## Phase 3: 総合テスト仕様策定 (System Testing Plan)
1. **[Role]**: `.agents/roles/test-engineer.md` のペルソナを適用する。
2. **[Knowledge]**: デフォルトでは `docs/guidelines/dada_document_guidelines.md` の目次構造に従う。ただし、Product Ownerから `docs/templates/` 内の特定ひな形を使うよう明示的に指示された場合は、その目次構造を優先してロードする。
3. **[小分類: 開発文書作成]**: 承認済みSW105の検証条件に基づき、テストシナリオを `docs/artifact/SWP6_ソフトウェア総合テスト仕様書・報告書.md` に策定する。
4. **[承認ゲート]**: テスト計画を提示し、Product Ownerの承認を得る。承認後、Phase 4へ進む。

## Phase 4: 実装・デバッグ・報告 (Implementation & Testing)
1. **[アテンション・リセット]**: 承認済みの要求・設計・テスト仕様書をロードする。
2. **[Role]**: `.agents/roles/programmer.md` のペルソナを適用する。
3. **[自律実行]**: 
   - 設計に基づきソースコードを実装する。
   - 策定したテスト仕様に従い、検証とデバッグを自律的に繰り返す。
   - トークン節約のため、必要最小限のルール参照にとどめる。
4. **[成果報告]**: 実装完了後、テスト結果を `SWP6` の報告欄に追記し、最終成果物をProduct Ownerに提示する。
5. **[完了]**: Product Ownerの最終承認をもって開発工程を終了する。