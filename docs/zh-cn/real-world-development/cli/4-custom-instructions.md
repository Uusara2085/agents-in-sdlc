---
title: "第 4 课 - 使用自定义说明引导 Copilot"
description: "查看存储库说明，添加文档标准，并将其应用于筛选功能代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，就应确保 Copilot 能获取相关指导。[说明文件][instruction-files]不仅描述想要什么代码，也能说明代码应如何组织。现在筛选功能已完成，接下来查看 Copilot 使用的说明、添加文档标准并将其应用于代码。

在本课中，你将：

- 了解存储库说明和按路径应用的说明文件如何提供给智能体。
- 更新说明文件，确保遵循编码标准。
- 查看说明文件对代码的影响。

## 场景

Tailspin Toys 有一套开发指南和要求，包括：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TypeScript 文档注释（TSDoc）或 JavaScript 文档注释（JSDoc）说明用途、参数和返回值（如适用，也包括可注入的 `db` 参数）。
- 可复用 Astro 组件应说明其 `Props` 接口，相关代码更改时应同步更新注释。
- 保留现有格式和 lint 指南。

通过说明文件，可以确保 Copilot 了解这些实践要求，并据此执行任务。

## 说明文件

自定义说明可以提供上下文和偏好，帮助 Copilot 了解你的编码风格和要求。你可以指定编码规范、库以及注释风格，也可以为整个存储库或特定文件类型提供说明。

说明文件有两种类型：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送给 Copilot 的单个说明文件。它应包含与大多数请求相关的项目级信息。
- `.github/instructions/*.instructions.md`：针对特定语言、文件类型或任务提供说明。

> [!NOTE]
> 其他说明格式及其支持情况因开发环境而异。依赖某种格式前，请查看[自定义说明支持参考][custom-instructions-support]。

## 查看项目中的自定义说明文件

模板项目已包含一组说明文件。先查看这些文件，再进行更改，以便了解更改的效果。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（不是终端）中打开 `.github/copilot-instructions.md`。
3. 查看简短的项目说明和编码指导。此文件适用于该存储库中与 Copilot 的每次交互。
4. 打开 `.github/instructions` 文件夹并查看其中的文件，包括 Astro、Drizzle 数据层、测试等说明。
5. 打开 `.github/instructions/unit-tests.instructions.md`。查看顶部的 `applyTo` 字段；它设置一个 glob，决定说明应用于哪些文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看它指向其他说明文件和项目现有文件的链接。这样可以将较大的说明集拆分成可复用文件，也可以为 Copilot 提供示例。

## 更新说明文件以符合团队规范

现有文件已包含许多指南，但还缺少一项标准：要求为新生成的 TypeScript 添加 TSDoc 注释。现在修改核心 `copilot-instructions.md`。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 章节（大约位于第 35 行）。
2. 将以下内容添加为该章节的最后一项：

   ```markdown
   - 所有新 TypeScript 代码都应包含 TSDoc 注释。
   ```

文件会自动保存。

## 使用更新后的说明

Copilot CLI 会在对话启动时加载存储库说明。保存更新后，退出并恢复筛选功能对话，让 Copilot 在保留功能上下文的同时加载新说明。

1. 如果筛选功能对话仍在运行，输入 `/exit` 退出。Copilot CLI 会自动保存对话。
2. 在 `game-filters-cli` 分支的存储库根目录中恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果系统提示，请选择筛选功能对话，并确认已检出 `game-filters-cli` 分支。
3. 请求 Copilot 根据更新后的指导修改代码：

   ```plaintext
   我们刚刚更新了说明和代码指导。请更新你生成的代码，使其符合这些要求。
   ```

4. 输入 `/diff` 并查看已更改的 TypeScript 文件。注意新生成的 TSDoc 注释，并确认它们准确描述代码。

## 总结与后续步骤

你已了解 Copilot CLI 如何从说明文件读取上下文，并将新的标准应用于功能代码。具体来说，你：

- 了解了存储库说明和按路径应用的说明文件如何提供给智能体。
- 更新说明文件，要求遵循编码标准。
- 查看了说明文件对代码的影响。

接下来，[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保以一致的方式运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义说明][instruction-files]
- [自定义说明支持情况][custom-instructions-support]
- [创建有效自定义说明的最佳实践][instructions-best-practices]
- [Awesome Copilot — 说明文件及其他资源集合][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
