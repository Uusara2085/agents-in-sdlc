---
title: "第 6 课 - 使用 Playwright MCP 验证功能"
description: "检查或配置 Copilot CLI 中的 Playwright MCP，并在浏览器中试用筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

编写代码只是开发工作的一部分。模型上下文协议（MCP）服务器可以让 Copilot CLI 使用内置功能之外的工具和服务。

在本课中，你将：

- 了解模型上下文协议（MCP）以及 Copilot CLI 如何使用它。
- 在 Playwright MCP 尚不可用时添加它。
- 让智能体控制浏览器并试用筛选功能。

## 场景

单元测试和端到端测试很重要，但验证界面更新还需要实际与界面交互。借助 Playwright MCP，Copilot 可以像用户一样操作网站，进一步自动验证更改。

## 什么是模型上下文协议（MCP）？

[模型上下文协议（MCP）][mcp-blog-post] 为 AI 智能体与外部工具和服务通信提供了方式。MCP 服务器充当智能体与外部工具、服务之间的桥梁，每个服务器都会提供一组可用的工具和资源。

常见的 MCP 服务器包括：

- **[GitHub MCP Server][github-mcp]**：提供管理 GitHub 存储库、议题和拉取请求的 API。
- **[Playwright MCP Server][playwright-mcp-server]**：提供基于 Playwright 的浏览器自动化功能。

GitHub 维护 [MCP 注册表][mcp-registry]，帮助开发者发现并参与生态系统。

> [!CAUTION]
> 请像对待项目中的其他依赖项一样对待 MCP 服务器。使用前先检查源代码、验证发布者并评估安全影响。

## 添加 Playwright MCP 服务器

如果 Copilot CLI 尚未配置 Playwright MCP 服务器，请添加它，以便 Copilot 像用户一样操作网站。

> [!NOTE]
> 如果 Copilot CLI 已配置 Playwright MCP，请跳过设置步骤并继续下一节。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令，打开添加 MCP 服务器对话框：

   ```plaintext
   /mcp add
   ```

3. 名称输入 `playwright`，然后按 <kbd>Tab</kbd>。
4. 确认服务器类型为 **STDIO**，按 <kbd>Enter</kbd>，然后按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中输入：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>S</kbd>（Windows/Linux）保存 MCP 服务器。
7. 按 <kbd>Esc</kbd> 退出 MCP 对话框。

## 让 Copilot 使用 Playwright 试用功能

之前你已手动确认功能是否正常。现在让 Copilot 使用 Playwright MCP 完成同样的检查。

1. 输入以下提示词，要求 Copilot 使用 Playwright MCP 验证功能：

   ```plaintext
   启动应用，并使用 Playwright MCP 根据议题和我们的计划检查筛选功能。告诉我哪些正常、哪些不正常，不要修改任何内容。完成后停止你启动的服务器。
   ```

> [!NOTE]
> 无需特意指定 Copilot 使用 MCP 服务器；它通常会根据当前上下文自行选择。不过，明确指出应该使用的服务器有助于获得更一致的结果，也能节省一些令牌。

2. 查看 Copilot 在浏览器中执行的操作步骤。
3. 阅读报告并确认功能表现符合预期。

Copilot 会启动服务器、使用 Playwright 操作网站、停止服务器并提供报告。

## 总结与后续步骤

你已从 Copilot CLI 使用 Playwright MCP 在真实浏览器中试用功能，具体来说：

- 了解了 MCP 及 Copilot CLI 如何使用它。
- 在 Playwright MCP 尚不可用时添加了服务器。
- 让智能体控制浏览器并试用了筛选功能。

接下来，创建一个[质量保证（QA）自定义智能体][next-lesson]，整合技能和浏览器工具。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [向 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
