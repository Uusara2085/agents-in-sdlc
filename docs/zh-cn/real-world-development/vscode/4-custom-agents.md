---
title: "练习 4 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的 AI 助手。将智能体定义在存储库的 `.github/agents` Markdown 文件中，可以为 Copilot 提供聚焦的说明、最佳实践、编码模式和领域知识，帮助它更有效地完成特定类型的工作。团队可以将专业知识整理为可复用智能体，例如执行[网页内容无障碍指南（WCAG）][wcag]合规检查的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体可定义在项目的 `.github/agents` 文件夹中，也可全局定义在 `~/.copilot/agents` 中。每个文件都包含 YAML frontmatter，至少要有 `name` 和 `description`，后面是描述智能体行为、专长和指令的 Markdown 提示词。

### 自定义智能体与智能体技能

自定义智能体与[智能体技能][agent-skills-concept]有些相似：两者主要通过 Markdown 文件定义，并会告诉 AI 如何执行任务。可以将**自定义智能体**理解为执行工作的角色，将**技能**理解为它使用的工具。

自定义智能体拥有自己的上下文窗口，并可在工作时协调技能甚至其他智能体。本实验中的无障碍自定义智能体会根据无障碍指南审查和更新网站，也可以调用拉取请求工作流技能或运行和管理测试的技能。

> [!NOTE]
> 自定义智能体没有唯一正确的编写方式。与其他 AI 用法一样，应在自己的环境和场景中测试并迭代。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 致力于让所有用户都能使用众筹平台，不受视力能力或偏好的影响。近期用户反馈指出，当前深色主题的文字与背景颜色对比度不足，难以阅读。设计团队因此要求实现可开关的高对比度模式。

无障碍至关重要，因此你将使用自定义智能体快速生成此功能。

本练习将介绍：

- 检查现有无障碍自定义智能体。
- 在 Copilot Chat 中使用无障碍智能体实现高对比度模式。

## 检查无障碍自定义智能体

项目已包含无障碍自定义智能体。先检查其内容，了解它将如何引导 Copilot。

返回 Codespace，在终端中从 `main` 创建新分支，用于单独保存无障碍功能，与练习 3 中的筛选功能 PR 分开：

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. 打开 `.github/agents/accessibility.md`。
2. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter。

3. 查看后续章节，其中介绍：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript 代码示例。
   - 常见陷阱和错误。

## 在 Copilot Chat 中使用自定义智能体

VS Code 会在 Copilot Chat 视图底部的智能体下拉列表中显示 `.github/agents` 中定义的自定义智能体。选择自定义智能体后，该会话会使用对应智能体的说明和工具。

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始一个干净的对话。模式和模型选择因练习而异；相关步骤会在适用时说明。

1. 如果 Chat 视图的智能体下拉列表中尚未选择 **Agent**，请先选择它。

   ![Chat 视图中的智能体选择器截图](../../../_images/shared-chat-mode-selector.png)

2. 在 Chat 视图底部选择智能体下拉列表；默认活动智能体为 **default**。
3. 从可用智能体列表中选择 **Accessibility agent**。
4. 向无障碍智能体发送以下提示词：

   ```plaintext
   为网站添加高对比度模式。用户应能通过开关启用或关闭高对比度模式，并将设置保存在浏览器的 local storage 中，以便重新加载页面后仍然有效。
   ```

5. Copilot Chat 会探索代码库、提出更改并编辑项目文件。每项编辑都会在聊天中显示文件路径和差异，供你审查。
6. 随着编辑进行，**Files changed** 指示器会更新，显示智能体修改的文件。

> [!NOTE]
> 此过程可能需要几分钟。Copilot 会修改存储库中的真实文件，例如 Astro 组件、CSS 和相关测试。

下一练习会审查并引导这项正在进行的工作。

## 总结与后续步骤

本课介绍了 GitHub Copilot 中的[自定义智能体][custom-agents]，即针对特定任务和领域定制的 AI 助手。使用自定义智能体可以将团队的专业知识和标准整理为可复用的智能体，引导 Copilot 更有效地完成工作。

本课介绍了：

- 自定义智能体的定义方式。
- 如何在 Copilot Chat 智能体模式中使用自定义智能体。

接下来，[监视并引导智能体工作][next-lesson]，在审查更改的同时，要求它在同一会话中添加浅色模式开关。

## 资源

- [关于自定义智能体][custom-agents]
- [在集成开发环境中创建自定义智能体][creating-custom-agents-ide]
- [VS Code 中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [awesome-copilot 中的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright MCP 服务器测试功能][previous-lesson] | [下一课：监视和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
