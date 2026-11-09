---
slug: zh-cn/real-world-development/cloud
title: "GitHub Copilot 云端智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot 云端智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** 可在云端异步处理工作。你在 GitHub 上分配任务后，云端智能体会在后台探索存储库、进行更改并创建拉取请求，让你可以继续处理其他事务。

本工作坊将介绍如何添加云端智能体会遵循的自定义说明、分配 GitHub 议题并由它实现工作。你还将使用自定义智能体调整工作方式，在智能体控制面板中监视并引导会话，最后审查它创建的拉取请求并迭代结果。

## 练习

| 练习 | 主题 | 说明 |
|----------|-------|-------------|
| [0. 先决条件][ex0] | 设置 | 创建存储库和 Codespace |
| [1. 自定义说明][ex1] | 上下文 | 添加云端智能体会遵循的自定义说明 |
| [2. 云端智能体][ex2] | 异步智能体 | 将议题分配给 Copilot 云端智能体 |
| [3. 自定义智能体][ex3] | 专业智能体 | 检查并使用自定义智能体 |
| [4. 管理智能体][ex4] | 监视 | 监视并引导智能体会话 |
| [5. 迭代][ex5] | 审查 | 审查拉取请求（PR）、迭代 Copilot 的工作并选择后续步骤 |

## 先决条件

参加本工作坊前，请确保具备以下条件：

- [ ] 拥有已启用 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 计划的 GitHub 帐户
- [ ] 已为帐户或组织启用 Copilot 云端智能体

> [!TIP]
> 没有付费计划？经过验证的学生可通过 [GitHub Education][student-plan] 免费使用 GitHub Copilot。**Copilot Student** 计划包含本工作坊使用的智能体、MCP、代码审查和 Copilot CLI 功能，可用于完成每个开发环境的工作坊。

> [!NOTE]
> 除 Copilot Free 外，Copilot Student、Pro、Pro+、Business 和 Enterprise 均可使用云端智能体。对于 Copilot Business 或 Enterprise，管理员必须为组织启用此功能。

> [!NOTE]
> 本工作坊不介绍模型上下文协议（MCP）。要了解如何在 Copilot 中使用 MCP 服务器，请参阅 [CLI 工作坊][cli]或 [VS Code 工作坊][vscode]。

## 开始

**[从练习 0：先决条件开始][ex0]**

[student-plan]: https://github.com/education/students
[cli]: ../cli/
[vscode]: ../vscode/
[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
