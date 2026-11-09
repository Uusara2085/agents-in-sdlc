---
title: "第 8 课 - 创建并合并功能拉取请求（PR）"
description: "检查筛选功能、说明、技能更新、质量保证（QA）配置和测试，然后创建 PR 并使用 Agent Merge。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

筛选功能实现、说明更新、技能更新、质量保证（QA）配置和测试都保存在同一个分支中。现在可以一并审查并创建拉取请求（PR）。星级评分 PR 是你手动合并的；这次将使用 **Agent Merge** 管理合并流程。

> [!NOTE]
> 通常会把功能、说明更新、技能更新和 QA 智能体拆分为多个 PR。为简化本工作坊，这些筛选和质量相关工作都保留在同一个对话和分支中，并通过此 PR 提交。

在本课中，你将：

- 了解 Agent Merge 以及它如何自动处理合并流程。
- 检查完整的功能更改和验证证据。
- 创建筛选功能 PR。
- 完成审查后启用 Agent Merge，并确认 PR 已合并。

## 场景

在筛选功能的开发过程中，你使用 Copilot 规划、实现并验证了功能。现在，Tailspin Toys 希望自动处理剩余 PR 工作，同时由开发者掌控合并授权。

## 了解 Agent Merge

**Agent Merge** 会自动处理合并 PR 所需的后续工作。启用后，Copilot 会解决 PR 的阻塞事项，例如修复持续集成（CI）检查失败、回复审查意见，以及在需要时变基；之后，在存储库允许的情况下启用 GitHub 自动合并。

之前你是自行选择 **Merge pull request**。Agent Merge 可以代为处理，但启用前仍须审查工作并确认 PR 已准备就绪。

## 使用 Agent Merge 管理 PR

检查所有代码、更改和验证结果后，创建 PR，再让 Agent Merge 处理其余流程。

1. 返回 Codespace。
2. 输入 `/agent` 打开智能体对话框。
3. 从选项中选择 **Default**，然后按 <kbd>Enter</kbd>。
4. 输入 `/pr create` 创建 PR。
5. 输入 `/pr agentmerge` 启用 Agent Merge。
6. Copilot 会监视 PR 的持续集成流程；检查全部成功后，它会执行合并。
7. 确认 Copilot 显示类似“PR #14 was squash-merged successfully.”的消息。

> [!IMPORTANT]
> Agent Merge 不会绕过必需的审批、分支保护、合并队列、存储库设置或权限限制。如果流程受阻，请阅读报告的原因；在存储库允许的情况下，完成审查后手动合并。

## 总结与后续步骤

你已自动化开发流程中的多个环节，包括生成代码、测试和验证代码，以及处理 PR。具体来说，你：

- 了解了 Agent Merge 及其如何自动处理合并流程。
- 检查了完整的功能更改和验证证据。
- 创建了筛选功能 PR。
- 审查后启用了 Agent Merge，并确认 PR 已合并。

接下来，探索更多用于管理上下文、模型、共享和可选云端委派的 [Copilot CLI 斜杠命令][next-lesson]。

## 资源

- [使用 Copilot CLI 管理拉取请求][manage-prs]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
