---
title: "演習 5 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム エージェント][previous-lesson] |
|:--|

agent mode の Copilot は、コードベースを調べ、変更を提案し、ファイルを編集してコマンドを実行します。VS Code の Copilot Chat では、ツールの呼び出しや編集をリアルタイムで確認し、差分ごとに変更を採用または取り消し、追加プロンプトで方向を調整できます。

この演習では、次のことを行います。

- アクセシビリティ エージェントの作業をリアルタイムで監視します。
- 提案されたファイル編集を確認して採用します。
- セッション中にライトモードの切り替えを追加するよう依頼します。

## シナリオ

[前の演習][previous-lesson]で使ったアクセシビリティ用カスタム エージェントは、高コントラスト モードを実装しています。作業中に、デザイン チームからライトモードも必要だという依頼がありました。新しい会話を始めず、既存のセッションに追加の作業を依頼します。

## Copilot の進捗を監視する

エージェントが調べたファイル、実行したコマンド、提案した変更は Copilot Chat ビューに表示されます。編集は差分と **Keep** / **Undo** の操作とともに表示されます。

1. 前の演習から Copilot Chat ビューに戻ります。
2. 会話をスクロールし、ツールの呼び出しやファイル編集を確認します。
3. 編集を採用するには **Keep**、取り消すには **Undo** を選びます。
4. Chat 上部の **Files changed** を開き、このセッションで変更されたファイルを確認します。
5. 高コントラスト モードの実装が終わるまで待ち、Copilot の最終報告を確認します。

> [!NOTE]
> ターミナル コマンドなどのツール実行で許可を求められた場合、エージェントは **Allow** を表示して一時停止します。実行してよいコマンドだけを許可してください。

## ライトモードを追加するようエージェントに依頼する

同じ会話でライトモードを依頼すると、エージェントは先ほどの変更や保存方法のコンテキストを引き継ぎます。

1. Copilot Chat の入力欄に次のプロンプトを送ります。

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. エージェントが既存の変更を確認し、ライトモードを追加する様子を見ます。
3. 新しい編集を確認し、**Keep** または **Undo** で各変更を判断します。
4. 望まない方向に進んだ場合は、入力欄の横にある **Stop** を選んで停止し、追加プロンプトで意図を伝えます。

> [!TIP]
> 作業中のセッションに追加指示を送ると、最初からやり直すより速く調整できます。たとえば、CSS の整理、既存設定パネルへの統合、キーボード ショートカットの追加を依頼できます。

## 作業内容をレビューする

コミットする前に、エージェントが変更した内容を確認します。

1. VS Code の **Source Control** ビューを開きます。
2. 変更されたファイルの一覧を確認します。Astro コンポーネント、スタイル、関連テストなどが含まれます。
3. 変更ファイルをいくつか開き、差分を確認します。Accessible Rich Internet Applications (ARIA) 属性、キーボード操作、セマンティック HTML、local storage による設定の保持を確認します。
4. 問題がなければ **Source Control** パネルでステージしてコミットします。次のレッスンで公開します。

## まとめと次のステップ

Copilot Chat の agent mode を使い、ファイル編集を確認して採用または取り消し、追加プロンプトで作業中のセッションを拡張しました。

- エージェントの作業をリアルタイムで監視しました。
- 個々のファイル編集を採用または取り消しました。
- 追加プロンプトでセッションの方向を調整しました。

次は[アクセシビリティの変更をプルリクエストとして公開し][next-lesson]、このワークショップで作成したカスタム エージェントの変更をレビューします。

## リソース

- [VS Code の Copilot Chat][copilot-chat-vscode]
- [agent mode の使用][agent-mode]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復して改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
