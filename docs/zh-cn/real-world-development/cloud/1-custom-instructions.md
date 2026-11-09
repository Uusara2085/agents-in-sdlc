---
title: "练习 1 - 自定义说明（云端智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云端智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，或 Copilot 需要了解背景信息，就应确保它能够获取这些上下文。[说明文件][instruction-files]可提供此类指导，帮助 Copilot 理解不仅要做什么，还要如何完成。

在本练习中，你将：

- 了解项目上下文、编码指南和文档标准如何通过存储库自定义说明及按路径应用的说明文件传递给 Copilot。
- 在 `.github/copilot-instructions.md` 中添加新的存储库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作坊不同，本工作坊不会使用“更新前/更新后”提示词比较，因为 Copilot 云端智能体会在 GitHub 上异步处理议题，难以实时并排展示效果。后续审查智能体生成的拉取请求时，可以看到说明文件的影响。

## 说明文件

### 场景

Tailspin Toys 有一套开发指南和要求，包括：

- 数据层始终需要单元测试。
- 用户界面应采用深色模式并具有现代感。
- 代码应通过 TypeScript 文档注释（TSDoc）添加说明。
- 每个文件开头都应添加描述文件用途的注释块。

通过说明文件，可以确保 Copilot 了解这些实践要求，并据此执行任务。

### 自定义说明

自定义说明为 Copilot 提供上下文和偏好，帮助它了解你的编码风格和要求。你可以指定编码规范、库以及注释风格。说明文件可以应用于整个存储库，也可以应用于特定类型的文件或任务。

说明文件有两种类型：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送给 Copilot 的单个说明文件。它应包含与大多数请求相关的项目级信息，例如技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：针对特定任务或文件类型提供指南，例如 TypeScript、Astro、创建 UI 组件或编写单元测试。

> [!NOTE]
> 在集成开发环境中，说明文件只用于 Copilot Chat 代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云端智能体在生成代码时都会使用存储库级说明文件和带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他规范的说明文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理说明文件的最佳实践

完整讨论如何创建说明文件超出了本工作坊的范围。示例项目展示了一种有代表性的做法：

- 在 `copilot-instructions.md` 中记录项目级指南，例如项目说明、结构和全局编码标准。
- 使用 `*.instructions.md` 为文件类型（单元测试、Astro 组件、数据层）或特定任务提供专门说明。
- 使用自然语言，保持说明清楚，并提供代码示例说明推荐和不推荐的写法。

说明文件没有唯一的正确写法，AI 的使用方式也不止一种。通过实践找出适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应建立完善的说明文件集合。查看本项目文件时，你会发现其中包含[用户界面更新][ui-instructions]和 [Astro][astro-instructions]等多种任务的说明。
>
> Copilot 也可以帮助生成说明文件。不同产品界面的入口不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。对应工作坊会在相关步骤中介绍具体入口。
>
> 如需模板或入门示例，请查看包含说明文件、自定义智能体和其他资源的 [awesome-copilot][awesome-copilot] 存储库。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义说明文件

先查看此存储库自带的说明文件：一个核心 `copilot-instructions.md` 和多个用于不同任务的 `*.instructions.md` 文件。可在编辑器或 GitHub 网页界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 查看项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等章节。在 **Code standards** 下查看嵌套的 **GitHub Actions Workflows** 指南。Copilot 在此存储库中的交互都会使用这些说明。
3. 打开 `.github/instructions` 文件夹，查看 Astro 文件、Drizzle 数据层、测试等说明。
4. 打开 `.github/instructions/unit-tests.instructions.md`。查看顶部的 `applyTo` 字段；它设置相对于存储库根目录的 glob，决定说明适用于哪些文件。本项目中，匹配 `**/*.test.ts` 的 TypeScript 测试文件会应用这些说明。
5. 查看此项目的单元测试说明。
6. 打开 `.github/instructions/drizzle.instructions.md` 并滚动到末尾。查看其指向其他说明文件（例如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的说明集拆分成可复用文件，也可以为 Copilot 提供代码示例。这里的路径相对于说明文件所在位置，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 章节记录了项目编码标准，但尚未要求代码内文档。下一步将添加 TSDoc 文档注释和文件头注释规范。

## 添加存储库级标准

本练习只需编辑一次：添加一条项目级规则，要求以 TSDoc 文档注释和文件级注释块记录代码说明。后续练习中，云端智能体会在处理分配给它的议题时读取这条规则。

编辑前先创建分支。云端智能体会读取议题目标分支中的说明；此处也通过单独提交保持更改清晰。

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。添加编码标准可以帮助 Copilot 提供更符合要求的代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到大约位于第 27 行的 **Code formatting requirements** 章节。注意其中记录了项目编码标准，但尚未规定代码内文档，因此此前生成的辅助函数没有文档注释。
3. 在现有标准下方添加以下 Markdown 内容，要求 Copilot 添加文件头注释和 TSDoc 文档注释：

   ```markdown
   - 每个导出的函数都应包含 TSDoc 注释，说明其用途、参数和返回值。
   - 在导入语句或任何代码之前，为文件添加说明其用途的注释块。
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如前一课所述，说明文件可以放在存储库级 `.github/copilot-instructions.md` 中提供全局指导，也可以放在 `*.instructions.md` 文件中，针对特定语言、文件类型或任务提供说明。刚添加的文档注释规则属于项目级标准，因此存储库级文件是合适的位置。

## 提交、推送并合并说明更新

云端智能体会从议题目标分支读取说明。下一课将把议题分配给 Copilot；它会从 `main` 分支创建分支。因此，必须先将说明更改合并到 `main`，云端智能体才能读取。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 到 `main` 的拉取请求并合并。后续练习中，云端智能体处理分配的议题时会读取这些说明。

> [!TIP]
> 如果本工作坊中要直接在 `main` 上操作，可以跳过创建分支并直接提交到 `main`。此处采用分支，是为了模拟真实项目的工作方式。

## 总结与后续步骤

你已了解 Copilot 如何读取本项目的说明文件，并在 `.github/copilot-instructions.md` 中添加了存储库级标准。后续会在云端智能体生成的拉取请求中看到该标准的效果。

接下来，将第一个议题[分配给 Copilot 云端智能体][next-lesson]。

## 资源

- [GitHub Copilot 自定义说明文件][instruction-files]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [编写更有效 Copilot 自定义说明的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot — 说明文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
