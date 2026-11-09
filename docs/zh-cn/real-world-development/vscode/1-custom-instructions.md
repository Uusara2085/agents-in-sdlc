---
title: "练习 1 - 自定义说明（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，或 Copilot 需要了解背景信息，就应确保它能够获取这些上下文。[说明文件][instruction-files]可提供此类代码生成指导。

在本练习中，你将：

- 了解项目上下文、编码指南和文档标准如何通过存储库自定义说明及按路径应用的说明文件传递给 Copilot。
- 使用当前说明生成筛选功能的第一个数据切片（发行商辅助函数）。
- 在 `.github/copilot-instructions.md` 中添加新的存储库级标准。
- 再次发送相同提示词，观察生成的代码如何遵循新标准。
- 提交说明更新和筛选功能切片到 `main`，供下一练习使用。

> [!CAUTION]
> 生成的代码可能不完全遵循你指定的标准。Copilot 的输出具有概率性。本练习的目标是观察更新说明后行为的整体变化，而不是要求输出与示例逐字相同。

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

## 为更改创建分支

先为更改创建分支，以遵循常见的版本控制实践。

1. 返回上一练习中使用的 Codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新说明前使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始一个干净的对话。模式和模型选择因练习而异；相关步骤会在适用时说明。

先使用当前说明文件发送提示词。之后更新说明并重新发送相同提示词，比较结果。

1. 关闭之前练习中打开的编辑器选项卡，避免 Copilot 获取不需要的上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道辅助函数应放在哪里。
3. 在 Chat 视图的智能体下拉列表中选择 **Agent**，使 Copilot 能够修改文件。

   ![Chat 视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示词：

   ```plaintext
   创建或更新 src/lib/publishers.ts，添加数据访问辅助函数，返回所有发行商的名称和 ID。应用文件更改。
   ```

5. Copilot 会探索项目并应用代码更新，通常会同时修改辅助函数文件和测试。
6. 查看建议的辅助函数是否为类型化函数、是否将 `db` 客户端作为第一个参数，以及是否返回类型化发行商数组。这些要求来自适用于 `src/lib/*.ts` 的 `.github/instructions/drizzle.instructions.md` 数据层规范。
7. 注意生成的代码**缺少** TSDoc 文档注释和文件级注释块。

> [!CAUTION]
> Copilot 的输出具有概率性，即使没有要求，它也可能添加文档注释。这种情况也没问题；本练习的重点是观察更新说明后的行为一致性。

## 添加存储库级标准

`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。添加编码标准可以帮助 Copilot 提供更符合要求的代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到大约位于第 27 行的 **Code formatting requirements** 章节。注意其中记录了项目编码标准，但尚未规定代码内文档，因此此前生成的辅助函数没有文档注释。
3. 在现有标准下方添加以下内容，要求 Copilot 添加文件头注释和 TSDoc 文档注释：

   ```markdown
   - 每个导出的函数都应包含 TSDoc 注释，说明其用途、参数和返回值。
   - 在导入语句或任何代码之前，为文件添加说明其用途的注释块。
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 说明文件可以放在存储库级 `.github/copilot-instructions.md` 中提供全局指导，也可以放在 `*.instructions.md` 文件中，针对特定语言、文件类型或任务提供说明。刚添加的文档注释规则属于项目级标准，因此存储库级文件是合适的位置。

## 重新发送提示词并观察变化

重新开始对话并发送相同提示词，以观察新增说明的效果。

1. 返回 Copilot Chat 并选择 **New Chat** 清除当前对话。
2. 再次打开 `src/lib/publishers.ts`，让 Copilot 聚焦于正确的文件。
3. 发送之前的**相同提示词**：

   ```plaintext
   创建或更新 src/lib/publishers.ts，添加数据访问辅助函数，返回所有发行商的名称和 ID。应用文件更改。
   ```

4. 查看建议文件顶部是否有类似以下的注释块：

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 查看建议函数是否包含类似以下的 TSDoc 注释：

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

你已引导 Copilot 遵循新的项目标准，并将其应用到真实代码中；下一练习会在此基础上继续实现功能。

## 提交说明并推送分支

说明文件与存储库中的其他文件一样，使用相同的源代码管理流程。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
2. 运行以下命令，确认说明更新和辅助函数更改已存在：

   ```bash
   git status
   ```

3. 暂存并提交说明更新，以及 Copilot 为辅助函数基础所做的所有更改：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 将分支推送到存储库：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送后，创建拉取请求并关联待办列表中的文档标准议题。Copilot 可以使用项目中已连接的 GitHub 工具查找议题、创建用于关闭议题的 PR 并合并更改。

> [!NOTE]
> 这是第一次让 Copilot 代你在 GitHub 上操作。项目模板已配置 GitHub 工具，无需额外设置。Copilot 首次使用工具时，VS Code 可能会提示你登录 GitHub；按提示授权。后续练习会介绍这种连接所用的模型上下文协议（MCP）。

1. 在 Codespace 中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图，并确认在智能体选择器中选择了 **Agent**。
3. 请求 Copilot 查找与更新说明文件有关的议题，并从当前分支创建 PR，说明其中包含说明更新和新的发行商辅助函数基础：

   ```plaintext
   找到与更新说明文件相关的议题。从当前分支创建拉取请求并关联该议题，同时说明 PR 还添加了后续筛选功能所需的发行商辅助函数基础。
   ```

4. Copilot 会查找议题并创建 PR。
5. 如果 Copilot 提示允许它代表你执行 GitHub 操作，请检查操作内容，并酌情选择 **Allow**。
6. PR 创建后，要求 Copilot 合并 PR 并将本地分支切回 main：

   ```plaintext
   将 PR 合并到 main。然后在本地切回 main 并拉取最新代码，使本地保持同步。
   ```

7. 如果 Copilot 提示允许执行 GitHub 操作和 shell 命令，请检查操作内容，并酌情选择 **Allow**。

现在，你已借助 GitHub Copilot 创建并合并了拉取请求。

## 总结与后续步骤

你已了解 Copilot 如何读取本项目的说明文件，并使用 VS Code 中的 Copilot Chat：

- 发送代码生成提示词，观察 Copilot 如何根据*现有*说明生成代码。
- 在 `.github/copilot-instructions.md` 中添加存储库级标准。
- 再次发送相同提示词，观察建议的代码如何遵循新标准。
- 将说明更新和辅助函数基础提交到 `main`，供下一练习使用。

接下来，在[智能体模式][next-lesson]中运用这些说明，让 Copilot 在整个代码库中添加新功能。

## 资源

- [GitHub Copilot 自定义说明文件][instruction-files]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [编写更有效 Copilot 自定义说明的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义说明][personal-instructions]
- [Awesome Copilot — 说明文件及其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
