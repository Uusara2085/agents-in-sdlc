---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Copilot cloud agent の演習を始める前に、必要な準備を整えます。Tailspin Toys リポジトリの自分用コピーを作成し、[Codespace][codespaces] を立ち上げます。Codespace は、命令ファイルの編集と cloud agent が作成した変更のレビューに使います。

## ラボ用リポジトリを設定する

コードを作成するためのリポジトリのコピーを、[テンプレート][template-repository]から作成します。新しいリポジトリには、演習に必要なファイルが含まれています。

1. 新しいブラウザー ウィンドウで[Tailspin Toys テンプレート][tailspin-template]を開きます。
2. ラボ用リポジトリで **Use this template** を選択し、次に **Create a new repository** を選択します。

   ![「Use this template」ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントの一環として参加している場合は、メンターの案内に従います。それ以外の場合は、GitHub Copilot を利用できる organization にリポジトリを作成します。

   ![リポジトリ テンプレートの設定を入力する画面](../../../_images/ex0-repository-settings.png)

4. 後で使うため、作成したリポジトリのパス（`organization-or-user-name/repository-name`）を控えておきます。

## Codespace を作成する

次に、Codespace を使って演習を進めます。[GitHub Codespaces][codespaces] は、ブラウザーから直接コードを作成、実行、デバッグできるクラウド開発環境です。

1. 作成したリポジトリを開きます。
2. **Code** を選択します。

   ![Code ボタンを選択する画面。](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選び、**+** を選択して Codespace を作成します。

   ![新しい Codespace を作成する](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかりますが、サービスを手動でインストールするよりも早く完了します。その間に、次の演習で詳しく確認する GitHub Copilot の機能を試せます。

> [!CAUTION]
> 後の演習で Codespace に戻ります。今はブラウザーのタブで開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの [dev container][dev-containers] で実行できます。どちらも必要な前提条件が整った環境を提供します。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、プロンプトが表示されたら **Reopen in Container** を選択します。Codespace と同じ dev container が構築されます。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## まとめ

ラボ用リポジトリのコピーを作成し、Codespace の作成を開始しました。以降の演習で、この Codespace を使って Copilot cloud agent と作業します。

## 次のステップ

cloud agent が従うカスタム命令を追加します。[演習 1 - カスタム命令][next-lesson]に進みます。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の使用を開始する][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
