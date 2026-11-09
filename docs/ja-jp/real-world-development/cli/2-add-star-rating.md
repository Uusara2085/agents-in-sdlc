---
title: "レッスン 2 - 星評価を追加する: 小さな改善"
description: "Copilot CLI でゲーム カードを変更し、差分とブラウザー表示を確認して、最初のプルリクエストをマージします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI をインストールし、会話を試しました。次は、ゲーム カードに星評価を表示する小さな変更を行います。評価データはすでにありますが、ホームページのカードには表示されていません。エージェントに変更を依頼し、レビューして、最初のプルリクエストとしてマージします。

このレッスンでは、次のことを行います。

- 機能ブランチで Copilot の会話を開始します。
- 小さな変更をエージェントに依頼します。
- `/diff` で変更をレビューします。
- アプリを起動し、転送されたブラウザーで確認します。
- 最初のプルリクエスト (PR) を作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価があり、ゲーム詳細ページにはすでに表示されています。ホームページのゲーム カードにはタイトル、カテゴリ、パブリッシャー、説明しか表示されません。既存の評価を各カードに表示する変更を加えます。

## 会話の構成

**会話**は、Copilot CLI でタスクに取り組む場所です。Copilot app と異なり、通常の CLI 会話では、専用の worktree ではなく、ターミナルで現在チェックアウトしているリポジトリと Git ブランチを使用します。保存した会話は後で再開できます。ファイルとブランチは通常の Git 状態としてディスク上にあります。

会話では、プロンプトとエージェントの応答、ファイルの調査や編集などのツール操作、`/diff` で確認できる変更を見られます。

## 会話を開始して変更を依頼する

新しい会話を開始し、機能を実装します。

1. Codespace に戻ります。
2. ターミナルが開いていない場合は、Mac では <kbd>Control</kbd>+<kbd>\`</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>\`</kbd> を押します。
3. Copilot CLI が起動していない場合は、次のコマンドを実行します。

   ```bash
   copilot --yolo
   ```

4. `/new` を入力して <kbd>Enter</kbd> を押し、新しいセッションを開始します。
5. 次のプロンプトで変更を依頼します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot はプロジェクトを調査し、ゲーム詳細の表示に使われているファイルを特定して、必要なコードを作成します。

## 差分をレビューする

マージする前に、AI が生成した変更をレビューします。

1. `/diff` を入力し、変更されたすべてのファイルを確認します。
2. `starRating` に値がある場合は数値が、`null` の場合は `No rating yet` がゲーム カードに表示されることを確認します。
3. 両方の状態がテストされていることを確認します。
4. Copilot が実行したチェックの結果を確認し、失敗があれば修正を依頼します。
5. レビューが終わったら <kbd>Esc</kbd> を押して差分画面を閉じます。

> [!NOTE]
> 生成 AI は確率的に動作するため、コードの詳細は異なる場合があります。特定の実装と一致するかではなく、動作を確認してください。

## 変更を確認する

Codespaces で転送されたブラウザーから更新後のユーザーインターフェイス (UI) を確認します。

1. Copilot に次のプロンプトを送ってアプリを起動します。

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら、**Open in Browser** を選択します。
3. ゲーム カードに5段階の評価が表示されることを確認します。
4. Copilot に次のプロンプトを送ってサーバーを停止します。

   ```plaintext
   Stop the development server you started.
   ```

## 最初のプルリクエストを作成してマージする

1. 既定のエージェントに次のプロンプトを送り、変更をコミットします。

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. `/pr create` を入力します。Copilot CLI が既存のコミットをプッシュして PR を作成し、URL を表示します。
3. Copilot CLI が表示した URL を、Mac では <kbd>Command</kbd>、Windows/Linux では <kbd>Ctrl</kbd> を押しながら選択します。
4. 変更ファイルとチェックをレビューします。
5. 問題がなければ **Merge pull request** を選択し、マージを確認します。
6. Codespace に戻り、`/exit` で Copilot CLI を終了します。
7. ローカルの `main` を更新します。

   ```bash
   git checkout main
   git pull
   ```

## まとめと次のステップ

GitHub Copilot CLI を使って最初の変更をリリースしました。

- 機能ブランチで Copilot の会話を開始しました。
- エージェントにゲーム カードの小さな変更を依頼しました。
- `/diff` で変更をレビューしました。
- アプリを実行し、転送されたブラウザーで星評価を確認しました。
- 最初の PR を作成してマージしました。

次は、[フィルタリングの Issue から作業を始め、Plan と Autopilot モードを使って機能を構築します][next-lesson]。

## リソース

- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
