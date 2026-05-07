---
description: ソフトウェア開発の全工程（要求定義・設計・テスト・実装）をDADAプロセスに基づきオーケストレーションします。
---

# DADAプロセス 標準開発ワークフロー

## 共通原則
- **プロセスの遵守**: 基本原則（承認ゲート、アテンション-リセット等）はすべて `.agents/rules/dada_workspace_rules.md` に従うこと。
- **ドキュメント準拠性**: 基本は `docs/guidelines/dada_document_guidelines.md` に従う。ただしProduct Ownerから「IEEE29148_2018に準拠」等の規格指定や、「企業のテンプレートに従う」等の指示があった場合は、`docs/templates/` 配下の該当ひな形ファイルを読み込み、その構造を絶対的に優先すること。

---

## Phase 1: 要求定義 (Requirements Definition)
1. **[作成]**: `.agents/roles/requirements-engineer.md` を適用し、`docs/artifact/SW105_ソフトウェア要求仕様書.md` を作成。
2. **[レビュー]**: `.agents/roles/requirements-reviewer.md` を適用。指摘を `docs/artifact/REV101_Requirements.md` に記録。
3. **[修正・記録]**: **`.agents/roles/requirements-engineer.md` を適用し**、指摘を修正して `REV101_Requirements.md` に対応結果を記録する。
4. **[承認ゲート]**: Product Ownerの承認を得る。承認後、スキル `context-reset` を実行し、Phase 2へ遷移する。

## Phase 2: アーキテクチャ設計 (Architecture Design)
1. **[作成]**: `.agents/roles/architect.md` を適用し、`docs/artifact/SW205_ソフトウェアアーキテクチャ設計書.md` を作成。
2. **[レビュー]**: `.agents/roles/architecture-reviewer.md` を適用。指摘を `docs/artifact/REV101_Design.md` に記録。
3. **[修正・記録]**: **`.agents/roles/architect.md` を適用し**、指摘を修正して `REV101_Design.md` に対応結果を記録する。
4. **[承認ゲート]**: Product Ownerの承認を得る。承認後、スキル `context-reset` を実行し、Phase 3へ遷移する。

## Phase 3: 総合テスト仕様策定 (System Testing Plan)
1. **[作成]**: `.agents/roles/test-engineer.md` を適用し、`docs/artifact/SWP6_ソフトウェア総合テスト仕様書・報告書.md` を策定。
2. **[レビュー]**: `.agents/roles/test-reviewer.md` を適用。指摘を `docs/artifact/REV101_Test.md` に記録。
3. **[修正・記録]**: **`.agents/roles/test-engineer.md` を適用し**、指摘を修正して `REV101_Test.md` に対応結果を記録する。
4. **[承認ゲート]**: Product Ownerの承認を得る。承認後、スキル `context-reset` を実行し、Phase 4へ遷移する。

## Phase 4: 実装・デバッグ・報告 (Implementation & Testing)
1. **[自律実装]**: `.agents/roles/programmer.md` を適用。`unit-test-generator` スキルを活用し自律的にデバッグを行う。
2. **[バグ対応]**: バグを修正した際は、必ず `docs/artifact/BUG101_バグ管理表.md` に記録し、解決済にすること。
   - **【設計へのループバック】**: バグ修正に伴い、アーキテクチャ設計（SW205）の変更が必要と判断した場合は、独断で実装を修正せず、必ず「Phase 2: アーキテクチャ設計」に戻り、設計書の修正と承認からやり直すこと。
3. **[レビュー]**: 成果物の完成後、報告の前に `.agents/roles/code-reviewer.md` を適用して自己検閲（Self-Correction）を行う。コーディング規約への準拠確認や品質評価を行い、必要なら再度プログラマーとして修正を行う。
4. **[完了報告]**: オールグリーン達成後、Product Ownerに報告。承認後、スキル `context-reset` を実行し、Phase 5へ遷移する。

## Phase 5: 人間による評価と要求見直し (Human Evaluation & Requirement Review)
1. **[評価1: テストの確認とバグ対応]**: Product Owner（人間）がプログラムを実際に実行して評価する。AIが自動テストできない領域のテスト結果は `SWP6` に人間が追記する。また、人間がバグを発見して `docs/artifact/BUG101_バグ管理表.md` に記載した場合、AIはそれを読み取ってPhase 4に戻りデバッグを行い、修正後に `BUG101` に「原因と修正内容」を記入（解決済に）すること。
2. **[評価2: 要求仕様の変更検討]**: 実際のプログラムの動作を踏まえて要求仕様を変更したくなった場合、プロセスは**「Phase 1: 要求定義」にループバック**する。Product OwnerがAIに新しい要求を自然言語で指示するか、Product Owner自身が直接要求仕様書(`SW105`)を書き直す。
3. **[再設計と実装への波及]**: 要求仕様が変更・確認された後は、自動的に**「Phase 2: アーキテクチャ設計」へ遷移し**、アーキテクチャ設計のやり直し（変更）を行う。これに伴い実装もやり直される。
4. **[完了]**: 追加の要求変更がなく、Product Ownerの最終承認が得られた段階で、開発工程を完全に終了する。