---
title: "演習 2 - Copilot agent mode で機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

小さなアプリケーションの変更でも、複数のファイルを更新し、テストを実行する必要があります。必要なファイルを探し、変更し、テストし、見落としたファイルを見つけて再度変更する作業を、Copilot agent mode に任せてみましょう。

Copilot agent mode は統合開発環境 (IDE) でより自律的に動作します。プロジェクト構成を調べ、必要なファイルを変更し、テストなどのタスクを実行し、見つかった問題を修正します。

> [!NOTE]
> agent mode と cloud agent は異なる用途向けです。agent mode は IDE 内で動作し、すばやいフィードバックと対話を提供します。cloud agent は Issue とプルリクエストを通じてチームの一員のように非同期で作業します。

この演習では、次のことを確認します。

- Copilot agent mode がプロジェクトを調べ、関連ファイルを見つけ、複数ファイルを連携して変更する方法。
- UI とデータ層にまたがる機能の実装方法。
- Copilot が生成した変更とテストをレビューしてからマージする方法。

## シナリオ

ゲームの一覧が増えてきたため、カテゴリとパブリッシャーで絞り込みたいと考えています。前の演習で追加したパブリッシャー ヘルパーを使い、残りのデータ層、UI、テストを Copilot agent mode で実装します。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、サイトの現在の動作を確認します。Tailspin Toys はボードゲームのクラウドファンディング サイトです。単一の Astro アプリがビルド時に静的 HTML を生成し、Drizzle ORM でローカル SQLite データベースを参照します。別のバックエンド API やクライアント側ユーザー インターフェイス (UI) フレームワークはありません。データアクセス ヘルパーは `src/lib/` にあり、Astro の `<script>` で Document Object Model (DOM) API を使って操作を追加します。

### Web サイトを起動する

`npm run dev` タスクで単一の Astro 開発サーバーを起動します。

1. Codespace に戻り、前の演習後に `main` にいることを確認します。
2. Mac では <kbd>Control</kbd>+<kbd>\`</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>\`</kbd> を押してターミナルを開きます。
3. `main` を更新し、フィルタリング用ブランチを作成します。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. サイトを起動します。

   ```bash
   npm run dev
   ```

5. サーバーが起動したら、ターミナルに表示された `http://localhost:4321` を Mac では <kbd>Command</kbd>、Windows/Linux では <kbd>Ctrl</kbd> を押しながら選択します。Codespace では `https://<your-codespace-name>-4321.app.github.dev/` に転送されます。

> [!NOTE]
> Codespace のターミナルで `http://localhost:4321` を選ぶと、Codespace へのプライベート トンネルに自動的に転送されます。ローカル Web サーバーは Codespace 上で実行されています。

### Web サイトを確認する

Web サイトの主な機能は次のとおりです。

- **Home Page**: タイトル、画像、説明とともにボードゲームを一覧表示します。
- **Game Details Page**: ゲームを選択すると、タイトル、説明、パブリッシャー、カテゴリなどの詳細を表示します。

## Copilot でバックログを確認する

テンプレートから作成した GitHub Issue のバックログを Copilot に表示させ、ユーザーへの有用性に基づく優先順位を確認します。

1. Copilot Chat を開き **New Chat** を選択して、新しい会話を始めます。
2. Chat ビューのエージェント選択メニューで **Agent** を選びます。

   ![Chat ビューで Agent を選択する画面。](../../../_images/shared-chat-mode-selector.png)

3. 利用可能なモデルから **Claude Sonnet 4.5** を選びます。
4. 次のプロンプトを送ります。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

5. Issue の一覧を取得するため **Continue** を選択し、生成された一覧を確認します。

> [!CAUTION]
> このワークショップで特定のモデルを推奨するものではありません。大規模言語モデル (LLM) は確率的に動作するため、生成結果が例と異なる場合があります。

## 命令ファイルを確認する

機能を生成する前に、Copilot にコンテキストを与える UI 命令ファイルを確認します。

1. Codespace で `.github/instructions/ui.instructions.md` を開きます。
2. アーキテクチャ、コンポーネントの設計、テスト容易性、アクセシビリティに関するガイダンスを確認します。
3. Astro、Tailwind CSS、Drizzle 向けの命令ファイルへのリンクも確認します。

## フィルタリング機能を実装する

フィルタリングを完成させるには、データ層のロジック、テスト、ゲーム一覧の UI を更新し、テストを実行する必要があります。

1. 現在の会話を続けるか、**New Chat** で新しい会話を開始します。
2. **Add Context**、**Instructions**、**ui** の順に選び、UI 命令ファイルを追加します。

   ![UI 命令ファイルを選択する画面。](../../../_images/ex3-select-instructions-file.png)

3. エージェント選択メニューで **Agent** を選び、モデルが **Claude Sonnet 4.5** であることを確認します。

   ![Chat ビューで Agent を選択する画面。](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送ります。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

5. Copilot がデータ層、UI、テストを調べて変更する様子を確認します。

   ![Copilot agent mode がプロジェクト内のファイルを調べる画面。](../../../_images/ex3-agent-mode-explores.png)

6. テスト実行の許可を求められたら **Continue** を選択します。テストが途中で失敗する場合もあります。最終的なコードとチェック結果を確認してください。

   ![Copilot Chat がテスト実行の許可を求める画面。](../../../_images/ex3-agent-mode-run-tests.png)

   ![Copilot agent mode の提案と完了した会話。](../../../_images/ex3-agent-mode-proposed-changes.png)

7. 生成されたコードをレビューし、ブラウザーで機能を確認します。
8. 問題がなければ Copilot Chat で **Keep** を選択します。

## まとめと次のステップ

Copilot agent mode を使って Tailspin Toys に機能を追加しました。

- Copilot agent mode がプロジェクトを調べ、複数ファイルを連携して変更する方法を確認しました。
- UI とデータ層にまたがる機能を実装しました。
- Copilot が生成した変更とテストをレビューしました。

次は[Playwright の Model Context Protocol (MCP) サーバーで機能をテストし、プルリクエストを作成します][next-lesson]。

### 追加の演習 - ページネーションを実装する

ゲーム一覧が増えた場合に備えて、Copilot にページネーションの実装を依頼します。既存の命令ファイルを使い、ページ サイズをユーザーが選べるか固定するかを決め、必要な指示をプロンプトに含めます。意図した結果になるまで Copilot に追加の変更を依頼します。

## リソース

- [Copilot の ask、edit、agent mode の違いと使い分け][choose-mode]
- [VS Code の agent mode][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
