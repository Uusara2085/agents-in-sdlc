---
title: "レッスン 5 - quality-checks スキルをカスタマイズして使う"
description: "既存の quality-checks スキルを確認し、結果の形式をカスタマイズして、フィルタリング機能を検証します。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書くことだけが開発ではありません。これまでにコードの動作を手動で検証し、命令ファイルを使って規約に従うよう Copilot を導きました。ここでは、テスト、lint、継続的インテグレーション (CI) のほかの作業を扱います。**エージェント スキル**を使うと、こうした作業の実行方法を Copilot に伝えられます。

このレッスンでは、次のことを行います。

- 既存の `quality-checks` スキルを確認します。
- 結果の形式をカスタマイズします。
- スキルを再読み込みして実行します。

## シナリオ

Tailspin Toys では、ユニットテスト、lint、型チェックに `quality-checks` スキルを使っています。チームは、実行結果を読みやすくするため、レポートを改善したいと考えています。

## 命令、スクリプト、リソース

エージェント スキルは、エージェントが必要に応じて読み込む、再利用可能なタスクの指示、実行可能なスクリプト、補助リソースをまとめたものです。基本的には、スキル名のフォルダーと、その中の `SKILL.md` で構成されます。Markdown には、スキルの名前と説明を定義する frontmatter、機能の概要、呼び出すタイミングのガイダンスを記載します。必要に応じて、スクリプトなどを含むサブフォルダーも追加できます。

> [!NOTE]
> 追加のファイルやフォルダーは必須ではありません。Tailspin Toys の `quality-checks` スキルには `SKILL.md` だけがあり、プロジェクトに用意されたコマンドを使います。

スキルは、チームで共有して再利用できるリポジトリの `.github/skills`、またはユーザー単位の `~/.copilot/skills` に配置できます。

## スキルを確認する

Tailspin Toys のチームが作成した `quality-checks` スキルを確認します。

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. 先頭の `name` と `description` を読みます。説明によって Copilot がスキルを呼び出すタイミングを判断します。
3. 命令を読み、テストと lint の手順を確認します。
4. **Results output formatting** セクションがまだないことを確認します。

## 変更前にスキルを実行する

Copilot CLI に、スキルを使って3つのチェックを実行するよう依頼します。

1. Interactive モードでフィルタリングの会話に戻ります。
2. 次のプロンプトを送ります。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 実行後のレポートを確認します。

## レポートをカスタマイズする

実行したチェック、成功・失敗の状態、ツールが報告した内容が分かるレポートに変更します。

1. `.github/skills/quality-checks/SKILL.md` を再度開きます。
2. ファイルの末尾に次のセクションを追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルが自動的に保存されたことを確認します。

## 更新したスキルを実行する

Copilot CLI は、会話を再起動せずに編集済みのスキルを再読み込みできます。

1. `/skills reload` を入力します。
2. 変更前と同じプロンプトを送ります。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 実行後のレポートを読み、最初の結果と比較します。

## まとめと次のステップ

既存のエージェント スキルをカスタマイズして使いました。

- ユニットテスト、lint、型チェックを実行する `quality-checks` スキルを確認しました。
- 結果の形式をカスタマイズしました。
- スキルを再読み込みして実行しました。

この変更はフィルタリング機能の PR に含めます。次は[Playwright MCP サーバーを使って Copilot にサイトを操作させます][next-lesson]。

## スキルの例

コミュニティによる次の例は参考資料であり、追加の課題ではありません。

- [Agent Skills 仕様][skill-spec]
- [コントリビューション ワークフロー: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とエクスポート スクリプト: `drawio`][drawio-example]
- [ブラウザー テスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
