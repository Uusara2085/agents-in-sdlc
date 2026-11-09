---
title: "レッスン 6 - Playwright MCP で機能を検証する"
description: "Copilot CLI で Playwright MCP を設定し、ブラウザーからフィルタリング機能を確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

コードを書くことだけが開発ではありません。データや外部サービスと連携し、Copilot が使える自動化ツールを追加する必要もあります。MCP サーバーを使うと、Copilot CLI に組み込まれていないツールやサービスを利用できます。

このレッスンでは、次のことを行います。

- Model Context Protocol (MCP) と Copilot CLI での利用方法を確認します。
- まだ設定されていない場合は Playwright MCP サーバーを追加します。
- エージェントにブラウザーを操作させ、フィルタリング機能を確認します。

## シナリオ

ユニットテストやエンドツーエンド テストは重要ですが、UI の変更を検証するには、ユーザーのように実際の UI を操作することも必要です。Copilot が作業中の Web サイトを使えるようにし、期待どおりの動作を確認します。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部のツールやサービスと通信するための仕組みです。MCP を通じて最新情報にアクセスしたり、エージェントに操作を依頼したりできます。

MCP サーバーは、AI エージェントと外部ツールやサービスをつなぎます。たとえば、次のようなサーバーがあります。

- **[GitHub MCP Server][github-mcp]**: GitHub リポジトリ、Issue、プルリクエストを管理する API を利用できます。
- **[Playwright MCP Server][playwright-mcp-server]**: Playwright を使ったブラウザー自動化機能を利用できます。

GitHub は、MCP エコシステムの発見や貢献を促す [MCP registry][mcp-registry] をホストしています。

> [!CAUTION]
> MCP サーバーもほかの依存関係と同様に扱ってください。使用前にソース コードと発行元を確認し、セキュリティへの影響を検討します。

## Playwright MCP サーバーを追加する

Copilot CLI に Playwright MCP がまだ設定されていない場合は、サーバーを追加します。

> [!NOTE]
> Playwright MCP がすでに設定されている場合は、ここでの設定手順を省略して次のセクションに進みます。

1. Codespace に戻ります。
2. Copilot CLI で次のコマンドを入力し、MCP サーバーの追加画面を開きます。

   ```plaintext
   /mcp add
   ```

3. 名前に `playwright` と入力して <kbd>Tab</kbd> を押します。
4. サーバーの種類が **STDIO** であることを確認し、<kbd>Enter</kbd>、次に <kbd>Tab</kbd> を押します。
5. **Command** ダイアログに次の内容を貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Mac では <kbd>Control</kbd>+<kbd>S</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>S</kbd> を押して保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを閉じます。

## Playwright で機能を確認するよう Copilot に依頼する

これまでは機能を手動で確認しました。今度は Playwright MCP サーバーを使って、同じ確認を Copilot に依頼します。

1. Copilot に次のプロンプトを送ります。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> Copilot は通常、自動的に MCP サーバーを判断します。ここでは Playwright MCP を使うよう明示し、結果の一貫性を高めます。

2. Copilot がブラウザーで機能を検証する手順を確認します。
3. 報告を読み、すべてが期待どおりに動作することを確認します。

Copilot はサーバーを起動し、Playwright で Web サイトを操作し、サーバーを停止して結果を報告します。

## まとめと次のステップ

Copilot CLI から Playwright MCP サーバーを使い、実際のブラウザーで機能を確認しました。

- MCP と Copilot CLI での利用方法を確認しました。
- 未設定の場合に Playwright MCP サーバーを追加しました。
- エージェントにブラウザーを操作させ、フィルタリング機能を確認しました。

次は、スキルとブラウザー ツールを組み合わせる [QA カスタム エージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ注目されているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
