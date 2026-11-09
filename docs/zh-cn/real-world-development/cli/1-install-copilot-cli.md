---
title: "第 1 课 - 安装 GitHub Copilot CLI"
description: "在 Codespace 中安装并验证 Copilot CLI，熟悉命令，并找到预置的筛选议题。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] 是在终端运行的智能体式编码助手，可通过命令行探索代码库、生成代码、运行命令并使用外部工具。它可以分担任务、按要求进行更改，让开发者保持专注。首先需要安装工具；可以使用已熟悉的工具完成此操作。

在本课中，你将：

- 使用 npm 安装 GitHub Copilot CLI。
- 使用 GitHub 帐户完成身份验证。
- 信任工作坊存储库并尝试简单对话。
- 使用内置 GitHub MCP 服务器查找筛选议题。

## 场景

团队开始使用 AI 智能体处理不断增长的待办事项。Copilot CLI 将这种能力带入许多开发者日常使用的终端。本课会完成安装和身份验证，为工作坊后续练习做好准备。

## 安装 Copilot CLI

可以通过 [npm][install-cli]、WinGet 或 Homebrew 安装 Copilot CLI。GitHub Codespaces 已预装 Node.js，因此本练习使用 npm。

1. 返回 Codespace 并打开终端。
2. 确认已安装 Node.js，且版本符合要求：

   ```bash
   node --version
   ```

   应显示 24 或更高版本。

3. 全局安装 Copilot CLI：

   ```bash
   npm install -g @github/copilot
   ```

4. 验证安装：

   ```bash
   copilot --version
   ```

   应显示版本号。

## 使用 GitHub 完成身份验证

首次启动时，Copilot CLI 会提示使用 GitHub 帐户完成身份验证。

1. 启动 Copilot CLI：

   ```bash
   copilot
   ```

2. 如果系统提示，请按照设备代码说明进行身份验证并授权 Copilot CLI。
3. Copilot CLI 会显示以下提示：

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. 确认显示的路径是 Tailspin Toys 存储库，然后选择 **Yes, and remember this folder for future sessions**。

> [!NOTE]
> 在 Codespace 中，GitHub 会话可能已完成身份验证。如果 Copilot CLI 启动时没有提示身份验证，就可以继续使用。

## 熟悉工具

普通 shell 提示符下的命令会直接在 Codespace 中运行。启动 Copilot CLI 后，自然语言会发送给智能体，斜杠命令则用于控制对话。

1. 输入 `/model`，使用方向键选择 **Auto**，按 <kbd>Enter</kbd>，再按一次 <kbd>Enter</kbd> 确认。
2. 输入 `/help` 查看当前安装版本提供的命令，然后按 <kbd>Esc</kbd> 关闭帮助界面。
3. 提出一个简单问题，确认一切正常：

   ```plaintext
   这个项目中有哪些关键文件？
   ```

4. 阅读回答，观察 Copilot 如何先探索存储库，再作答。
5. 输入 `/mcp list`，确认内置的 GitHub MCP 服务器可用。
6. 使用以下提示词查找筛选议题：

   ```plaintext
   使用 GitHub MCP，查找此存储库中标题为 "Allow users to filter games by category and publisher." 的议题。提供该议题的 URL 和简短摘要。不要进行任何更改。
   ```

7. 打开 URL 并阅读议题。完成一个快速更改后会再次使用它。

> [!TIP]
> 普通 Copilot CLI 会话使用终端当前检出的分支，不会自动创建工作树。每次更改前都需要创建功能分支。

## 使用工作坊快捷方式

Copilot CLI 通常会在使用超出既有权限的工具前征求批准。为了让工作坊更专注于练习，可以使用 `--yolo` 重新启动 CLI。此经用户批准的快捷方式会在 Codespace 中取消权限提示。

> [!CAUTION]
> `--yolo` 会启用完整的自动权限（`--allow-all-tools`、`--allow-all-paths` 和 `--allow-all-urls`）。只能在 Codespace 或虚拟机等隔离环境中使用，绝不要将它设为日常开发的默认别名。详情请参阅[允许和拒绝工具使用][allow-all-warning]。

本工作坊还会使用 `--enable-all-github-mcp-tools` 启用后续练习所需的 GitHub MCP 读写工具。Codespace 限制了对本地计算机的访问，但仍可访问经过身份验证的 GitHub 资源。发布或合并前，请审查更改。

1. 使用 `/exit` 退出 Copilot CLI。
2. 在存储库根目录重新启动：

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. 再询问一个关于项目的简单问题，确认对话正常，然后使用 `/exit` 退出。

Copilot 会自动保存对话。后续更新说明或添加智能体后，将使用 `copilot --resume` 返回同一功能对话和分支。

## 总结与后续步骤

恭喜！本课中，你：

- 使用 npm 安装了 GitHub Copilot CLI。
- 使用 GitHub 帐户完成了身份验证。
- 信任工作坊存储库并尝试了简单对话。
- 使用内置 GitHub MCP 服务器找到了筛选议题。

接下来，开始[第一个范围明确的更改][next-lesson]，使用 Copilot CLI 在游戏卡片上显示星级评分。

## 资源

- [安装 GitHub Copilot CLI][install-cli]
- [关于 GitHub Copilot CLI][about-copilot-cli]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
