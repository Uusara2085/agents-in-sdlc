---
title: "演習 1 - カスタム命令 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: エージェント モード →][next-lesson]

生成 AI を使うときは、Copilot が参照できるコンテキストを用意することが重要です。[命令ファイル][instruction-files]を使うと、コード生成の指針を伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム命令とパスに応じた命令が Copilot に適用される方法を確認します。
- 既存の命令でフィルタリング用のデータ取得ヘルパーを生成します。
- `.github/copilot-instructions.md` にリポジトリ全体の標準を追加します。
- 同じプロンプトを再実行し、生成コードが新しい標準に従うことを確認します。
- 命令とフィルタリングの基礎を `main` にコミットし、次の演習に備えます。

> [!CAUTION]
> Copilot の生成結果は確率的であり、設定した標準から外れる場合があります。命令を更新する前後で、文字単位の一致ではなく傾向の変化を確認してください。

## 命令ファイル

### シナリオ

Tailspin Toys には、データ層にユニットテストを追加すること、ユーザー インターフェイス (UI) をダークモードで現代的な見た目にすること、TypeScript Documentation (TSDoc) コメントとファイル ヘッダーを追加することなどの開発ガイドラインがあります。命令ファイルを使い、Copilot がこれらの開発習慣に沿って作業できるようにします。

### カスタム命令

カスタム命令は、コーディング規約やライブラリなどのコンテキストを Copilot に伝えます。

- `.github/copilot-instructions.md` は、リポジトリへのすべてのリクエストに適用するプロジェクト全体の情報を記載します。
- `.github/instructions/*.instructions.md` は、TypeScript、Astro、UI コンポーネント、ユニットテストなど、特定のファイル形式やタスクに適用します。

> [!NOTE]
> 統合開発環境 (IDE) では、命令ファイルは Copilot Chat のコード生成に使われます。コード補完や次の編集候補には使われません。Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ単位の命令と `applyTo` frontmatter を持つ `*.instructions.md` の両方を使います。Copilot は AGENTS.md や CLAUDE.md などの形式もサポートしています。詳しくは[カスタム命令のサポート][custom-instructions-support]を参照してください。

### 命令ファイルを管理するためのベスト プラクティス

- `copilot-instructions.md` にはプロジェクトの説明、構成、全体の標準を記載します。
- `*.instructions.md` には、ユニットテスト、Astro コンポーネント、データ層など、特定のファイル形式やタスク向けの指示を記載します。
- 平易な言葉を使い、コードの良い例と悪い例を示します。

> [!TIP]
> プロジェクトには [UI の命令][ui-instructions]や [Astro の命令][astro-instructions]などが含まれています。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` を使って、Copilot に命令ファイルの生成を依頼することもできます。テンプレートは [awesome-copilot][awesome-copilot]で確認できます。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム命令を確認する

プロジェクトに含まれる命令を確認し、Copilot に渡すコンテキストを把握します。

1. `.github/copilot-instructions.md` を開き、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の **GitHub Actions Workflows** の指針も確認してください。
2. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの命令ファイルを確認します。
3. `.github/instructions/unit-tests.instructions.md` を開き、`applyTo` が命令の対象ファイルを決める glob であることを確認します。
4. ユニットテストに関する命令を読みます。
5. `.github/instructions/drizzle.instructions.md` の末尾にある他の命令ファイルやプロジェクト ファイルへのリンクを確認します。パスは命令ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** にはコーディング標準が記載されていますが、コード内のドキュメントに関するルールはまだありません。

## 変更用ブランチを作成する

命令とヘルパーの変更をフィルタリングの作業から分けるため、専用ブランチを作成します。

1. 前の演習で使った Codespace に戻ります。
2. Mac では <kbd>Control</kbd>+<kbd>\`</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>\`</kbd> を押して新しいターミナルを開きます。
3. 新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 命令を更新する前に Copilot Chat を使う

命令を変更する前にプロンプトを送り、現在の指示で Copilot が生成する内容を確認します。

1. Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択します。
2. 前の演習で開いたエディター タブを閉じます。
3. `src/lib/publishers.ts` を開きます。
4. Chat ビューのエージェント選択メニューで **Agent** を選びます。
5. モデルの一覧で **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> このモデルの記載は、特定のモデルを推奨するものではありません。ワークショップの作成時に使ったモデルを記載しています。大規模言語モデル (LLM) は確率的に動作するため、生成結果が異なる場合があります。

6. Copilot に次のプロンプトを送ります。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

7. 生成されたヘルパーが型付き関数であり、データ層の規約に従って `db` クライアントを最初の引数に受け取り、パブリッシャーの型付き配列を返すことを確認します。
8. TSDoc コメントとファイル ヘッダーがまだないことを確認します。Copilot の結果は確率的なため、コメントが追加される場合もあります。

## リポジトリ全体の標準を追加する

Copilot の現在の出力を確認した後、命令ファイルに新しい標準を加えます。

1. `.github/copilot-instructions.md` を開き直します。
2. **Code formatting requirements** セクションの末尾に次の行を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

3. `copilot-instructions.md` を保存します。

## プロンプトを再実行して変化を確認する

1. Copilot Chat で **New Chat** を選択します。
2. `src/lib/publishers.ts` を開き、Copilot が対象ファイルを把握できるようにします。
3. 先ほどと同じプロンプトを送ります。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 生成されたファイルの先頭に、ファイルの役割を説明するコメントがあることを確認します。
5. 関数に目的、パラメーター、戻り値を説明する TSDoc コメントが含まれていることを確認します。

## 命令をコミットしてブランチをプッシュする

命令とヘルパーの変更を確認し、ブランチをリポジトリに公開します。

1. Mac では <kbd>Control</kbd>+<kbd>\`</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>\`</kbd> を押して新しいターミナルを開きます。
2. 変更を確認します。

   ```bash
   git status
   ```

3. 命令とヘルパーの変更をステージしてコミットします。`git status` に追加のファイル（テストなど）が表示された場合は、それらも追加します。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status に他の関連ファイルがあれば、それらも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プルリクエストを作成してマージする

GitHub のツールを使って、命令ファイル更新の Issue に関連付けたプルリクエスト (PR) を作成し、マージします。

1. Codespace の Copilot Chat で **New Chat** を選択し、エージェント選択メニューで **Agent** を選びます。
2. Mac では <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>、Windows/Linux では <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> を押して Copilot Chat ビューを開きます。
3. 次のプロンプトで Issue を探し、現在のブランチから PR を作成するよう依頼します。

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が GitHub 操作の許可を求めたら、コマンドを確認して適切な場合に **Allow** を選択します。
5. PR が作成されたら、次のプロンプトでマージしてローカル ブランチを更新するよう依頼します。

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

6. GitHub 操作やシェル コマンドの許可を求められたら、内容を確認し、適切な場合に **Allow** を選択します。

## まとめと次のステップ

命令ファイルが Copilot にコンテキストを与える方法を確認し、VS Code の Copilot Chat で同じコード生成プロンプトを使いました。

- 既存の命令で Copilot が生成するコードを確認しました。
- `.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。
- 同じプロンプトを再実行し、新しい標準が反映されることを確認しました。
- 命令の更新とヘルパーの基礎をコミットし、`main` にマージしました。

次は[エージェント モードでコードベース全体に機能を追加します][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う命令ファイル][instruction-files]
- [カスタム命令のベスト プラクティス][instructions-best-practices]
- [Copilot 向けのより良いカスタム命令を書くための5つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム命令][personal-instructions]
- [命令ファイルなどを集めた Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
