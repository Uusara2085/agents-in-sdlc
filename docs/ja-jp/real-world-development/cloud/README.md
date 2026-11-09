---
slug: ja-jp/real-world-development/cloud
title: "GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** を使うと、GitHub Copilot をクラウド上で非同期に動作させられます。GitHub で作業を割り当てると、cloud agent はバックグラウンドでリポジトリを調べ、変更を加え、プルリクエストを作成します。その間、開発者は別の作業を進められます。

各演習では、まず cloud agent が従うカスタム命令を追加し、GitHub Issue を割り当てて実装を依頼します。カスタム エージェントを確認して使い、エージェントのダッシュボードからセッションを監視して作業の方向を調整し、最後にプルリクエストをレビューして結果を改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. カスタム命令][ex1] | コンテキスト | cloud agent が従うカスタム命令を追加します |
| [2. Cloud agent][ex2] | 非同期エージェント | GitHub Issue を Copilot cloud agent に割り当てます |
| [3. カスタム エージェント][ex3] | 専門エージェント | カスタム エージェントを確認して使います |
| [4. エージェントの管理][ex4] | 監視 | エージェントのセッションを監視し、方向を調整します |
| [5. 反復して改善する][ex5] | レビュー | プルリクエスト (PR) をレビューし、Copilot の作業を改善して、次のステップを選びます |

## 前提条件

このワークショップを始める前に、次のものを準備してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** プランがある GitHub アカウント
- [ ] アカウントまたは組織で Copilot cloud agent が有効になっていること

> [!TIP]
> 有料プランがない場合、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使用するエージェント、Model Context Protocol (MCP)、コードレビュー、Copilot CLI の機能が含まれています。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Cloud agent は **Copilot Student、Pro、Pro+、Business、Enterprise** で利用できます。Copilot Free は対象外です。Copilot Business または Enterprise では、管理者が組織で有効にする必要があります。

> [!NOTE]
> この環境では Model Context Protocol (MCP) を扱いません。Copilot で MCP サーバーを使う方法については、[CLI ワークショップ](../cli/)または [VS Code ワークショップ](../vscode/)を参照してください。

## 始める

**[演習 0: 前提条件から始める][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
