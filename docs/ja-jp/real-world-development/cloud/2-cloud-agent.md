---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: カスタム命令][previous-lesson]

多くの組織では、未解決のセキュリティ問題、更新が必要なレガシー コード、バックログに残った機能要望など、技術的負債に取り組む時間が不足しています。GitHub Copilot cloud agent は、コードの更新や機能追加などを非同期に行い、作業が終わると人がレビューできるドラフトのプルリクエスト (PR) を作成します。開発者は定型作業を任せ、その間に全体像を考える必要のある仕事を進められます。

この演習では、次のことを行います。

- コード生成環境を確認します。
- 安全な操作が行われる仕組みを確認します。
- Issue の範囲を明確にする重要性を確認します。
- Issue を Copilot に割り当てます。

## シナリオ

Tailspin Toys には、アプリケーションの公開関数に TSDoc コメントを追加する技術的負債があります。また、デザイン チームはゲーム詳細ページに同じカテゴリのゲームを表示し、ユーザーがゲームを見つけやすくしたいと考えています。まず受け入れテストで UX を試せる実装が必要ですが、ほかに優先度の高い Issue もあります。これらの作業を cloud agent に非同期で任せ、後から結果をレビューします。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者のようにバックグラウンドで作業できます。たとえば、[GitHub Issue を Copilot に割り当て][assign-issue]ると、エージェントはドラフト PR を作成して進捗を記録し、環境を準備して作業を開始します。作業中または完了後にセッションを確認でき、レビューの準備ができると PR で通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法はありません。タスクの複雑さを理解し、[cloud agent に依頼する作業の範囲][cloud-agent-best-practices]を明確にしてください。AI ペア プログラマーとして扱い、段階的に学び、試し、調整します。生成 AI を使ってもソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム命令

前の演習では、カスタム命令が Copilot の作業を導く方法を確認しました。cloud agent に作業を割り当てる前に、リポジトリに含まれる命令ファイルを読み取り専用で確認します。

- `.github/copilot-instructions.md` の **Code standards** を開き、TypeScript の規約と TSDoc コメントに関する指示を確認します。
- `.github/instructions/unit-tests.instructions.md` を開き、`applyTo` frontmatter が `**/*.test.ts` に命令を適用することを確認します。

次の手順で `Code lacks documentation` Issue を割り当てたら、命令ファイルによって TSDoc コメント、TypeScript の規約、ファイル ヘッダーが反映されるか確認します。

## Copilot cloud agent の開発環境を準備する

cloud agent は GitHub Actions を使って作業環境を用意します。`.github/workflows/copilot-setup-steps.yml` のセットアップ ワークフローでは、必要な開発ツールや依存関係を設定できます。このテンプレートでは、Node.js、プロジェクトの依存関係、エンドツーエンド テスト用のブラウザー、マイグレーションとシードを適用した SQLite データベースを準備済みです。

```yaml
name: "Copilot Setup Steps"

# リポジトリの Actions タブからセットアップ手順をテストできます。
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 手順に必要な最小限の権限を設定します。Copilot の操作には独自のトークンが使われます。
    permissions:
      # セットアップ手順でリポジトリをチェックアウトする場合は contents: read が必要です。チェックアウトしない場合は、手順の完了後に Copilot が自動で行います。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Node.js を使う Astro アプリのセットアップ
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub Actions ワークフローと同様の形式ですが、次の点を確認してください。

- `copilot-setup-steps` という単一のジョブが、Copilot の PR 作業開始前に GitHub Actions で実行されます。
- `workflow_dispatch` を使うと、リポジトリの **Actions** タブから手動でワークフローを実行し、Copilot に割り当てる前にセットアップをテストできます。

## ドキュメントを追加する Issue を割り当てる

公開関数のドキュメントを追加する作業を cloud agent に依頼し、作業の進み方を確認します。

1. 新しいブラウザー タブで github.com のリポジトリを開きます。
2. **Issues** タブを選び、**New issue**、**Blank issue** の順に選択します。
3. **Title** に `Code lacks documentation` と入力します。
4. **Description** に次の内容を入力します。

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

5. **Create** を選択して Issue を作成します。
6. 右側の **Assign to Copilot** を選び、割り当てダイアログで **Assign** を選択します。

   ![Copilot を Issue に割り当てる画面。](../../../_images/shared-assign-copilot.png)

   ![Copilot の割り当て内容を確認する画面。](../../../_images/ex4-assign-copilot-details.png)

7. **Pull Requests** タブを開き、新しく作成された PR を選択します。タイトルは `[WIP]: Code lacks documentation` のような形式です。表示されない場合は少し待ってからページを更新します。
8. Copilot のタスクリストが表示されたら、実行予定の作業を確認します。環境の準備やプロジェクトの分析に数分かかることがあります。
9. PR のタイムラインで Copilot が作業を開始したことを確認し、**View session** を選択します。表示が更新されない場合はページを更新します。

   ![Copilot のセッションを表示するボタン。](../../../_images/ex4-view-session.png)

10. セッションで、Copilot がコードを調べ、計画を立て、変更を作成する様子を確認します。

処理中は別の作業を進められます。続いて、関連ゲームの表示も cloud agent に依頼します。

## ゲーム詳細ページに関連ゲームを追加する

別のタスクをエージェントに任せ、開発者はほかの作業を進められます。関連ゲームを表示する Issue を作成して割り当てます。

1. リポジトリの **Issues** タブで **New issue**、**Blank issue** の順に選びます。
2. **Title** に `Show related games on the game details page` と入力します。
3. **Description** に次の要件を入力します。

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

4. **Create** を選んで Issue を作成し、右側の **Assign to Copilot** から **Assign** を選択します。

   ![Copilot を Issue に割り当てる画面。](../../../_images/shared-assign-copilot.png)

5. Issue の最初のコメントに 👀 が表示され、Copilot が作業を開始したことを確認します。

   ![Copilot が Issue の作業中であることを示す目の絵文字。](../../../_images/ex4-issue-eyes-emoji.png)

cloud agent はバックグラウンドで作業します。完了後に結果をレビューしてください。次はカスタム エージェントを作成して使います。

## まとめと次のステップ

この演習では、[GitHub Copilot cloud agent][copilot-agents]に Issue を割り当て、非同期に作業を進める方法を確認しました。技術的負債への対応、新機能の作成、コードの移行などを依頼できます。

次のことを行いました。

- コード生成環境を確認しました。
- 安全な操作が行われる仕組みを確認しました。
- Issue の範囲を明確にする重要性を確認しました。
- Issue を Copilot に割り当てました。

次は[カスタム エージェントを作成して使います][next-lesson]。Copilot cloud agent は [MCP サーバー][cloud-agent-mcp]とカスタム命令にも対応しています。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローに関するベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
