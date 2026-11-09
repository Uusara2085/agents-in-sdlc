---
title: "练习 2 - GitHub Copilot 云端智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：自定义说明][previous-lesson]

许多组织都面临技术债务，例如尚未解决的安全问题、需要更新的旧代码，或长期积压的功能请求。GitHub Copilot 云端智能体可以自主在后台更新代码和添加功能。工作完成后，它会创建草稿拉取请求，供开发者审查。这样可以将繁琐任务交给智能体，加快开发进度，让开发者专注于更重要的工作。

本课将介绍如何使用 Copilot 云端智能体：

- 自定义代码生成环境。
- 确保操作安全。
- 编写范围明确的议题。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 有一些技术债务需要处理。最初创建网站的承包商没有为代码添加文档。团队希望首先为应用中所有导出的函数添加 TypeScript 文档注释（TSDoc）。

设计团队还准备改善游戏发现体验，希望在每款游戏的详情页显示同一类别中的其他游戏，供用户继续浏览。当前不需要完善的实现，只需要能用于用户体验验收测试的版本。此需求目前被阻塞，但其他议题优先级更高。

这类任务很容易被推迟，适合交给 Copilot 云端智能体异步处理。开发者可以先处理其他工作，之后再回来审查智能体的结果。

## 了解 GitHub Copilot 云端智能体

