---
title: "レッスン 9 - GitHub Copilot CLI のスラッシュ コマンド"
description: "コンテキスト管理、モデル選択、セッション共有、cloud agent への任意の委任に使えるスラッシュ コマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

GitHub Copilot CLI には、多くのスラッシュ コマンドがあります。これまでに `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` を使いました。ここでは、さらに便利なコマンドを確認します。

このレッスンでは、次のことを行います。

- `/context` と `/compact` で会話のコンテキスト管理を確認します。
- `/model` で利用可能なモデルを確認します。
- `/share` でセッションをエクスポートまたは共有する方法を確認します。
- 並列作業、worktree、cloud agent への委任に使えるコマンドを確認します。

## シナリオ

CLI の基本的なワークフローを終えたので、コンテキストの管理、モデルの切り替え、セッションの共有、[Copilot cloud agent][about-cloud-agent]への任意の委任を確認します。

## Copilot CLI のコンテキストを確認する

複雑なタスクでは、モデルのコンテキスト ウィンドウの上限に達することがあります。Copilot CLI は必要に応じて会話を自動的に圧縮しますが、スラッシュ コマンドで確認、実行することもできます。

1. Codespace に戻り、Copilot CLI が起動していない場合はリポジトリのルートから起動します。
2. `/context` を入力します。
3. モデル、現在のトークン使用量、システム命令、ツール、メッセージ、空き領域への割り当てを確認します。
4. `/compact` を入力して会話を圧縮します。
5. もう一度 `/context` を入力し、結果を比べます。会話が短い場合、変化が小さいことがあります。

> [!NOTE]
> コンテキスト ウィンドウがいっぱいになると、Copilot CLI は自動的に圧縮します。タイミングを選びたい場合は `/compact` を使います。無関係なタスクに移るときに会話を新しくするには、`/clear` または `/new` を使います。

## モデルを選ぶ

利用可能なモデルと使用状況を確認し、必要に応じてモデルを変更します。

1. `/model` を入力します。
2. 利用可能なモデルと使用状況を確認します。
3. 現在のモデルを維持するか、別のモデルを選ぶか、<kbd>Esc</kbd> で一覧を閉じます。

## セッションを共有する

`/share` は、セッションを Markdown または HyperText Markup Language (HTML) ファイルにエクスポートしたり、共有リンクを作成したり、GitHub gist として公開したりできます。

1. `/help` を入力し、インストール済みバージョンの `/share` オプションを確認します。
2. 共有する場合は、たとえばローカルに Markdown を出力する `/share file` など、目的に合う方法を選びます。
3. エクスポートした内容を、送信または公開する前に確認します。プロンプト、応答、プロジェクトの詳細が含まれる場合があります。

リンクや gist の公開は任意です。チームが共有を意図していないリポジトリや会話の内容は公開しないでください。

## 省略可能: 作業の拡張や委任

基本のワークショップは完了です。より大きなタスクには、次のコマンドも利用できます。

- `/fleet` は独立したサブタスクをサブエージェントに分割し、並行して実行します。
- `/worktree` は別のタスク用に分離された Git worktree を作成します。
- `/delegate` はタスクを Copilot cloud agent に送り、非同期で処理してプルリクエストを作成する場合があります。

これらのコマンドは追加の worktree やリモート作業を作成するため、任意です。試すときは新しい範囲の明確なタスクから始め、通常のワークフローで結果をレビューしてください。非同期エージェントについて詳しく知るには、[cloud agent ワークショップ][cloud-workshop]に進みます。

## まとめと次のステップ

スラッシュ コマンドを使って Copilot CLI を設定し、セッションを共有し、内部の状態を確認しました。

- `/context` と `/compact` で会話のコンテキスト管理を確認しました。
- `/model` で利用可能なモデルを確認しました。
- `/share` でセッションをエクスポートまたは共有する方法を確認しました。
- 並列作業、worktree、cloud agent への任意の委任に使えるコマンドを確認しました。

ほかのコマンドもあります。次は[ここまでの内容を振り返り、次のステップを確認します][next-lesson]。

## リソース

- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
