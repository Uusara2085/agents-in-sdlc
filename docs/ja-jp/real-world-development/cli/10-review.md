---
title: "レッスン 10 - 振り返りと次のステップ"
description: "Copilot CLI のワークフロー、2つのプルリクエスト、再利用できるカスタマイズ、関連リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys で一連の作業を進めました。

- Codespace を準備して Copilot CLI をインストールし、プロジェクトを確認して、フィルタリングの Issue を見つけました。
- 星評価を追加し、転送されたブラウザーで確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルタリングの Issue から作業を始め、Plan モードで方針を決め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム命令でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、ユニットテスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルタリングを確認しました。
- 品質保証 (QA) カスタム エージェントを作成して選択し、要件、テスト範囲、スキルの結果、ブラウザー上の証拠を評価しました。
- フィルタリングの変更全体をレビューし、Agent Merge によるマージを承認しました。
- コンテキスト、モデル、共有、cloud agent への任意の委任に使えるスラッシュ コマンドを確認しました。

## 作成したもの

このワークショップでは、更新した `main` からそれぞれブランチを作り、2つの PR を作成しました。

1. **星評価:** 既存の `starRating` と未評価状態をゲーム カードに表示します。
2. **フィルタリングと品質ワークフロー:** フィルタリングを実装し、命令を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルと関連テストを追加します。

フィルタリングの計画から PR の作成までは、同じ会話とブランチを使いました。ワークショップを簡潔にするため、作業を一つの PR にまとめています。

## 検証方法の違い

自動テスト、自分で行うブラウザー確認、MCP を通じた Copilot のブラウザー確認を組み合わせました。`quality-checks` スキルはユニットテスト、lint、型チェックを実行し、設定した形式で結果を報告します。QA エージェントは、それらの結果と要件、テスト範囲のレビューをまとめます。

追加するテストは実際の不足を補うものにします。QA の実行で追加テストが不要と判断される場合もあります。ツールの不足、スキップされたチェック、失敗は明示すべき阻害要因であり、成功ではありません。マージを許可する前にコードと検証結果を確認し、変更後は関連する証拠を更新してください。

## ベスト プラクティス

Copilot に与えるコンテキストとツールが、作業結果を左右します。このワークショップでは、命令を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを設定しました。命令は標準を、スキルは繰り返し作業を、カスタム エージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合った**モードとモデル**を選びます。**Plan** は実装前の検討、**Interactive** は細かな変更を一緒に進める場合、**Autopilot** は範囲が明確なタスクに適しています。定型的な編集には高速なモデル、複雑な作業にはより高性能なモデルを選びます。

何を、なぜ、どのように作るかを明確に伝えることも重要です。

## さらに確認する

Copilot CLI には、次の機能もあります。

- `/review` でコード レビュー エージェントに変更を分析させます。
- `/rubber-duck` で問題を説明し、別の視点を得ます。
- `/fleet` で独立したサブタスクを並行して進めます。
- `/worktree` で別のタスクを分離します。
- `/delegate` で Copilot cloud agent にタスクを委任します。

## 次のステップ

ツールの使い方を身に付けるには、実際に使い続けるのが一番です。業務や個人のプロジェクトで試し、学んだことをチームと共有してください。ターミナルから Tailspin Toys を拡張するには、任意の[Foundry Backer Concierge シリーズ][foundry]に進みます。別の環境を試す場合は、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
