---
title: "演習 1 - カスタム命令 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクの進め方に決まりがある場合や、Copilot に知っておいてほしい背景情報がある場合は、その情報を参照できるようにします。[命令ファイル][instruction-files]を使うと、Copilot に「何を」するかだけでなく、「どのように」行うかも伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム命令とパスに応じた命令ファイルを確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code や CLI の演習とは異なり、ここでは命令の変更前後を比較するプロンプトを実行しません。Copilot cloud agent は GitHub Issue に基づいて非同期に動作するため、リアルタイムで並べて効果を示すのが難しいためです。この環境の後半で cloud agent が作成するプルリクエストをレビューするときに、命令ファイルの影響を確認します。

## 命令ファイル

### シナリオ

Tailspin Toys には、開発に関するガイドラインがあります。

- データ層には必ずユニットテストを追加します。
- UI はダークモードにし、現代的な見た目にします。
- コードには TypeScript Documentation (TSDoc) のドキュメント コメントを追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメント ブロックを追加します。

命令ファイルを使い、Copilot がこれらの開発習慣に沿って作業できるようにします。

### カスタム命令

カスタム命令は、コーディング スタイルや要件などのコンテキストを Copilot に伝えます。リポジトリ全体に適用する命令と、特定のファイルやタスクに適用する命令を作成できます。

- `.github/copilot-instructions.md` は、リポジトリへのすべてのリクエストで Copilot に渡される単一の命令ファイルです。技術スタック、プロジェクトの概要、共通のベスト プラクティスなど、広く関係する情報を記載します。
- `.github/instructions/*.instructions.md` は、特定の言語やファイルの種類（TypeScript や Astro など）、または UI コンポーネントやユニットテストの作成などのタスクに適用する命令ファイルです。

> [!NOTE]
> IDE では、命令ファイルは Copilot Chat のコード生成に使われます。コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ単位の命令と `applyTo` frontmatter を持つ `*.instructions.md` ファイルの両方を使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの形式の命令ファイルもサポートしています。詳しくは[カスタム命令のサポート][custom-instructions-support]を参照してください。

### 命令ファイルを管理するためのベスト プラクティス

サンプル プロジェクトには、代表的な構成の命令ファイルが用意されています。

- `copilot-instructions.md` には、構築するもの、プロジェクト構成、全体に適用するコーディング標準などを記載します。
- `*.instructions.md` は、ユニットテスト、Astro コンポーネント、データ層など、特定のファイル形式やタスク向けに使います。
- 平易な言葉で、明確なガイダンスとコードの良い例・悪い例を示します。

命令ファイルの作成方法は一つではありません。実際に試し、プロジェクトに合う方法を見つけてください。

> [!TIP]
> このプロジェクトには [UI の命令][ui-instructions]や [Astro の命令][astro-instructions]など、さまざまなタスク向けの命令ファイルがあります。Copilot に命令ファイルの生成を依頼することもできます。VS Code では **Configure Chat → Generate Agent Instructions**、Copilot CLI では `/init` を使います。テンプレートを探す場合は、命令ファイルやカスタム エージェントなどを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム命令ファイルを確認する

リポジトリに用意された命令ファイルを確認し、Copilot に与えるプロジェクトのコンテキストを把握します。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の **GitHub Actions Workflows** に関するガイダンスも確認してください。これらの命令は、このリポジトリで Copilot を使う際に適用されます。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの命令ファイルを確認します。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、適用対象のファイルを決める glob であることを確認します。ここでは、たとえば `**/*.test.ts` に一致する TypeScript のテスト ファイルが対象です。
5. このプロジェクトでユニットテストを作成する際の命令を確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、末尾にある他の命令ファイル（`unit-tests.instructions.md` など）やプロジェクト内のファイルへのリンクを確認します。これらのパスはリポジトリのルートではなく、命令ファイルの場所を基準にしています。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはコーディング標準が記載されていますが、コード内のドキュメントに関する規則はまだありません。次の手順で TSDoc コメントとファイル先頭のコメントを追加します。

## リポジトリ全体に適用する標準を追加する

cloud agent が後の演習で割り当てられた Issue に取り組むときに、追加した命令を使えるようにします。まずブランチを作成します。

1. Codespace のターミナルで新しいブランチを作成し、切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`copilot-instructions.md` に、コード内のドキュメントに関するリポジトリ全体の標準を追加します。

1. `.github/copilot-instructions.md` を開き直します。
2. **Code formatting requirements** セクションを探します。この標準には、コード内のドキュメントに関するルールがまだありません。
3. 既存の標準の直後に、次の行を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 命令ファイルは、リポジトリ全体に適用する `.github/copilot-instructions.md` と、特定の言語、ファイル形式、タスクに適用する `*.instructions.md` のどちらにも作成できます。コード コメントの規則のようにプロジェクト全体に関わる標準には、リポジトリ単位のファイルが適しています。

## 命令の変更をコミット、プッシュ、マージする

次の演習で cloud agent が `main` からブランチを作成するときに新しい命令を読み込めるよう、変更を `main` に反映します。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` に向けたプルリクエストを作成し、マージします。

> [!TIP]
> この演習では `main` に直接作業してもかまいません。その場合はブランチ作成を省略して、`main` に直接コミットします。ブランチを使う手順は、実際のプロジェクトでの作業方法に近づけるためのものです。

## まとめと次のステップ

このプロジェクトの命令ファイルから Copilot がコンテキストを得る方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。以降の演習で、cloud agent が作成するプルリクエストにこの標準が反映されます。

次は[最初の Issue を Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う命令ファイル][instruction-files]
- [カスタム命令を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 向けのより良いカスタム命令を書くための5つのヒント][copilot-instructions-five-tips]
- [命令ファイルなどを集めた Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
