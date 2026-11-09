---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是简单的应用更新，通常也需要修改多个文件并运行测试。开发者需要找到相关文件、进行更改、运行测试、调试、发现遗漏并再次修改。Copilot 智能体模式可以帮助处理这些步骤。

Copilot 智能体模式可在集成开发环境中自主探索项目结构、进行所需更改、运行测试，并自动修复发现的问题。现在使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和云端智能体虽然名称相似，但适用于不同的工作方式。智能体模式在集成开发环境中执行任务，适合快速反馈和交互。云端智能体则像团队中的配对程序员，通过议题和拉取请求异步协作。

在本练习中，你将了解如何：

- 使用 Copilot 智能体模式探索项目、查找相关文件并协同修改。
- 使用 GitHub Copilot 智能体模式跨用户界面（UI）和数据层实现功能。
- 在合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

## 场景

游戏列表不断增长，你希望用户能够按类别和发行商筛选。上一练习已添加发行商辅助函数；现在使用 Copilot 智能体模式完成剩余的数据层、界面和测试工作。

## 运行 Tailspin Toys 网站

先查看网站当前功能，再进行修改。

Tailspin Toys 是一个面向开发者的桌游众筹平台，可列出游戏并显示游戏详情。该网站是一个 Astro 应用，会在构建时将页面渲染为静态 HTML。页面在 frontmatter 中通过 Drizzle ORM 直接查询本地 SQLite 数据库，没有单独的后端 API 或客户端界面框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能通过使用标准 DOM API 的精简 Astro `<script>` 实现。

### 启动网站

项目提供 `npm run dev` 命令，用于启动单个 Astro 开发服务器。通过以下步骤在 GitHub Codespace 中运行网站：

1. 返回 Codespace。上一练习结束后，你应已切回 `main`。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
3. 更新 `main` 并为筛选功能创建分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，应显示类似以下内容的横幅：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出对话框，询问是否打开 `http://localhost:4321` 的浏览器窗口，请选择 **x** 将其关闭。

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），同时选择终端中的 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中选择终端显示的 localhost 链接时，会自动重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是指向当前 Codespace 的专用隧道，网站服务器正在其中运行。

### 浏览网站

网站启动后，可以浏览其现有功能：

- **主页**：显示桌游列表、标题、图片和描述。
- **游戏详情页**：选择游戏后会打开详情页，其中包含标题、描述、发行商和类别等信息。

## 使用 Copilot 查看待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始一个干净的对话。模式和模型选择因练习而异；相关步骤会在适用时说明。

网站初始版本可以正常运行，但还需要添加新功能。项目模板已自动创建议题待办列表。让 GitHub Copilot 查看这些议题。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。**Agent** 智能体可自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![Chat 视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本工作坊作者并非推荐某个模型。编写本工作坊时使用了 Claude Sonnet 4.5，因此将它写入说明，希望代码建议相对一致，提供良好体验。不过，由于大语言模型（LLM）的输出具有概率性，你看到的建议可能与示例不同，这是正常且预期的情况。

> [!NOTE]
> Copilot 可能会使用不同的模型上下文协议（MCP）命令，但仍应能完成任务。

3. 向 Copilot 发送以下提示词，询问待办议题：

   ```plaintext
   请显示 GitHub 存储库中的待办事项，并帮助我按对用户最有用的程度确定优先级。
   ```

4. 选择 **Continue** 以运行列出所有议题的命令。
5. 查看生成的议题列表。

Copilot 还会根据它对用户价值的判断对议题排序。

## 查看说明文件

让智能体生成代码前，先查看用于提供项目上下文的说明文件。本练习将使用[用户界面（UI）][ui-instructions]文件，其中说明了如何为网站添加功能。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看整体指导，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - Astro、Tailwind CSS 和 Drizzle 等文件类型的专用说明链接。

> [!TIP]
> 说明文件可以链接到其他说明文件和项目文件。链接路径相对于说明文件所在位置。这样可以复用说明、拆分较复杂的规则，并为 Copilot 提供示例和模板。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md

## 实现筛选功能

完成筛选至少需要对应用进行三项更改：

- 在数据层 (`src/lib/`) 添加或完善剩余筛选逻辑。
- 添加或更新筛选行为测试。
- 更新游戏列表页，添加筛选界面。

合并前还需要运行并通过测试。Copilot 智能体模式可以协助完成这些任务。

1. 继续当前 Copilot 对话，或选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions**，再选择 `ui` 说明文件。

   ![选择 UI 说明文件的示例截图](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选择 **Agent**。

   ![Chat 视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示词，根据待办议题要求 Copilot 实现功能：

   ```plaintext
   请根据待办列表中相关 GitHub 议题的要求，更新网站以支持按发行商和类别筛选。上一练习已经添加发行商辅助函数；完成剩余的数据层、界面和测试工作时，请保留并按需完善该工作。完成前确保所有测试通过。服务器已经在运行，无需重新启动。
   ```

6. 查看 Copilot 如何探索项目并查找相关文件，包括数据层辅助函数、界面和测试。随后它会修改文件并运行测试。

   ![Copilot 正在探索项目文件的截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会探索项目、修改文件并运行测试。根据任务和代码库的复杂程度，这可能需要几分钟。工作期间，编辑器中可能会显示 **Keep** 和 **Undo** 按钮。Copilot 完成后，所有更改都会显示相应的 **Keep** 或 **Undo** 按钮；无需在工作进行中选择。

7. Copilot 提示运行测试时，选择 **Continue**。

   ![Copilot Chat 提示用户确认运行测试的对话框截图](../../../_images/ex3-agent-mode-run-tests.png)

8. 处理中可能会暂停，甚至出现测试失败。这没有问题；Copilot 会在生成代码和运行测试之间反复迭代，直至任务完成且未检测到错误。

   ![已完成的 Copilot 智能体模式 Chat 会话截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，查找潜在问题。

> [!CAUTION]
> 务必审查 Copilot 或其他 AI 工具生成的代码。

10. 返回正在运行网站的浏览器，试用新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结与后续步骤

本练习介绍了如何使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加功能。你了解了如何：

- 使用 GitHub Copilot 智能体模式跨界面和数据层实现功能。
- 使用 Copilot 智能体模式探索项目、查找相关文件并协同修改。
- 在合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

接下来，使用 [Playwright MCP 服务器测试功能][next-lesson]，并创建功能拉取请求。

### 附加探索练习 — 实现分页

随着游戏列表不断增长，网站将需要分页功能。使用本练习中掌握的技能，提示 Copilot 为网站添加分页。编写提示词时可以考虑：

- 遵循现有最佳实践，包括使用已有说明文件。
- 确定分页方式，例如是否允许用户选择页面大小，还是使用固定页面大小。
- 在提示词中提供足够指导，确保 Copilot 按预期实现功能。
- 通过迭代向 GitHub Copilot 提供上下文并要求修改。这是正常的协作流程。

## 资源

- [Copilot ask、edit 和 agent 模式：功能及适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
