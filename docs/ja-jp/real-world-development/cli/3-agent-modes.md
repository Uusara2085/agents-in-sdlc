---
title: "レッスン 3 - エージェント モード: Plan と Autopilot"
description: "Plan で方針を決め、Autopilot で Issue に基づくフィルタリングを実装し、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

小さな機能を追加したので、次はより大きな変更に取り組みます。Issue を起点に機能を実装し、コードの妥当性と動作を確認してから、プロジェクトにマージする一連の開発プロセスを進めます。

この機能の作業では、同じ会話とブランチを使います。通常はファイルの種類ごとにブランチや PR を分けますが、ここでは主な概念に集中するため、作業を一つにまとめます。

このレッスンでは、次のことを行います。

- GitHub Issue から Copilot の会話を始めます。
- Plan モードで要件を決めます。
- Autopilot モードで機能を実装します。
- コードをレビューします。
- 転送されたブラウザーで機能を手動で検証します。

以降の作業では、リポジトリの命令を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP による検証を追加して QA エージェントを作成し、機能の PR を開きます。

## シナリオ

Tailspin Toys のカタログが増え、ユーザーがカテゴリやパブリッシャーでゲームを絞り込めるようにしたいと考えています。バックログの Issue には機能が記載されていますが、カテゴリを組み合わせる方法など、実装前に決めるべき点があります。Plan モードで方針を決め、範囲を定めた実装を Autopilot に任せます。

## 背景

AI エージェントを使っても、開発プロセスの基本は変わりません。

1. 必要な作業を説明する Issue から始めます。
2. 実装計画を立てます。
3. コードを作成してレビューします。
4. テストを実行します。
5. 新しい機能を手動で検証します。
6. プルリクエスト (PR) を作成します。
7. レビューと継続的インテグレーションが成功したら、コードをマージします。

チームや組織によって詳細は異なりますが、AI が生成したコードも、通常のコードと同じレビューと検証を行います。

## 会話モード

**会話モード**は、エージェントに与える自律性の程度を制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> でモードを切り替えます。

- **Interactive**: エージェントと共同で作業します。エージェントは変更を提案し、次に進む前に入力を待ちます。
- **Plan**: エージェントは計画を作成します。計画中にプロジェクト ファイルを編集することはできません。
- **Autopilot**: エージェントが自律的にコードを書き、テストを実行し、完了するまで反復します。

まず Plan モードで計画を確認し、その後 Autopilot で実装します。

## Issue から作業を開始する

フィルタリングの実装に使う Codespace、リポジトリ、ターミナルを準備します。

1. Codespace に戻ります。停止している場合は再起動します。
2. 星評価の PR がマージ済みであることを確認します。
3. ターミナルが開いていない場合は、Mac では <kbd>Control</kbd>+<kbd>\`</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>\`</kbd> を押します。
4. `main` を更新し、フィルタリング用ブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を2回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての Issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** を選びます。
9. <kbd>C</kbd> を押して Issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトに `#7` などの Issue 番号が表示されます。`#` を使って GitHub の Issue や PR をコンテキストに追加できます。

## フィルタリング機能を計画する

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替え、プロンプトの下に **Plan** と表示されていることを確認します。
2. 追加された Issue の後に次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

3. フィルタリングの仕様について Copilot から質問されたら、希望する動作を回答します。
4. 計画が完成したら、Mac では <kbd>Control</kbd>+<kbd>E</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>E</kbd> を押して展開します。
5. 計画を読み、内容を確認します。
6. 決定した内容と異なる部分があれば、Copilot に修正を依頼します。

## Autopilot を承認する

計画を確認したら、実装を依頼します。

1. **Accept plan and build on autopilot (recommended)** または、インストール済みのバージョンに表示される同様の選択肢を選びます。
2. プロンプトの下に **Autopilot** と表示されていることを確認します。
3. Copilot が計画に沿ってコードを生成し、テストを実行する様子を確認します。

> [!NOTE]
> 承認すると実装がすぐに始まることがあります。必ず先に計画をレビューしてください。依存関係が不足している、またはポートが競合していると報告された場合は、チェック完了と見なす前に問題を解決します。

## 実装をレビューして検証する

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードにし、モード表示が **Plan** または **Autopilot** ではないことを確認します。
2. `/diff` を入力して、フィルタリングの実装とテストを確認します。
3. Issue と計画で決めた内容に照らして変更を確認します。
4. レビューが終わったら <kbd>Esc</kbd> を押して差分表示を閉じます。
5. プロジェクトのチェック結果を確認し、失敗があれば Copilot に解決を依頼します。

## 新機能を試す

1. Copilot に次のプロンプトを送り、アプリを起動します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら、**Open in Browser** を選択します。
3. Plan で決めたカテゴリとパブリッシャーのフィルター、および組み合わせを試します。
4. リセットと結果が空の場合の動作が、Issue と決定内容に合っていることを確認します。
5. Codespace に戻り、Copilot に起動した開発サーバーの停止を依頼します。

## まとめと次のステップ

会話モードを使って機能を構築し、レビューしました。

- GitHub Issue から Copilot の会話を始めました。
- Plan モードで要件を決めました。
- Autopilot モードで機能を実装しました。
- コードをレビューしました。
- 転送されたブラウザーで機能を手動で検証しました。

次は、[カスタム命令を使ってコード生成の規約を確認します][next-lesson]。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
