---
title: "演習 3 - Playwright MCP サーバーで機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: エージェント モード][previous-lesson] · [次のレッスン: カスタム エージェント →][next-lesson]

agent mode でフィルタリング機能を実装しました。プルリクエストを作成する前に、ブラウザーで動作を確認します。Playwright MCP サーバーを接続して、Copilot に実際のブラウザーを操作させ、機能をテストしてからブランチを公開し、PR を作成します。

この演習では、次のことを行います。

- Model Context Protocol (MCP) と MCP サーバーが Copilot にツールを追加する仕組みを確認します。
- Playwright MCP サーバーをワークスペースに追加します。
- Copilot にブラウザーでフィルタリング機能をテストさせます。
- ブランチを公開し、フィルタリングの PR を作成します。

## Model Context Protocol (MCP) とは

MCP は、Copilot がエディターの外部にあるツールやサービスを使うための標準的な方法です。MCP サーバーを介してリソースから最新情報を取得したり、ツールを使って操作したりできます。

![コンテキスト、大規模言語モデル (LLM)、MCP サーバーや VS Code 拡張機能が提供するツールと連携する agent mode の図。](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) は、AI エージェントが外部のツールやサービスと通信できるようにします。よく使われる MCP サーバーには、GitHub リポジトリを管理する [GitHub MCP Server](https://github.com/github/github-mcp-server) と、ブラウザー自動化を提供する [Playwright MCP Server](https://github.com/microsoft/playwright-mcp) があります。GitHub は [MCP registry](https://github.com/mcp) をホストしています。

> [!CAUTION]
> MCP サーバーもほかの依存関係と同様に扱ってください。使用前にソース コードと発行元を確認し、セキュリティへの影響を検討します。信頼できるサーバーだけを使い、機密リソースや操作へのアクセスには注意してください。

## MCP の構成を確認する

`.vscode/mcp.json` は、VS Code ワークスペースで利用する MCP サーバーを設定します。

1. Codespace で `.vscode/mcp.json` を開きます。
2. 次の `github` サーバーがすでに設定されていることを確認します。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

このエントリはテンプレートに含まれているため、前の演習で Copilot が Issue のバックログを読み取れました。[リモート GitHub MCP サーバー][remote-github-mcp-server]を使い、HTTP 経由で接続します。Copilot が初めてツールを使うときに GitHub で認証します。

## Playwright MCP サーバーを追加する

Playwright MCP サーバーは Copilot が操作できるブラウザーを提供します。

1. `.vscode/mcp.json` の `github` と並べて `playwright` エントリを追加し、ファイルを次のようにします。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. ファイルを保存します。

`github` はリモート サーバーですが、`playwright` はローカル サーバーです。VS Code が `npx @playwright/mcp@latest` を実行して起動します。Codespace にはブラウザー画面を表示するデスクトップがないため、`--headless` を指定します。

> [!NOTE]
> Tailspin Toys ではエンドツーエンド テスト用に Playwright を使っているため、通常ブラウザーはすでにインストールされています。ブラウザーがないと Copilot が報告した場合は、`npx playwright install chromium` を実行して再試行します。

## サーバーを起動して信頼する

VS Code は MCP サーバーを必要に応じて起動し、初回利用時に信頼するか確認します。

1. `.vscode/mcp.json` の `playwright` エントリの上に表示される **Start** を選択します。
2. 信頼確認が表示されたら、設定を確認してサーバーを信頼します。

手動で起動する必要はありません。省略した場合は、次の手順で Copilot がサーバーを使うときに VS Code が起動します。

## フィルタリング機能をテストする

Playwright MCP を使うと、Copilot はブラウザーでページを開き、移動し、フィルターを適用して、結果を報告できます。サーバーとアプリを起動した状態で、次のプロンプトを Copilot に送ります。

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot は Playwright MCP でブラウザーを起動し、各手順を実行して結果を返します。Issue の受け入れ条件に照らして報告を確認し、問題があれば追加質問をするか、コードを修正させてから PR を作成します。

> [!NOTE]
> テスト時は `http://localhost:4321` でアプリが動作している必要があります。開発サーバーを停止した場合は、プロンプトを送る前に再起動します。初回の利用時にブラウザーのダウンロードが必要な場合があります。欠落を報告されたら、`npx playwright install chromium` を実行して再試行します。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## ブランチを公開してプルリクエストを作成する

1. Codespace の **Source Control** パネルを開き、Copilot が行った変更を確認します。
2. **+** アイコンを選んで変更をステージします。
3. **Sparkle** ボタンでコミット メッセージを生成します。

   ![Source Control パネルに表示された Copilot の変更。](../../../_images/ex3-source-control-changes.png)

4. **Publish** を選択し、ブランチをリポジトリにプッシュします。

## プルリクエストを作成する

Copilot に関連する Issue を見つけ、ブランチから PR を作成してもらいます。

1. Copilot Chat パネルで **New Chat** を選択します。
2. GitHub ツールを使えるように、エージェント選択メニューで **Agent** を選びます。
3. 次のプロンプトで PR の作成を依頼します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. GitHub ツールの実行に必要な場合は **Continue** を選択します。初回は GitHub への認証を求められることがあります。
5. Copilot が Issue を探し、PR を作成したことを確認します。
6. Copilot が表示したリンクを開いて PR をレビューします。まだマージしないでください。

## まとめと次のステップ

- MCP と MCP サーバーが Copilot にツールを追加する仕組みを確認しました。
- Playwright MCP サーバーをワークスペースに追加しました。
- ブラウザーでフィルタリング機能をテストしました。
- ブランチを公開し、フィルタリングの PR を作成しました。

MCP サーバーを使って機能をテストしました。次は、アクセシビリティのレビューなどに使える[カスタム エージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ注目されているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP Registry][mcp-registry]
- [VS Code の MCP サーバー][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
