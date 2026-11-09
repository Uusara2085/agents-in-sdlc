---
title: "第 7 课 - 创建并使用质量保证（QA）智能体"
description: "创建质量保证（QA）自定义智能体，结合议题需求、quality-checks 技能和 Playwright MCP。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，也使用 Playwright 模型上下文协议（MCP）在浏览器中查看筛选功能。现在创建自定义智能体，将这些能力整合到明确的质量保证（QA）流程中。

在本课中，你将：

- 了解自定义智能体如何结合说明、技能和 MCP 工具。
- 创建并检查可重复使用的质量保证配置文件。
- 选择 QA 智能体，根据筛选议题审查其发现。

## 场景

创建拉取请求（PR）前，Tailspin Toys 希望统一检查需求、代码质量、自动化检查、测试覆盖范围和浏览器行为。自定义智能体可以协调 QA 流程并生成可复用报告。

## 什么是自定义智能体？

自定义智能体是通过 Markdown 配置文件定义的 Copilot 专用角色。配置文件说明智能体的目标、指令和可用工具。本练习会在 `.github/agents/qa.agent.md` 中定义 QA 角色，并在 Copilot CLI 中选择它。

不同自定义项各司其职：存储库说明记录团队标准，`quality-checks` 技能封装可重复检查，Playwright MCP 提供浏览器工具，QA 配置文件则指导 Copilot 使用这些能力评估需求并报告发现。配置文件不会取代其他自定义项，也不需要新建对话。

## 创建 QA 配置文件

创建功能 PR 前，让 Copilot 创建可复用的 QA 配置文件，明确 QA 检查内容和工作边界。

1. 返回 Codespace，并确认筛选功能对话处于 Interactive 模式。
2. 请求默认智能体创建自定义智能体：

   ```plaintext
   在 .github/agents/qa.agent.md 中创建名为 QA 的自定义智能体。它应根据议题和已商定的需求检查功能，遵循存储库说明，运行 quality-checks 技能，使用 Playwright MCP 验证行为，并在测试覆盖不足时添加测试。

   对每项需求，报告通过、失败或受阻状态，并提供支持证据。修改实现代码前必须征求我的同意，不得提交更改或创建拉取请求。

   现在只创建配置文件，供我审查。
   ```

## 检查配置文件

使用新智能体前，先确认 Copilot 捕获了预期的 QA 流程和边界，避免配置不完整或权限范围过大。

1. 输入 `/diff` 并打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 为必填项；`name` 可选，但填写后会显示明确的智能体名称。
3. 阅读配置文件说明，确认 QA 会从需求开始、遵循存储库说明、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据、修改实现代码前会征求同意，并且不会提交更改或创建 PR。
5. 如果缺少任何职责或边界，请先要求默认智能体修改配置文件。

## 根据议题运行 QA

Copilot CLI 会在对话启动时加载项目智能体。创建配置文件后，恢复同一个筛选功能对话并选择 QA，以便它使用已有的议题和规划决策。

1. 输入以下命令启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 刚创建的智能体可能不会立即出现在可用智能体列表中，但仍可使用上述命令启用。

2. 输入以下提示词，请 QA 智能体审查功能：

   ```plaintext
   根据议题和计划中确定的事项审查筛选功能。它可以准备好创建 PR 了吗？
   ```

3. 等待 QA 智能体完成检查。
4. 阅读它提供的报告。

## 总结与后续步骤

你已添加可复用的专业角色并审查了它的工作，具体来说：

- 了解了自定义智能体如何结合说明、技能和 MCP 工具。
- 创建并检查了可复用的 QA 配置文件。
- 选择 QA 智能体，并根据筛选议题审查了它的发现。

现在，功能实现、技能更新、QA 配置文件、测试和验证报告都已准备好接受审查。接下来，将它们放入[功能 PR 并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
