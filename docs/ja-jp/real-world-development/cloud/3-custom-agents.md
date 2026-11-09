---
title: "演習 3 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフローの特定のタスクや分野に特化した人工知能 (AI) アシスタントを作成できます。リポジトリの `.github/agents` にある Markdown ファイルでエージェントを定義し、役割に応じた指示、ベスト プラクティス、コーディング パターン、専門知識を指定します。チームの知見を再利用できるようにし、たとえば [Web Content Accessibility Guidelines (WCAG)][wcag] に沿ったアクセシビリティ エージェント、セキュリティ エージェント、テスト エージェントを作成できます。

カスタム エージェントはプロジェクト内の `.github/agents` またはグローバルな `~/.copilot/agents` に配置した Markdown ファイルで定義します。各ファイルには少なくとも `name` と `description` を含む YAML frontmatter と、エージェントの動作、専門性、指示を記載する Markdown プロンプトが必要です。

### カスタム エージェントとエージェント スキルの違い

カスタム エージェントと[エージェント スキル][agent-skills-concept]は、どちらも主に Markdown ファイルで定義し、AI に作業方法を伝えます。大まかに言うと、**カスタム エージェントは作業者、スキルは道具**です。

カスタム エージェントは独自のコンテキスト ウィンドウを持ち、スキルやほかのエージェントを使って作業を進めます。この演習のアクセシビリティ エージェントは、サイトをアクセシビリティ ガイドラインに沿ってレビューし、更新します。その過程で、PR ワークフローやテスト実行用のスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成方法は一つではありません。ほかの AI 機能と同様に、環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

この演習では、次のことを行います。

- カスタム エージェントの定義方法を確認します。
- タスクをカスタム エージェントに割り当てます。

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、すべての人がクラウドファンディング プラットフォームを使えるようにしたいと考えています。現在のダークテーマは、テキストと背景色のコントラストが不十分で、読みにくいというユーザーの声が寄せられています。このアクセシビリティ上の課題に対応するため、デザイン チームはユーザーが切り替えられる高コントラスト モードを求めています。アクセシビリティが重要なため、カスタム エージェントを使って機能をできるだけ早く生成します。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントはすでに用意されています。内容を確認して、Copilot の作業にどのような指針を与えるかを把握します。

1. Codespace に戻り、`.github/agents/accessibility.md` を開きます。
2. `name` と `description` を含む YAML frontmatter を確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` を含む frontmatter が必要です。

3. 続くセクションを確認します。アクセシブルな Web サイトのコード生成に関する役割、アクセシビリティのベスト プラクティス、HTML・CSS・JavaScript のコード例、よくある問題が記載されています。

## Issue を作成して割り当てる

このエージェントに高コントラスト モードの実装を依頼します。

1. リポジトリの **Issues** タブを開き、**New issue**、**Blank issue** の順に選択します。
2. **Title** に `Add high contrast mode to website` と入力します。
3. **Description** に次の内容を入力します。

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

4. **Create** を選択して Issue を作成します。
5. 右側の **Assign to Copilot** を選択します。
6. エージェントの一覧から **Accessibility agent** を選択し、**Assign** を選択します。

   ![カスタム エージェントとして Accessibility agent を選択した Copilot の Issue 割り当て画面。](../../../_images/ex5-select-custom-agent.png)

Copilot はバックグラウンドで作業を開始します。

## まとめと次のステップ

この演習では、特定のタスクや分野に特化した GitHub Copilot の[カスタム エージェント][custom-agents]を確認しました。カスタム エージェントを使うと、チームの知見や標準を再利用可能な形で定義できます。

次のことを行いました。

- カスタム エージェントの定義方法を確認しました。
- タスクをカスタム エージェントに割り当てました。

Copilot が高コントラスト モードを実装している間に、[エージェントのセッションを監視して方向を調整します][next-lesson]。

## リソース

- [カスタム エージェントについて][custom-agents]
- [組織でカスタム エージェントを使うための準備][org-custom-agents]
- [Enterprise でカスタム エージェントを使うための準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
