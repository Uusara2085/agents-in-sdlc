---
title: "レッスン 8 - 機能の PR を作成してマージする"
description: "フィルタリング、命令、スキル、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルタリングの実装、命令の更新、スキルの更新、品質保証 (QA) プロファイル、テストは同じブランチにあります。まとめてレビューし、プルリクエスト (PR) を作成します。星評価の PR は手動でマージしました。今回は **Agent Merge** に PR の処理を任せます。

> [!NOTE]
> 通常は機能、命令、スキル、QA エージェントを複数の PR に分けます。このワークショップでは手順を簡潔にするため、フィルタリングと品質確認の作業を一つの会話とブランチで進め、一つの PR にまとめました。

このレッスンでは、次のことを行います。

- Agent Merge と、マージまでの作業を自動化する方法を確認します。
- 変更全体と検証結果をレビューします。
- フィルタリングの PR を作成します。
- レビュー後にのみ Agent Merge を有効にし、PR がマージされたことを確認します。

## シナリオ

フィルタリングの作業では、Copilot を使って機能を計画、実装、検証しました。Tailspin Toys では、マージの許可を開発者が管理しながら、PR の残りの作業を自動化したいと考えています。

## Agent Merge について

**Agent Merge** は、プルリクエストをマージ可能にするために残っている作業を自動化します。有効にすると、継続的インテグレーション (CI) の失敗への対応、レビュー コメントへの返信、必要に応じた rebase を行い、リポジトリが許可していれば GitHub の自動マージを有効にします。Agent Merge を使う場合でも、事前に変更をレビューし、マージ可能と判断してください。

## Agent Merge で PR を管理する

コードのレビューと PR の作成を行い、残りの処理を Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェント ダイアログを開きます。
3. **Default** を選択し、<kbd>Enter</kbd> を押します。
4. `/pr create` を実行して PR を作成します。
5. `/pr agentmerge` を実行して Agent Merge を有効にします。
6. Copilot が PR の CI を監視し、すべて成功したらマージすることを確認します。
7. `PR #14 was squash-merged successfully.` のような Copilot のメッセージを確認します。

> [!IMPORTANT]
> Agent Merge は、必須レビュー、ブランチ保護、マージ キュー、リポジトリ設定、権限の不足を回避しません。処理がブロックされた場合は理由を確認し、リポジトリで許可されている手順に従って手動でマージします。

## まとめと次のステップ

コード生成、テスト、検証に加えて、プルリクエストの処理も自動化しました。

- Agent Merge と、マージまでの作業を自動化する方法を確認しました。
- 変更全体と検証結果をレビューしました。
- フィルタリングの PR を作成しました。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認しました。

次は、コンテキスト、モデル、共有、cloud agent への任意の委任に使える[便利な Copilot CLI スラッシュ コマンドを確認します][next-lesson]。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