[GitHub Copilot 云端智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)可以像开发者一样在后台执行任务。可以通过多种方式启动任务，例如[将 GitHub 议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配任务后，Copilot 会创建草稿拉取请求（PR）跟踪进度、设置工作环境并开始处理。任务进行中或完成后，都可以查看 Copilot 会话。解决方案准备好审查时，Copilot 会在 PR 中提及你。

## 明确任务范围的重要性

GitHub Copilot 没有魔法，使用它并不能省去思考。即使看似简单的任务也可能有复杂细节，因此要谨慎确定 Copilot 云端智能体任务的范围，并将它视为 AI 配对程序员：分阶段工作、学习、试验并不断调整。加入生成式 AI 并不会改变软件开发的基本原则。

## 此存储库中的自定义说明

前面的练习介绍了自定义说明及其如何引导 Copilot。如果已完成自定义说明练习，就已了解 `.github/copilot-instructions.md` 的作用；否则，可以先快速查看。分配任务前，以只读方式检查存储库现有的说明文件，之后便能识别它们的影响。

在 GitHub 网页界面或已启动的 Codespace 中打开以下文件：

- `.github/copilot-instructions.md`：查看 **Code standards**，尤其是 TypeScript 规范和 TSDoc 文档注释要求。
- `.github/instructions/unit-tests.instructions.md`：注意 `applyTo` frontmatter，它将说明应用于 `**/*.test.ts` 文件。

下一节将 `Code lacks documentation` 议题分配给云端智能体时，留意生成的 PR 是否遵循 TSDoc 注释、TypeScript 规范和文件头注释要求。这些要求来自上述说明文件；稍后审查 PR 时还会再次查看。

## 为 Copilot 云端智能体设置开发环境

编写代码通常需要特定环境并运行一些设置脚本。将任务分配给 Copilot 时也一样，它会像软件工程师一样处理任务。

云端智能体使用 [GitHub Actions][github-actions] 执行任务。可以在 `.github/workflows/copilot-setup-steps.yml` 中创建[专用设置工作流][setup-workflow]，在 Copilot 开始工作前安装必要的开发工具和依赖项。实验已预先配置此工作流，以确保 Copilot 可以访问 Node.js、项目依赖项、端到端测试所需的浏览器二进制文件，以及单体 Astro 应用所需的迁移并填充数据的 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 允许你在存储库的 "Actions" 选项卡中测试设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 为这些步骤设置所需的最低权限。Copilot 会使用自己的令牌执行操作。
    permissions:
      # 如果要在设置步骤中克隆存储库（例如安装依赖项），需要 `contents: read` 权限。如果未在设置步骤中克隆存储库，Copilot 会在步骤完成后自动克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端/应用设置 - Node.js（整个应用现在使用 Astro + Drizzle/libSQL）
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 迁移并填充本地 SQLite 数据库，以便构建和测试时有可用数据。
      - name: Set up the database
        run: npm run db:setup
```

此文件与其他 GitHub 工作流类似，但有几个关键点：

- 它包含名为 `copilot-setup-steps` 的单个作业。Copilot 开始处理 PR 前，GitHub Actions 会运行此作业。
- `workflow_dispatch` 触发器允许你在存储库的 **Actions** 选项卡中手动运行工作流。这有助于验证工作流，而不必等待 Copilot 启动它。

## 添加代码文档

虽然每个人都知道文档很重要，但许多项目中的信息已经过时或完全缺失。这类技术债务常常无人处理，会拖慢开发效率，增加维护代码库或引入新团队成员的难度。Copilot 擅长生成文档，因此适合将此议题分配给云端智能体。它会在后台生成文档，后续练习会审查结果。

1. 在新的浏览器选项卡中打开 GitHub.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 创建空白议题。
5. 将 **Title** 设为 `Code lacks documentation`。
6. 将 **Description** 设为：

   ```plaintext
   我们组织要求在有助于解释行为时，为函数和方法添加 TSDoc 文档注释。不幸的是，近期更新没有遵循此标准。我们需要更新现有代码，在文档注释有助于说明行为的地方添加注释。
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。
10. 选择 **Pull Requests** 选项卡。
11. 打开新建的 PR，标题可能类似 `[WIP]: Code lacks documentation`。如果列表中尚未出现新 PR，请稍等片刻并刷新浏览器。
12. 几分钟后，Copilot 应会创建待办列表。

> [!NOTE]
> Copilot 可能需要几分钟才会在 PR 中显示待办列表。它需要先创建环境（运行前面介绍的工作流）、分析项目并确定处理任务的方案。

13. 查看 Copilot 将执行的任务列表。
14. 向下滚动 PR 时间线，查看 Copilot 已开始处理议题的更新。
15. 选择 **View session**。

   ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新窗口才能看到更新后的状态。

16. 浏览实时会话，观察 Copilot 如何探索代码并了解当前状态、暂停思考并制定方案，以及生成代码。

此过程可能需要几分钟。云端智能体的主要优势之一是异步执行任务，让你可以处理其他工作。接下来将另一个任务分配给 Copilot，然后转而为应用编写功能代码。

## 为游戏详情页添加相关游戏

GitHub Copilot 云端智能体的一大优势是可以拆分工作：你专注于一组任务，智能体同时处理另一组。即使为设计团队添加相关游戏功能不需要很长时间，仍可利用这段时间处理其他工作。现在将此任务分配给 Copilot 云端智能体。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 使用空白模板。
5. 将 **Title** 设为 `Show related games on the game details page`。
6. 将 **Description** 设为：

   ```markdown
   我们希望在每款游戏的详情页上显示相关游戏，帮助用户发现更多游戏。设计团队希望探索用户体验并进行验收测试。需求如下：

   - 在 `src/lib/` 中添加数据访问辅助函数，返回给定游戏所在类别的其他游戏，但不包括该游戏本身。
   - 在游戏详情页显示“Related games”区域，并使用该辅助函数。
   - 处理游戏没有相关游戏的情况。
   - 为新辅助函数创建单元测试。
   - 创建 PR 前确保所有测试通过。
   ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将 Copilot 分配给议题](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

过一会儿，议题的第一条评论旁应出现 👀，表示 Copilot 已开始处理任务。

![Copilot 使用眼睛表情符号表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在处理第二项请求。它会像软件工程师一样工作，因此无需持续监视；任务完成后再审查即可。现在可以转而创建和使用自定义智能体。

## 总结与后续步骤

本课介绍了 [GitHub Copilot 云端智能体][copilot-agents]。可以将议题分配给 Copilot，让它异步处理技术债务、创建新功能，或协助将代码迁移到其他框架。

本课介绍了：

- 自定义代码生成环境。
- 确保操作安全。
- 明确议题范围的重要性。
- 将议题分配给 Copilot。

云端智能体正在后台工作，现在可以开始创建和使用自定义智能体。云端智能体也可以使用[模型上下文协议（MCP）服务器][cloud-agent-mcp]，并可读取前面练习中配置的自定义说明。

## 资源

- [关于 Copilot 云端智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云端智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
