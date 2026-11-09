---
title: "演習 5: GitHub Copilot の作業を反復して改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このワークショップでは、コードへのドキュメント追加、関連ゲーム機能、高コントラストとライトモードを Copilot に依頼しました。変更を確認し、必要に応じて Copilot に修正を依頼します。

### シナリオ

生成 AI を使っても、ソフトウェア設計や開発・運用 (DevOps) の基本は変わりません。生成されたコードをレビューし、通常の開発プロセスを進めます。チーム全体に Copilot のコードレビューを有効にする前に、ドキュメント、関連ゲーム、アクセシビリティの各変更を確認します。

## セキュリティと GitHub Copilot cloud agent

cloud agent は非同期に作業するため、安全性を保つための制約があります。

- Copilot はリポジトリを読み取れますが、書き込みは作業ブランチに限られます。
- cloud agent は GitHub Actions 内に一時的な環境を作成して実行されます。
- GitHub Actions ワークフローの実行には、人による承認が必要です。
- [外部リソースへのアクセス][agent-firewall]は、MCP サーバーを含め、既定で制限されています。

## 生成されたドキュメントをレビューする

最初に、コードへのドキュメント追加を依頼した Copilot のプルリクエスト (PR) を確認します。

> [!NOTE]
> PR に Copilot がファイアウォールでブロックされたという警告が表示される場合があります。外部リソースや Model Context Protocol (MCP) サーバーへのアクセスは既定で制限されているため、これは想定された動作です。必要であれば、[cloud agent のファイアウォールを設定または無効化][agent-firewall]できます。

1. github.com のリポジトリを開きます。
2. **Pull Requests** を選択し、**Add missing documentation** などのタイトルの PR を開きます。
3. Copilot が作業中で `[WIP]` が付いている場合は、完了するまで待ちます。
4. **Files changed** タブを選び、変更をレビューします。

   ![プルリクエストで Files changed タブを開いた画面。](../../../_images/shared-pr-files-changed.png)
5. 追加された TSDoc コメントやその他のドキュメントを確認します。Exercise 2 で確認した命令ファイルに基づく TSDoc コメント、TypeScript の規約、ファイル ヘッダーを確認してください。
6. **Conversation** タブに戻り、ワークフローの承認待ちを確認します。
7. 承認待ちのワークフローがある場合は、**Approve and run workflows** を選択します。

   ![承認待ちのワークフローを承認して実行するボタン。](../../../_images/shared-approve-workflows.png)
8. PR の checks セクションでワークフローの結果を確認します。Astro アプリのプロジェクト チェックが成功するまで待ちます。

## GitHub Copilot に変更を依頼する

PR のコメントで **@copilot** をタグ付けすると、Copilot に更新を依頼できます。たとえば、次のような変更を頼めます。

- 各コード ファイルの先頭に役割を説明するコメントを追加する。
- TypeScript と Astro ファイルに TSDoc コメントを追加する。
- Astro アプリの構成を説明する README を作成する。

1. PR のコメントに **@copilot** を付け、変更を依頼します。
2. **View Session** を選び、Copilot が作業する様子を確認します。
3. **Back to pull request** を選んで PR に戻ります。

   ![プルリクエストに戻る操作。](../../../_images/ex7-back-to-pr.png)
4. Copilot の作業が完了したら、新しいコミットが追加されたことを確認します。
5. **Files changed** タブで変更をレビューします。

満足するまで改善を繰り返せます。問題がなければ、ドラフト PR をレビュー可能な状態にして `main` にマージします。

![ドラフト PR をレビュー可能な状態に変更する操作。](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する PR をレビューします。

1. GitHub のリポジトリで **Pull Requests** タブを開きます。
2. **Show related games on the game details page** などのタイトルの PR を選択します。
3. **Files changed** タブで生成された変更をレビューします。
4. **Conversation** タブでワークフローの承認待ちを確認し、必要なら **Approve and run workflows** を選択します。

   ![承認待ちのワークフローを承認して実行するボタン。](../../../_images/shared-approve-workflows.png)
5. PR の checks セクションで Astro アプリのチェックが成功したことを確認します。
6. **省略可能:** Codespace のターミナルで Copilot が作成したブランチに切り替えて、機能を手動でテストします。`<branch-name>` は実際のブランチ名に置き換えます。

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

必要であれば、PR の **Conversation** タブにコメントを追加し、関連ゲームの表示件数やコメント ヘッダー、TSDoc コメントについて修正を依頼できます。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティ用カスタム エージェントに依頼した高コントラスト モードとライトモードをレビューします。

1. リポジトリの **Pull Requests** タブを開きます。
2. **Add high contrast mode to website** などのタイトルの PR を選択します。
3. Copilot がまだ作業中で `[WIP]` が付いている場合は、完了まで待ちます。
4. **Files changed** タブで変更をレビューします。特に次の点を確認します。
   - モードを切り替える UI コンポーネント
   - ユーザー設定を保持する local storage の使用
   - 高コントラスト モードとライトモードの CSS やスタイル
   - ARIA ラベルやキーボード操作などのアクセシビリティ属性
   - モード切り替えを管理する JavaScript/TypeScript
5. **Conversation** タブに戻り、ワークフローの承認待ちがあれば **Approve and run workflows** を選択します。

   ![承認待ちのワークフローを承認して実行するボタン。](../../../_images/shared-approve-workflows.png)
6. PR の checks セクションでワークフローが成功したことを確認します。
7. **省略可能:** Codespace でブランチをチェックアウトし、ブラウザーで高コントラストとライトモードの切り替えをテストします。ページを再読み込みしても設定が保持されることを確認します。

アクセシビリティ エージェントが、アクセシビリティのベスト プラクティスに沿って実装を導いたことを確認してください。改善点があれば、PR のコメントで **@copilot** に更新を依頼できます。

## 省略可能な演習 - さらに作業を委任する

実際のバックログから作業を選び、cloud agent に Issue を割り当ててみます。たとえば、次のような Issue を作成できます。

- ゲーム詳細ページに支援希望者向けフォームを追加する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセス ヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent の各演習を完了しました。

- リポジトリに含まれるカスタム命令を確認し、cloud agent の出力への影響を確認しました。
- Issue を Copilot cloud agent に割り当て、環境準備、計画、非同期の実行を確認しました。
- アクセシビリティ用カスタム エージェントを作成して使い、高コントラストとライトモードを追加しました。
- Copilot agents ページからセッションを監視し、作業中に方向を調整しました。
- PR をレビューし、**@copilot** で変更を依頼し、ワークフローを承認しました。

## 振り返りと次のステップ

Cloud agent の演習を完了しました。別の環境も試す場合は、次のワークショップに進みます。

- **[VS Code ワークショップ](../../vscode/)** — IDE で Copilot Chat の agent mode と MCP 統合を試します。
- **[CLI ワークショップ](../../cli/)** — Plan、Autopilot、エージェント スキル、QA カスタム エージェント、Playwright MCP、Agent Merge、cloud agent への `/delegate` を使い、ターミナルから変更を完了します。

自身のリポジトリでは、リファクタリングやテスト範囲の拡大を Issue として登録して cloud agent に割り当てたり、別分野のカスタム エージェントを作成したり、別の技術スタック向けに `copilot-setup-steps.yml` を設定したりできます。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot agents について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]
- [Copilot cloud agent のファイアウォールを設定する][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[previous-lesson]: ../4-managing-agents/
[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
