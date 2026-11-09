---
title: "レッスン 4 - カスタム命令で Copilot を導く"
description: "リポジトリの命令を確認してドキュメント標準を追加し、フィルタリング機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときは、コンテキストが重要です。タスクの進め方に決まりがある場合は、そのガイダンスを Copilot が参照できるようにします。[命令ファイル][instruction-files]では、求めるコードだけでなく、その構成方法も説明できます。フィルタリング機能を実装したので、Copilot が使った命令を確認し、ドキュメント標準を追加して、コードに適用します。

このレッスンでは、次のことを行います。

- リポジトリの命令とパスに応じた命令がエージェントに適用される方法を確認します。
- コーディング標準に従うため、命令ファイルを更新します。
- 命令ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には開発ガイドラインがあります。

- コメントには、コードの言い換えではなく、意図や自明でない判断を記述します。
- `db/` と `src/lib/` の公開関数には、目的、パラメーター、戻り値を説明する TypeScript Documentation (TSDoc) / JavaScript Documentation (JSDoc) を記述します。`db` 引数を注入する場合は、その説明も含めます。
- 再利用可能な Astro コンポーネントでは `Props` の契約を説明し、関連コードが変わったらコメントも更新します。
- 既存の書式と lint のガイダンスを維持します。

## 命令ファイル

カスタム命令は、コーディング規約やコメントなどの希望を Copilot に伝えます。

- `.github/copilot-instructions.md` は、リポジトリへのすべてのリクエストに適用するプロジェクト全体の情報を記載します。
- `.github/instructions/*.instructions.md` は、言語、ファイル形式、タスクごとのガイダンスを記載します。

> [!NOTE]
> 環境によって、ほかの命令形式のサポート状況は異なります。形式を利用する前に[カスタム命令のサポート][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム命令ファイルを確認する

Copilot がプロジェクトで使う命令を読み、全体に適用されるガイダンスを確認します。

1. Codespace に戻ります。
2. Codespaces のエディターで `.github/copilot-instructions.md` を開き、プロジェクトの説明と全体のコーディング ガイダンスを確認します。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの命令を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開き、`applyTo` が命令を適用するファイルを決める glob であることを確認します。
5. `.github/instructions/drizzle.instructions.md` を開き、ほかの命令ファイルやプロジェクト ファイルへのリンクを確認します。これらのパスは命令ファイルの場所からの相対パスです。

## チームのガイダンスに合わせて命令を更新する

`copilot-instructions.md` を更新し、新しく生成する TypeScript に TSDoc コメントを追加する標準を設定します。

1. `.github/copilot-instructions.md` の **Code formatting guidance** セクションを開きます。
2. 最後の箇条書きに次の行を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

変更は自動的に保存されます。

## 更新したガイダンスを適用する

Copilot CLI は会話の開始時にリポジトリの命令を読み込みます。フィルタリングのコンテキストを保ったまま、新しい命令を読み込むため会話を再開します。

1. フィルタリングの会話が開いている場合は `/exit` を入力します。Copilot CLI は会話を自動的に保存します。
2. `game-filters-cli` ブランチのリポジトリ ルートで、保存した会話を再開します。

   ```bash
   copilot --resume
   ```

3. プロンプトが表示されたらフィルタリングの会話を選び、`game-filters-cli` ブランチに切り替わっていることを確認します。
4. Copilot に次のプロンプトを送ります。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

5. `/diff` を入力し、変更された TypeScript ファイルを確認します。追加された TSDoc コメントがコードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が命令ファイルからコンテキストを取得する方法を確認し、新しい標準を機能に適用しました。

- リポジトリの命令とパスに応じた命令がエージェントに適用される方法を確認しました。
- コーディング標準に従うため、命令ファイルを更新しました。
- 命令ファイルがコードに与える影響を確認しました。

次は[再利用可能な quality-checks スキルをカスタマイズして実行します][next-lesson]。

## リソース

- [Copilot CLI にカスタム命令を追加する][instruction-files]
- [カスタム命令のサポート][custom-instructions-support]
- [効果的なカスタム命令を作るためのベスト プラクティス][instructions-best-practices]
- [命令ファイルなどを集めた Awesome Copilot][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
