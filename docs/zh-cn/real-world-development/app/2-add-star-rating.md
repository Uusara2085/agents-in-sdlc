---
title: "第 2 课 - 添加星级评分：快速上手"
description: "在 GitHub Copilot app 中启动第一个智能体会话，对游戏卡片进行一项小改动，并通过第一个拉取请求合并更改。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

上一课中，你熟悉了工作区并尝试快速聊天。现在启动**智能体会话**，对项目进行第一次更改。这项改动很小：游戏数据中已有星级评分，但主页的游戏卡片还没有显示它。你将让智能体显示评分、审查更改，并通过第一个拉取请求合并更改。

在本课中，你将：

- 启动智能体会话并了解会话结构。
- 让智能体对项目进行一项范围明确的小改动。
- 在工作区差异视图中审查更改。
- 在本地运行应用，并在浏览器中确认更改。
- 创建并合并第一个拉取请求。

## 场景

Tailspin Toys 中的每款游戏都可以有星级评分，游戏详情页已经显示该评分。但主页的游戏卡片只显示标题、类别、发行商和说明。作为热身，你将让智能体在每张卡片上显示现有评分。这项小巧且独立的更改很适合作为第一个会话任务。

## 会话剖析

**会话**是与智能体的对话，在独立工作区中运行。每个会话都有专用的 **git 工作树和分支**，因此可以同时运行多个会话，例如一个添加功能，另一个修复 bug，而不会让更改互相冲突。侧边栏按存储库分组显示会话；选择任一会话即可切换。

会话中有三类内容：与智能体的**对话**、智能体探索和编辑文件时的**工具活动**，以及附带差异的**已更改文件**列表。

## 启动会话并请求更改

现在为项目启动新会话，并请求实现这项功能。在[应用设置][prior-lesson]期间，你已从 GitHub 存储库添加项目。接下来为该存储库创建新会话并提出更改请求。

1. 返回或打开 GitHub Copilot app。
2. 选择侧边栏顶部的 **+**，启动会话。
3. 选择 `tailspin-toys` 存储库。
4. 在提示框下方选择 **new working tree** 和 **Interactive** 模式。使用以下提示请求更改：

    ```plaintext
    在列表页的游戏卡片中显示每款游戏的 starRating（满分为 5 分）。如果评分为 null，则显示 "No rating yet"。保持卡片布局不变，添加测试并运行相关检查。
    ```

5. 按 <kbd>Enter</kbd> 将提示发送给 Copilot。

Copilot app 会先创建新的工作树，也就是项目的隔离副本。然后，它会探索项目，找到需要更新的文件并编写实现。现在，你已使用 Copilot app 添加一项新功能。

## 审查差异

所有人工智能（AI）生成的更改都应在合并前审查，即使是小改动也不例外。现在直接在 Copilot app 中查看更改。

1. 在应用右上角选择 **Toggle review panel**。打开的面板中选择 **Changes**，查看已更改的文件及其差异。

    ![GitHub Copilot app 顶部工具栏，箭头指向 Create PR 右侧的 Toggle review panel 按钮](../../../_images/app-2-review-panel.png)

2. 查看 `GameCard.astro` 中新增的代码，该文件用于显示游戏详情。代码应与以下示例大致相同：有评分时显示评分，`starRating` 为 `null` 时显示“No rating yet”：

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> 与所有生成式 AI 工具一样，Copilot 的输出具有概率性，并非确定性，因此实际代码可能与示例不同，但应大致相似。

## 检查更改

打开浏览器前，先查看智能体自动化检查的结果。确认测试覆盖数值类型的 `starRating` 和 `null` 回退。缺少先决条件或跳过的检查不算通过；批准任何安装请求前，先审查请求内容。

仅阅读代码并不能证明功能正常。现在让 Copilot 启动网站，并在浏览器画布中打开，以便检查更新后的界面。

> [!TIP]
> 画布是 Copilot app 内的交互式小组件。稍后你将探索自定义画布，甚至创建自己的画布；现在先使用内置的浏览器画布。

1. 使用以下提示，让 Copilot 启动应用并在浏览器画布中打开页面：

    ```plaintext
    启动应用，并在浏览器画布中打开。
    ```

2. 稍等片刻，应用将启动，Copilot app 内会打开浏览器窗口。
3. 确认有评分的游戏卡片会显示评分值，满分为 5 分。
4. 完成后，使用以下提示让 Copilot 停止此会话启动的开发服务器并关闭浏览器画布：

    ```plaintext
    停止开发服务器并关闭浏览器画布。
    ```

## 创建并合并第一个拉取请求

功能已完成，现在创建拉取请求（PR），将新代码合并到现有代码库中。

1. 选择右上角的 **Create PR**。
2. 如果系统提示，选择 **Sign in with your browser**，并按照提示完成身份验证。
3. 如果 Copilot 说明存储库策略要求创建 PR 前必须关联议题，请确认它应遵循该流程。
4. 等待 Copilot 创建 PR。
5. 选择聊天上方的 **PR** 气泡，在审查窗格中打开 PR。可在此按需审查拉取请求。
6. 准备好后，选择 **Ready to merge**。
7. 在新对话框中选择 **Merge pull request**，合并拉取请求。

## 总结与后续步骤

你已交付使用 GitHub Copilot app 完成的第一项更改。本课中，你：

- 启动了智能体会话并了解会话结构。
- 让智能体对游戏卡片进行一项范围明确的小改动。
- 在工作区差异视图中审查了更改。
- 在本地运行应用，并在浏览器中确认了星级评分。
- 创建了 PR 1、审查其检查结果并明确合并。

接下来，[从筛选功能议题开始，并使用 Plan 和 Autopilot 模式][next-lesson]构建一项更大的功能。

## 资源

- [在 GitHub Copilot app 中使用智能体会话][agent-sessions]
- [关于 GitHub Copilot app][about-copilot-app]
- [使用 GitHub Copilot app 管理议题和拉取请求][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#安装并配置-github-copilot-app
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
