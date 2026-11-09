---
title: "レッスン 0 - 前提条件"
description: "Tailspin Toys のコピーを作成し、Copilot CLI ワークショップ用の GitHub Codespace を準備します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI のレッスンを始める前に、必要な準備を整えます。Tailspin Toys リポジトリの自分用コピーを作成し、[Codespace][codespaces] を立ち上げます。次のレッスンでは、統合ターミナルを使って Copilot CLI をインストールし、実行します。

このレッスンでは、次のことを行います。

- テンプレートから Tailspin Toys プロジェクトのコピーを作成します。
- Codespace を作成し、プロジェクトの準備ができたことを確認します。

## ラボ用リポジトリを設定する

ラボで作成するコードには、自分用の Tailspin Toys リポジトリを使います。[テンプレート リポジトリ][tailspin-template]からコピーを作成してください。新しいリポジトリには、演習に必要なファイルがすべて含まれています。

1. 新しいブラウザー ウィンドウで[Tailspin Toys テンプレート][tailspin-template]を開きます。
2. **Use this template**、**Create a new repository** の順に選択します。
3. GitHub または Microsoft が主催するイベントに参加している場合は、メンターの案内に従います。それ以外の場合は、GitHub Copilot を利用できる organization にリポジトリを作成します。
4. 後で使うため、作成したリポジトリのパス（`organization-or-user-name/repository-name`）を控えておきます。

> [!NOTE]
> テンプレートからリポジトリを作成すると、GitHub Issue のバックログも自動的に作成されます。ワークショップではこの Issue を使うため、自分で登録する必要はありません。

新しいワークショップ テンプレートを使ってください。リポジトリには命令ファイル、アプリケーション コード、テスト、`quality-checks` スキル、バックログが含まれます。古いコピーを使う場合は、必要なファイルがあるか事前に進行役へ確認してください。

## Codespace を作成する

次に、Codespace を使ってワークショップを進めます。[GitHub Codespaces][codespaces] は、ブラウザーから直接コードを作成、実行、デバッグできるクラウド開発環境です。

1. 作成したリポジトリを開きます。
2. **Code** を選択します。
3. **Codespaces** タブを選び、**Create codespace on main** を選択します。
4. Codespace のセットアップが完了するまで待ちます。テンプレートがプロジェクトの依存関係、Playwright Chromium、ローカル データベースを準備します。
5. **Do you trust the authors of the files in this folder?** と表示されたら、**Trust Folder & Continue** を選択します。
6. リポジトリのルートでターミナルを開き、アプリを起動します。

   ```bash
   npm run dev
   ```

7. Codespaces でポート `4321` が利用可能になったら **Open in Browser** を選択し、Tailspin Toys のサイトが読み込まれることを確認します。
8. ターミナルに戻り、<kbd>Ctrl</kbd>+<kbd>C</kbd> で開発サーバーを停止します。

## まとめと次のステップ

このレッスンでは、次のことを行いました。

- テンプレートから Tailspin Toys プロジェクトのコピーを作成しました。
- Codespace を作成し、プロジェクトの準備ができたことを確認しました。

次は Codespace に[GitHub Copilot CLI をインストールし][next-lesson]、GitHub アカウントで認証します。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces を使い始める][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-install-copilot-cli/
[codespaces]: https://github.com/features/codespaces
