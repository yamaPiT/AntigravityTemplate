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
   - **[設計差し戻し]**: デバッグの過程で設計変更が必要になった場合は、必ず「Phase 2: アーキテクチャ設計」に戻り、設計書を書き直してProduct Ownerの承認を求めること。
   - **[実装やり直し]**: アーキテクチャ設計が変更された場合は、必ずその新しい設計に完全に合致するよう実装をやり直すこと。
4. **[成果報告]**: 実装完了後、テスト結果を `SWP6` の報告欄に追記し、最終成果物をProduct Ownerに提示する。
5. **[フェーズ移行]**: 成果物提示後、Phase 5へ進む。

## Phase 5: 人間による評価と要求見直し (Human Evaluation & Requirement Review)
1. **[評価1: テストの確認と補足]**: Product Owner（人間）がプログラムを実際に実行して評価する。AIが自動テストできない領域（UIの感覚的な確認やハードウェア連携など）については、人間がテストを行い、その結果を `docs/artifact/SWP6_ソフトウェア総合テスト仕様書・報告書.md` に追記する。
2. **[評価2: 要求仕様の変更検討]**: 実際のプログラムの動作を踏まえて要求仕様を変更したくなった場合、プロセスは「Phase 1: 要求定義」にループバックする。
   - Product OwnerがAIに新しい要求を自然言語で指示するか、Product Owner自身が直接要求仕様書(`SW105`)を書き直す。
3. **[再設計と実装への波及]**: 要求仕様が変更・確認された後は、自動的に「Phase 2: アーキテクチャ設計」へ進み、アーキテクチャ設計のやり直し（変更）を行う。これに伴い実装もやり直される。
4. **[完了]**: 追加の要求変更がなく、Product Ownerの最終承認が得られた段階で、開発工程を完全に終了する。