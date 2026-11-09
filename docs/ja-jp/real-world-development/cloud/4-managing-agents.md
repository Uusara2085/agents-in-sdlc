---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の演習では、Copilot cloud agent にユーザー体験の改善と機能追加を依頼しました。cloud agent は非同期かつ自律的に動作しますが、作業を監視することも重要です。GitHub.com の[エージェント ページ][agents-page]では、オープンなプルリクエスト (PR) があるタスクを確認し、実行中のセッションに追加の指示を送れます。

この演習では、次のことを行います。

- エージェント ページで cloud agent のタスクを監視します。
- 実行中のセッションに追加機能を依頼します。

## シナリオ

高コントラスト モードを依頼した後、チームはライトモードも追加したいと考えました。同じスタイル変更の作業中にモード切り替え機能を追加できるよう、エージェントにライトモードも実装するよう依頼します。

## Copilot cloud agent のタスクを確認する

cloud agent に割り当てたタスクの状態を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)を開きます。
2. メイン ペインと左ペインのタスクリストを確認します。コードのドキュメント追加、ゲームを変更する API の生成、Web サイトへの高コントラスト モード追加などのタスクが表示されます。
3. 実行中のタスクを選択し、Copilot が行った操作を確認します。リポジトリのチェックアウト、環境の作成、Model Context Protocol (MCP) サーバーの設定、タスクを完了するための作業などが表示されます。

> [!NOTE]
> 表示される手順は、作業の状態や Copilot が選んだ方法によって異なります。

4. 右側に表示される PR ペインで、PR と変更ファイルを確認します。

## cloud agent の作業に追加指示を送る

高コントラスト モードの作業を続けながら、ライトモードの切り替えも追加するよう依頼します。

1. 高コントラスト モードに関するセッションを選択します。タイトルは Copilot が付けた名前や作業状態によって異なります。

   ![エージェントの管理画面に表示されたアクセシビリティ セッション。](../../../_images/ex6-accessibility-session.png)

2. セッションがセットアップを完了し、作業を開始するまで数分待ちます。開始すると、セッションに進捗メッセージが表示されます。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Copilot agents ページで、作業中のセッションに追加指示を送るダイアログを示す画面。](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot が指示を受け取り、作業に追加したことを確認します。

## Copilot の作業を続ける

Copilot は、メッセージを送信した時点で進めていた処理を終えてから、更新されたタスクに取り組みます。作業には数分かかることがあります。その間に、これまでに学んだ内容を振り返ってください。

## まとめと次のステップ

Copilot agents ページを使って、cloud agent の作業を監視し、進行中のセッションに追加の依頼を送りました。

次のことを行いました。

- エージェントの管理画面で cloud agent のタスクを監視しました。
- 実行中のセッションに追加機能を依頼しました。

次は、Copilot が作成したプルリクエストを[反復して改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復して改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
