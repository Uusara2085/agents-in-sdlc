---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の演習を始める前に、Tailspin Toys リポジトリのコピーを作成し、作業用の [Codespace][codespaces] を立ち上げ、エディターで GitHub Copilot Chat が動作することを確認します。

## ラボ用リポジトリを設定する

コードを作成するためのリポジトリのコピーを、[テンプレート リポジトリ][template-repository]から作成します。

1. 新しいブラウザー ウィンドウで[Tailspin Toys テンプレート][tailspin-template]を開きます。
2. **Use this template**、**Create a new repository** の順に選択します。

   ![「Use this template」ボタン。](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントに参加している場合は、メンターの案内に従います。それ以外の場合は、GitHub Copilot を利用できる organization にリポジトリを作成します。

   ![リポジトリ テンプレートの設定を入力する画面。](../../../_images/ex0-repository-settings.png)

4. 後で使うため、作成したリポジトリのパス（`organization-or-user-name/repository-name`）を控えておきます。

> [!NOTE]
> テンプレートからリポジトリを作成すると、GitHub Issue のバックログも自動的に作成されます。ワークショップではこの Issue を使うため、自分で登録する必要はありません。

## Codespace を作成する

次に、Codespace を使って演習を進めます。[GitHub Codespaces][codespaces] は、ブラウザーから直接コードを作成、実行、デバッグできるクラウド開発環境です。

1. 作成したリポジトリを開きます。
2. **Code** を選択します。

   ![Code ボタンを選択する画面。](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選び、**+** を選択して Codespace を作成します。

   ![新しい Codespace を作成する画面。](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかります。準備ができるまで、GitHub Copilot の機能を確認できます。

> [!CAUTION]
> 後の演習で Codespace に戻ります。今はブラウザーのタブで開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの [dev container][dev-containers] で実行できます。ローカルで進める場合は、クローンしたリポジトリを VS Code で開き、プロンプトが表示されたら **Reopen in Container** を選択します。Codespace と同じ dev container が構築されます。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## GitHub Copilot Chat と agent mode を使う

VS Code で GitHub Copilot Chat の agent mode を使うには、IDE に GitHub Copilot Chat 拡張機能が必要です。GitHub Codespace では、通常すでにインストールされています。

> [!TIP]
> 拡張機能がない場合は、[Visual Studio Code Marketplace からインストール][copilot-chat-extension]するか、VS Code の Extensions ビューで **GitHub Copilot Chat** を検索し、**Install** を選択します。

拡張機能をインストールした後、GitHub アカウントでの認証が必要になる場合があります。

1. Codespace に戻ります。
2. エディター右側に Copilot Chat が表示されていない場合は、上部の **Copilot Chat** アイコンを選択します。
3. Copilot Chat に `Hello world` などのメッセージを入力し、<kbd>Enter</kbd> を押します。
4. GitHub アカウントへのサインインを求められた場合は、画面の指示に従って認証します。
5. 認証後に Copilot Chat が表示されることを確認します。

   ![Copilot Chat の認証プロンプトの例。](../../../_images/ex1-copilot-authentication.png)

## まとめ

ラボ用リポジトリのコピーを作成し、Codespace の準備を始めました。コードを書くときに使う Copilot Chat も確認しました。

## 次のステップ

Copilot にプロジェクトの規約を伝えます。[演習 1 - カスタム命令][next-lesson]に進みます。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces を使い始める][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
