---
title: "レッスン 1 - GitHub Copilot CLI をインストールする"
description: "Codespace に Copilot CLI をインストールして認証し、基本操作を確認して、フィルタリングの Issue を見つけます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] は、ターミナルで動作するエージェント型コーディング アシスタントです。コードベースの探索、コード生成、コマンド実行、外部ツールとの連携をコマンドラインから行えます。タスクを任せたり、変更を依頼したりできます。まず Copilot CLI をインストールします。

このレッスンでは、次のことを行います。

- npm で GitHub Copilot CLI をインストールします。
- GitHub アカウントで認証します。
- ワークショップのリポジトリを信頼し、簡単な会話を試します。
- 組み込みの GitHub MCP サーバーを使って、フィルタリングの Issue を見つけます。

## シナリオ

チームでは、増え続けるバックログに取り組むため、AI エージェントを使い始めています。Copilot CLI は多くの開発者が日常的に使うターミナルでその機能を提供します。このレッスンでインストールと認証を済ませ、残りのワークショップに備えます。

## Copilot CLI をインストールする

Copilot CLI は [npm][install-cli]、WinGet、Homebrew でインストールできます。GitHub Codespaces には Node.js が含まれているため、ここでは npm を使います。

1. Codespace に戻り、ターミナルを開きます。
2. Node.js がインストールされ、必要なバージョンを満たしていることを確認します。

   ```bash
   node --version
   ```

   バージョン 24 以上が表示されます。

3. Copilot CLI をグローバルにインストールします。

   ```bash
   npm install -g @github/copilot
   ```

4. インストールを確認します。

   ```bash
   copilot --version
   ```

   バージョン番号が表示されます。

## GitHub で認証する

初回起動時に、Copilot CLI から GitHub アカウントでの認証を求められます。

1. Copilot CLI を起動します。

   ```bash
   copilot
   ```

2. 求められたら、device code の手順に従って認証し、Copilot CLI のアクセスを許可します。
3. Copilot CLI が次のように表示したら、パスが Tailspin Toys リポジトリであることを確認します。

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. **Yes, and remember this folder for future sessions** を選択します。

> [!NOTE]
> Codespace では GitHub セッションを通じて認証済みの場合があります。認証を求められずに Copilot CLI が起動した場合は、そのまま進めてください。

## 基本操作を確認する

通常のシェル プロンプトに入力したコマンドは Codespace で実行されます。Copilot CLI の起動後は、自然言語をエージェントに送り、スラッシュ コマンドで会話を操作します。

1. `/model` を入力し、矢印キーで **Auto** を選択して <kbd>Enter</kbd> を押し、もう一度 <kbd>Enter</kbd> を押して確定します。
2. `/help` を入力して、インストール済みバージョンのコマンドを確認します。<kbd>Esc</kbd> でヘルプ画面を閉じます。
3. 次の質問を送り、正しく動作することを確認します。

   ```plaintext
   What are the key files in this project?
   ```

4. Copilot がリポジトリを調べてから回答することを確認します。
5. `/mcp list` を入力し、組み込みの GitHub MCP サーバーが利用できることを確認します。
6. 次のプロンプトでフィルタリングの Issue を探します。

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. 表示された URL を開き、Issue の内容を読みます。最初の変更が終わった後に使います。

> [!TIP]
> 通常の Copilot CLI セッションは、ターミナルで現在チェックアウトしているブランチを使い、自動で worktree を作成しません。変更を始める前に機能ブランチを作成します。

## ワークショップ用のショートカットを使う

Copilot CLI は、許可されていないツールを使う前に確認を求めます。このワークショップでは、Codespace 内で承認プロンプトを省略して演習に集中できるよう、`--yolo` を付けて再起動します。

> [!CAUTION]
> `--yolo` は、すべてのツール、パス、URL を許可する `--allow-all-tools`、`--allow-all-paths`、`--allow-all-urls` を有効にします。Codespace や VM などの分離された環境でのみ使い、日常的な開発の既定値として alias に設定しないでください。詳細は[ツールの許可と拒否][allow-all-warning]を参照してください。

`--enable-all-github-mcp-tools` は、後のレッスンで Issue や PR を操作するための GitHub MCP の読み取り・書き込みツールを有効にします。Codespace によってローカル コンピューターへのアクセスは制限されますが、認証済みの GitHub リソースは実際のものです。公開やマージの前に変更をレビューしてください。

1. `/exit` で Copilot CLI を終了します。
2. リポジトリのルートから再起動します。

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. プロジェクトについて簡単な質問を送り、会話が動作することを確認してから `/exit` で終了します。

Copilot は会話を自動的に保存します。後で命令を変更したりエージェントを追加したりしたら、`copilot --resume` で同じ会話とブランチを再開します。

## まとめと次のステップ

このレッスンでは、次のことを行いました。

- npm で GitHub Copilot CLI をインストールしました。
- GitHub アカウントで認証しました。
- ワークショップのリポジトリを信頼し、会話を試しました。
- 組み込みの GitHub MCP サーバーを使って、フィルタリングの Issue を見つけました。

次は[最初の変更に取り組み][next-lesson]、ゲーム カードに星評価を表示します。

## リソース

- [GitHub Copilot CLI をインストールする][install-cli]
- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
