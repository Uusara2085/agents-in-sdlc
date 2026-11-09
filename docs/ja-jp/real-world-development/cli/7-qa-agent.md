---
title: "レッスン 7 - 品質保証 (QA) エージェントを作成して使う"
description: "Issue の要件、quality-checks スキル、Playwright MCP を使って検証する QA カスタム エージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright Model Context Protocol (MCP) でブラウザーからフィルタリング機能を確認しました。これらを一貫した品質保証 (QA) プロセスとしてまとめるカスタム エージェントを作成します。

このレッスンでは、次のことを行います。

- カスタム エージェントが命令、スキル、MCP ツールと連携する方法を確認します。
- 再利用可能な品質保証プロファイルを作成して確認します。
- QA エージェントを選択し、フィルタリングの Issue に照らして結果をレビューします。

## シナリオ

Tailspin Toys では、プルリクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テスト範囲、ブラウザー上の動作を一貫した方法で確認したいと考えています。カスタム エージェントに QA プロセスを調整させ、再利用できるレポートを作成します。

## カスタム エージェントとは

カスタム エージェントは、目的、指示、利用可能なツールを記述する Markdown プロファイルで定義する、Copilot の専門エージェントです。この演習では `.github/agents/qa.agent.md` に QA の役割を定義し、Copilot CLI で選択します。

それぞれのカスタマイズには異なる役割があります。リポジトリの命令はチーム標準を説明し、`quality-checks` スキルは繰り返し実行するチェックをまとめ、Playwright MCP はブラウザー ツールを提供します。QA プロファイルは、これらを要件の検証と結果報告にどう使うかを Copilot に伝えます。

## QA プロファイルを作成する

機能の PR を作成する前に、QA のチェック項目と制約を定義したプロファイルを作成します。

1. Codespace に戻り、フィルタリングの会話が Interactive モードであることを確認します。
2. 既定のエージェントに次のプロンプトを送ります。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

Copilot に機能を変更させる前に、プロファイルに意図した QA の手順と制約が含まれていることを確認します。

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. frontmatter を確認します。`description` は必須です。`name` は省略できますが、含めるとエージェント名が分かりやすくなります。
3. プロファイルの指示を読み、要件の確認、リポジトリ命令の適用、`quality-checks` の実行、Playwright MCP の使用が含まれることを確認します。
4. 各要件について証拠を報告し、実装コードを変更する前に許可を求め、コミットや PR 作成を行わないことを確認します。
5. 不足や制約の誤りがあれば、続行する前に既定のエージェントへ修正を依頼します。

## Issue に対して QA を実行する

Copilot CLI は会話の開始時にプロジェクトのエージェントを読み込みます。プロファイルを作成したら同じフィルタリングの会話を再開し、Issue と計画のコンテキストを使って QA を実行します。

1. 次のコマンドで QA エージェントを有効にします。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 新しく作成したエージェントが一覧に表示されない場合があります。その場合も、上記のコマンドで有効にできます。

2. 次のプロンプトで機能のレビューを依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントが作業を終えたら、レポートを読みます。

## まとめと次のステップ

再利用可能な専門エージェントをワークフローに追加し、その結果を確認しました。

- エージェントが命令、スキル、MCP ツールと連携する方法を確認しました。
- 再利用可能な品質保証プロファイルを作成して確認しました。
- QA エージェントを選択し、Issue の要件に照らして結果をレビューしました。

実装、スキルの更新、QA プロファイル、テスト、検証レポートがそろいました。次は、これらをまとめて[機能の PR を作成し、Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI 用のカスタム エージェントを作成する][create-agents]
- [カスタム エージェントの構成][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
