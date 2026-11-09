---
title: "演習 4 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフローの特定のタスクや分野に特化した AI アシスタントを作成できます。リポジトリの `.github/agents` にある Markdown ファイルでエージェントを定義し、指示、ベスト プラクティス、コーディング パターン、専門知識を指定します。たとえば、[Web Content Accessibility Guidelines (WCAG)][wcag] に沿ったアクセシビリティ エージェント、セキュリティ エージェント、テスト エージェントを作成できます。

各エージェント ファイルには `name` と `description` を含む YAML frontmatter と、エージェントの動作を定義する Markdown プロンプトがあります。エージェントはプロジェクト内の `.github/agents` またはグローバルな `~/.copilot/agents` に配置できます。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントは作業者、[エージェント スキル][agent-skills-concept]は道具と考えると分かりやすいでしょう。カスタム エージェントには独自のコンテキスト ウィンドウがあり、スキルやほかのエージェントを使って作業できます。

> [!NOTE]
> カスタム エージェントの作成方法は一つではありません。さまざまな環境やシナリオで試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず誰もが使えるサイトを目指しています。現在のダークテーマは、テキストと背景色のコントラストが不十分で読みにくいというフィードバックがありました。アクセシビリティ用カスタム エージェントを使い、ユーザーが切り替えられる高コントラスト モードを追加します。

この演習では、次のことを行います。

- 既存のアクセシビリティ用カスタム エージェントを確認します。
- Copilot Chat の agent mode でエージェントを使い、高コントラスト モードを実装します。

## アクセシビリティ カスタム エージェントを確認する

1. Codespace に戻り、ターミナルを開いて、`main` からアクセシビリティ作業用のブランチを作成します。フィルタリング PR とは分けて作業します。

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. `.github/agents/accessibility.md` を開きます。
3. `name` と `description` を含む YAML frontmatter を確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` を含む frontmatter が必要です。

4. アクセシブルなサイト向けの責任、ベスト プラクティス、HTML・CSS・JavaScript のコード例、よくある問題を確認します。

## Copilot Chat でカスタム エージェントを使う

VS Code の Copilot Chat ビューでは、`.github/agents` にあるカスタム エージェントを選択し、その指示とツールに沿って会話できます。

1. Copilot Chat パネルを開き、**New Chat** を選択します。
2. Chat ビューのエージェント選択メニューで **Agent** を選びます。

   ![Chat ビューで Agent を選択する画面。](../../../_images/shared-chat-mode-selector.png)

3. エージェント選択メニューを開き、**Accessibility agent** を選びます。

   ![Copilot の Issue 割り当てでカスタム エージェントを選択する画面。](../../../_images/ex5-select-custom-agent.png)

4. 次のプロンプトを送ります。

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot がコードベースを調べ、変更を提案して適用する様子を確認します。
6. **Files changed** の表示で、エージェントが変更したファイルを確認します。

Copilot は Astro コンポーネント、CSS、関連テストなどを変更します。作業中はレビューと追加指示を続けます。

## まとめと次のステップ

このレッスンでは、特定のタスクや分野に特化した GitHub Copilot の[カスタム エージェント][custom-agents]を確認しました。

- カスタム エージェントの定義方法を確認しました。
- Copilot Chat の agent mode でカスタム エージェントを使いました。

次は[エージェントの作業を監視して方向を調整し][next-lesson]、同じセッションでライトモードを追加します。

## リソース

- [カスタム エージェントについて][custom-agents]
- [IDE でカスタム エージェントを作成する][creating-custom-agents-ide]
- [VS Code のカスタム エージェント][custom-agents-vscode]
- [カスタム エージェントの構成][custom-agents-config]
- [awesome-copilot のカスタム エージェント][awesome-copilot-agents]

---

| [← 前のレッスン: Playwright MCP サーバーで機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
