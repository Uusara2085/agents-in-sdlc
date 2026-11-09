---
title: "练习 4 - 监视和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前两项练习中，你让 Copilot 云端智能体承担了三个改善用户体验和添加功能的任务。云端智能体虽然异步自主工作，但监视任务进度仍然很重要。

你可以使用多种工具管理分配给云端智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个控制面板中，可以查看所有已创建开放拉取请求（PR）的智能体任务、检查执行情况，也可以引导正在运行的会话。

在本课中，你将：

- 使用智能体页面监视云端智能体任务。
- 引导正在运行的会话，要求添加其他功能。

## 场景

将高对比度模式任务分配给智能体后，团队决定也添加浅色模式。由于智能体已经在更新网站样式并添加模式切换功能，因此可以顺便实现。你将引导智能体，使它同时添加浅色模式和高对比度模式。

## 查看 Copilot 云端智能体任务

先查看分配给 Copilot 云端智能体的所有任务的当前状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。列表应包含分配给 Copilot 的任务，例如：
   - 更新代码文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一项正在运行的任务，检查 Copilot 执行的操作，例如：
   - 从存储库检出代码。
   - 为 Copilot 创建环境。
   - 设置 MCP 服务器。
   - 执行完成任务所需的其他操作。

> [!NOTE]
> 列出的具体步骤会因 Copilot 当前的工作状态和执行方式而异。

4. 同时查看右侧显示的 PR 面板，以监视 PR 和已更改的文件。

## 引导云端智能体

了解当前任务状态后，可以要求 Copilot 在实现高对比度模式时也添加浅色模式。

1. 选择标题与添加高对比度模式相关的会话。确切标题取决于 Copilot 使用的名称和当前工作状态。

   ![智能体控制面板中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 监视会话几分钟，直到设置完成并开始执行任务。出现类似下方的消息时，表示已开始工作。
3. 在 **Steer active session while Copilot is working** 对话框中输入以下提示词：

   ```plaintext
   添加高对比度模式的同时，也添加浅色模式。用户应能通过开关切换浅色模式，并选择所需的显示模式。
   ```

   ![智能体页面中突出显示 Steer active session while Copilot is working 对话框的截图](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示词。
5. 注意 Copilot 会确认收到提示词，并将它纳入工作流程。

## 等待 Copilot 完成

与之前一样，Copilot 会继续处理更新后的任务。它会先完成发送消息时正在执行的步骤，再将新请求加入工作流程。

此过程可能需要几分钟，可以利用这段时间回顾已学内容。

## 总结与后续步骤

本课介绍了 Copilot 智能体页面，这是监视和引导 GitHub Copilot 云端智能体任务的中心位置。你可以跟踪所有进行中和已完成的任务、检查正在执行的工作，也可以重新引导正在运行的任务，调整范围或补充说明。

本课介绍了：

- 使用控制面板和智能体页面监视云端智能体任务。
- 重新引导正在运行的会话，要求添加其他功能。

Copilot 正在完成无障碍功能。接下来，[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
