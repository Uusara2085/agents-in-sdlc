---
title: "第 3 课 - 智能体模式：Plan 和 Autopilot"
description: "先用 Plan 确定方案，再用 Autopilot 根据议题构建筛选功能，最后通过 Interactive 模式检查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

我们已为项目添加一个小功能。较大的更改则需要更完整的流程。GitHub Copilot CLI 可以融入组织现有的开发流程，帮助团队以合适的方式构建正确的功能。本课开始一系列智能体辅助开发练习：根据议题实现功能、确认代码有效并符合预期，最终成功合并。

> [!NOTE]
> 后续功能工作将沿用同一对话和分支。实际项目中通常会为不同类型的文件创建不同分支或 PR；本工作坊采用简化流程，以便聚焦核心概念。

在本课中，你将：

- 根据 GitHub 议题启动新的 Copilot 对话。
- 在 Plan 模式中确定需求。
- 使用 Autopilot 模式实现功能。
- 检查代码。
- 在转发的浏览器中手动验证功能。

后续还会更新存储库说明、自定义现有的 `quality-checks` 技能、添加 MCP 验证、创建 QA 智能体并创建功能 PR。

## 场景

Tailspin Toys 的目录不断扩大，访客需要按类别和发行商筛选游戏。待办议题描述了功能，但组合类别等细节需要在编码前商定。你将使用 Plan 模式确定这些决策，再授权 Autopilot 在明确范围内实现功能。

## 背景

引入 AI 编码智能体不会改变软件开发的基本原则，反而使这些原则更加重要。常见流程如下：

1. 从描述需求的已创建议题开始。
2. 制定实现计划。
3. 编写并审查代码。
4. 运行测试以验证代码。
5. 手动验证新功能。
6. 创建拉取请求（PR）。
7. 代码通过审查且持续集成（CI）成功后，合并代码。

> [!NOTE]
> 具体流程因团队和组织而异，但通常都与上述流程类似。

遵循标准流程，可以确保 AI 生成的代码满足需求，并接受与手写代码相同的审查。

## 对话模式

**对话模式**控制智能体的自主程度。按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 可在模式之间切换：

- **Interactive**：你与智能体协作；智能体提出更改建议，并等待你的输入后再继续。
- **Plan**：智能体先制定计划，但不能编辑项目文件。
- **Autopilot**：智能体自主编写代码、运行测试并反复迭代，直至任务完成。

先使用 Plan 模式审查计划，再使用 Autopilot 实现。

## 从议题开始

开始筛选功能前，返回 Codespace 并确认存储库和终端已准备就绪。

1. 返回 Codespace；如果它已停止，请重新启动。
2. 确认星级评分 PR 已合并。
3. 如果终端未打开，按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
4. 更新 `main`，然后为筛选功能创建分支：

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. 启动 Copilot CLI：

   ```bash
   copilot --yolo
   ```

6. 按两次 <kbd>Tab</kbd> 打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd> 显示所有议题。
8. 使用方向键选中标题为 **Allow users to filter games by category and publisher** 的议题。
9. 按 <kbd>C</kbd> 将议题添加到提示词，并返回 **Session** 选项卡。

提示词现在会以 `#7`（或类似编号）开头。`#` 可将 GitHub 上的议题或拉取请求（PR）加入上下文。

## 规划筛选功能

在实现功能或执行任务前先确定方案，有助于明确预期。对于复杂工作，花时间规划尤其重要。切换到 Plan 模式并要求 Copilot 制定计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到 Plan 模式，确认提示词下方的模式指示器显示 **Plan**。
2. 在上一步添加的议题引用后输入：

   ```plaintext
   为实现此功能制定计划。
   ```

Copilot 会探索项目并确定合适的实现方式。

3. Copilot 可能会询问筛选功能的细节；根据你的偏好作答。
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 查看计划内容。
6. 如果计划与已决定的事项不符，请要求 Copilot 修改。

## 批准 Autopilot

计划确定并审查后，就可以开始实现。

1. 选择 **Accept plan and build on autopilot (recommended)**，或你安装的版本中含义相同的选项。
2. 确认提示词下方的模式指示器显示 **Autopilot**。
3. 查看 Copilot 按计划迭代、生成代码并运行测试。

> [!NOTE]
> 批准计划后，实现可能立即开始，因此务必先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，请先解决设置问题，再将检查视为已完成。

## 审查并验证实现

与其他代码一样，生成的代码在合并前也必须审查。检查代码并运行网站，确认功能正常。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到 Interactive 模式。确认模式指示器不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff`，检查筛选功能实现和测试。
3. 对照议题和规划时做出的决定检查结果。
4. 检查完成后，按 <kbd>Esc</kbd> 退出差异视图。
5. 查看项目检查结果；如有失败，请要求 Copilot 修复。

## 试用新功能

代码看起来没问题后，还需要确认它能够运行。让 Copilot 启动应用，并通过 Codespaces 转发的端口打开网站。

1. 请求 Copilot 启动应用：

   ```plaintext
   启动应用，让我在浏览器中试用筛选功能。告诉我 URL，并让服务器继续运行。
   ```

2. Codespaces 显示端口 `4321` 可用时，选择 **Open in Browser**。
3. 尝试按类别、发行商筛选，以及计划中确定的组合方式。
4. 确认重置和无结果状态符合议题要求及你的决定。
5. 返回 Codespace，请 Copilot 停止它启动的开发服务器。

## 总结与后续步骤

你使用不同的对话模式构建并检查了功能，具体来说：

- 根据 GitHub 议题启动了新的 Copilot 对话。
- 在 Plan 模式中确定了需求。
- 使用 Autopilot 模式实现了功能。
- 检查了代码。
- 在转发的浏览器中手动验证了功能。

接下来，通过[自定义说明][next-lesson]深入了解如何让代码遵循已记录的实践。

## 资源

- [GitHub Copilot CLI 中的 Autopilot][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
