---
title: "练习 3 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的 AI 助手。将智能体定义在存储库的 `.github/agents` Markdown 文件中，可以为 Copilot 提供聚焦的说明、最佳实践、编码模式和领域知识，帮助它更有效地完成特定类型的工作。团队可以将专业知识整理为可复用智能体，例如执行 [WCAG][wcag] 合规检查的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体可定义在项目的 `.github/agents` 文件夹中，也可全局定义在 `~/.copilot/agents` 中。每个文件都包含 YAML frontmatter，至少要有 `name` 和 `description`，后面是描述智能体行为、专长和指令的 Markdown 提示词。

### 自定义智能体与智能体技能

自定义智能体与[智能体技能][agent-skills-concept]有些相似：两者主要通过 Markdown 文件定义，并会告诉 AI 如何执行任务。可以将**自定义智能体**理解为执行工作的角色，将**技能**理解为它使用的工具。

自定义智能体拥有自己的上下文窗口，并可在工作时协调技能甚至其他智能体。本实验中的无障碍自定义智能体会根据无障碍指南审查和更新网站，也可以调用拉取请求工作流技能或运行和管理测试的技能。

> [!NOTE]
> 自定义智能体没有唯一正确的编写方式。与其他 AI 用法一样，应在自己的环境和场景中测试并迭代。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

本练习将介绍：

- 自定义智能体的定义方式。
- 如何将任务分配给自定义智能体。

## 场景

Tailspin Toys 希望众筹平台能满足所有用户的需求，不受视力能力或偏好的影响。近期用户反馈指出，当前深色主题的文字与背景颜色对比度不足，难以阅读。设计团队因此要求实现可开关的高对比度模式。

无障碍至关重要，因此你将使用自定义智能体快速生成此功能。

## 检查无障碍自定义智能体

项目已包含无障碍自定义智能体。先检查其内容，了解它将如何引导 Copilot。

返回 Codespace，然后查看无障碍自定义智能体文件：

1. 打开 `.github/agents/accessibility.md`。
2. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter。

3. 查看后续章节，其中介绍：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - HTML、CSS 和 JavaScript 代码示例。
   - 常见陷阱和错误。

## 创建并分配议题

智能体页面是集中管理环境中所有智能体的位置。你可以在此向 Copilot 云端智能体分配任务、监视任务进度，以及重新引导正在运行的会话。现在将创建高对比度模式任务并分配给 Copilot。

1. 打开你的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建空白议题。
5. 在 **Title** 中输入 `Add high contrast mode to website`。
6. 在 **Description** 中输入：

   ```plaintext
   我们需要为网站添加高对比度模式。用户应能通过开关启用或关闭高对比度模式。此设置应保存在浏览器的 local storage 中。
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。
9. 从自定义智能体列表中选择 **Accessibility agent**。

   ![Copilot 云端智能体分配界面中突出显示自定义智能体和 Accessibility 的截图](../../../_images/ex5-select-custom-agent.png)

10. 选择 **Assign**。
11. Copilot 将在后台开始处理任务。

## 总结与后续步骤

本课介绍了 GitHub Copilot 中的[自定义智能体][custom-agents]，即针对特定任务和领域定制的 AI 助手。使用自定义智能体可以将团队的专业知识和标准整理为可复用的智能体，引导 Copilot 更有效地完成工作。

本课介绍了：

- 自定义智能体的定义方式。
- 如何分配任务。

Copilot 正在后台实现高对比度模式。接下来，在智能体控制面板中[监视并引导会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [在组织中使用自定义智能体的准备工作][org-custom-agents]
- [在企业中使用自定义智能体的准备工作][enterprise-custom-agents]

---

| [← 上一课：GitHub Copilot 云端智能体][previous-lesson] | [下一课：监视和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
