---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 Copilot 云端智能体练习前，需要先做好准备。你将创建 Tailspin Toys 存储库的副本并启动一个 [Codespace][codespaces]，用它编辑说明文件并审查云端智能体生成的工作。

## 设置实验存储库

从[模板存储库][template-repository]创建副本，作为练习项目。新存储库包含实验所需文件。

1. 在新的浏览器窗口中打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面中选择 **Use this template**，然后选择 **Create a new repository**。

   ![Use this template 按钮](../../../_images/ex0-use-template.png)

3. 如果你参加由 GitHub 或 Microsoft 举办的活动，请遵循导师提供的说明。否则，请在你有权使用 GitHub Copilot 的组织中创建存储库。

   ![输入存储库模板设置](../../../_images/ex0-repository-settings.png)

4. 记下新建存储库的路径（**organization-or-user-name/repository-name**），稍后会用到。

## 创建 Codespace

接下来，使用 Codespace 完成本实验。

[GitHub Codespaces][codespaces] 是基于云的开发环境，可在浏览器中编写、运行和调试代码。它提供功能完整的集成开发环境，支持多种编程语言、扩展和工具。

1. 打开刚创建的存储库。
2. 选择绿色的 **Code** 按钮。

   ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，再选择 **+** 按钮创建 Codespace。

   ![创建 Codespace](../../../_images/ex0-create-codespace.png)

Codespace 创建需要几分钟，但仍比手动安装所有服务快得多。等待期间，可以了解 GitHub Copilot 的其他功能。

> [!CAUTION]
> 后续练习会再次使用此 Codespace。现在先在浏览器选项卡中保持它打开。

> [!NOTE]
> 本工作坊可在 Codespace 或本地[开发容器][dev-containers]中运行，两者都会安装顺利完成工作坊所需的先决条件。如果要在本地运行，请在 VS Code 中打开克隆的存储库；出现提示时选择 **Reopen in Container**。VS Code 将构建与 Codespace 相同的开发容器。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 总结

恭喜，你已创建实验存储库副本并开始创建 Codespace。后续练习会使用该环境与你一起完成云端智能体工作流。

## 下一步

接下来，添加云端智能体会遵循的自定义说明。继续阅读[练习 1：自定义说明][next-lesson]。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [开始使用 Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
