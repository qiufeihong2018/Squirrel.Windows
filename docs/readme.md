
# 表格内容

该文档为所有Squirrel文档提供了一个目录。

## 文件概述

* **[Squirrel Goals](goals.md)** - Squirrel.Windows 项目的目标概述。
* **[频繁询问的问题 (FAQ)](faq.md)** - 频繁询问的问题列表。
* **[Squirrel.Windows License](../COPYING)** - copyright and license for using Squirrel.Windows

## 开始导引

The **[Getting Started Guide](getting-started/0-overview.md)** 
提供了一个一步一个指导将squirrel集成进简单名叫myapp的windows应用。

1. **[集成](getting-started/1-integrating.md)** - i将Squirrel `UpdateManager` 集成到MyApp中。
1. **[打包](getting-started/2-packaging.md)** - 打包MyApp文件并准备发布。
1. **[分发](getting-started/3-distributing.md)** - 为MyApp提供安装和更新文件。
1. **[安装](getting-started/4-installing.md)** - MyApp的初始安装过程。
1. **[更新](getting-started/5-updating.md)** - 更新MyApp现有安装的过程。

## Using Squirrel


* **Installing** - 与通过Setup.exe(和Setup.msi)初始安装应用程序相关的文档。
  * [Install Process](using/install-process.md) - 安装过程中的步骤概述。
  * [Custom Squirrel Events](using/custom-squirrel-events.md) - 为Squirrel事件预设置自定义操作。
  * [Custom Squirrel Events (non-c# apps)](using/custom-squirrel-events-non-cs.md) - 使一个非c#应用程序能够感知和处理自定义事件的步骤。
  * [Loading GIF](using/loading-gif.md) - 在大型应用程序的初始安装期间指定一个“加载”映像。
  * [GitHub](using/github.md) - 使用GitHub进行安装、发布和更新的概述。
  * [Machine-wide Installs](using/machine-wide-installs.md) - 通过组策略生成适合安装的MSI文件。
  * [Debugging Installs](using/debugging-installs.md) - tips for debugging Squirrel.Windows initial installs.调试Squirrel.Windows的提示，初始安装
* **打包** - 打包应用程序文件和准备发布相关的文档。
  * [命名约定](using/naming.md) - 用于命名的源的概述(例如，快捷名称)。
  * [NuGet 包元数据](using/nuget-package-metadata.md) - 概述NuGet元数据和Squirrel对它的使用。
  * [包装工具](using/packaging-tools.md) - 可以帮助打包应用程序的工具(例如，NuGet、OctoPack、Auto.Squirrel)
  * [Squirrel命令行](using/squirrel-command-line.md) - 命令行选项 `Squirrel --releasify`
  * [Delta包](using/delta-packages.md) - 概述 `Squirrel.exe` 如何创建Delta包。
  * [应用程序签名](using/application-signing.md) - 向`Setup.exe` 和您的应用程序添加代码签名。
* **分发** - 与散布Setup.exe和更新包文件相关的文档。
  * [Microsoft IIS](using/microsoft-iis.md) - 使用Microsoft IIS发布应用程序的概述。
  * [Amazon S3](using/amazon-s3.md) - 使用Amazon S3分发应用程序的概述。
  * [GitHub](using/github.md) - 使用GitHub进行安装、发布和更新的概述。
* **更新** - 与通过`UpdateManager`更新现有安装相关的文档。
  * [更新程序](using/update-process.md) - 更新过程中的步骤概述。
  * [更新管理](using/update-manager.md) - `UpdateManager`的参考指南。
  * [GitHub](using/github.md) - 使用GitHub进行安装、发布和更新的概述。
  * [调试更新](using/debugging-updates.md) - tips for debugging Squirrel.Windows updates.调试提示Squirrel.Windows更新。
  * [分阶段发布](using/staged-rollouts.md) - 如何使用阶段性的发布来逐步增加安装分发


## 参与

为什么不回馈社会，通过对这个项目的贡献让松鼠变得更好呢?

* [贡献](contributing/contributing.md) - 概述您可以更多地参与Squirrel.Windows的方法。
* [建造 Squirrel](contributing/building-squirrel.md) - 为不耐烦的人建造松鼠的步骤。
* [solution.VS解决方案概述](contributing/vs-solution-overview.md) - Squirrel中各种项目的概述。Windows Visual Studio解决方案。
* [分支策略](contributing/branching-strategy.md) - 
概述在squirrel 开发中使用的不同分支。
