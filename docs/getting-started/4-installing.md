| [docs](..) / [getting-started](.) / 4-installing.md |
|:---|
# 步骤 4. 安装

安装MyApp的过程和执行 `Setup.exe` 应用程序一样简单。`Setup.exe` 是由 `Squirrel --releasify` 进程生成的，位于`Releases` 目录中。
## Setup.exe

`Setup.exe` 是一个c++引导程序，用于在用户的本地系统上安装MyApp。它包含了嵌入在exe文件中的最新完整版本的MyApp包文件 (see [Install Process](../using/install-process.md) for details).

## 安装过程概述

The `Setup.exe` 应用程序执行以下操作 (see [Install Process](../using/install-process.md) for details):

* 为要安装的MyApp创建一个`%LocalAppData%\MyApp` 要安装的MyApp的目录。.
* directory.提取并准备 `app-1.0.0`目录下的MyApp文件。
* 在安装过程结束时启动`app-1.0.0\MyApp.exe` 。
### 安装文件结构

在初始化之后，MyApp的安装如下所示

#### `%LocalAppData%\MyApp` Directory

![](images/1.3-local-app-data-dir.png)


---
| Previous: [3. Distributing](3-distributing.md) | Next: [5. Updating](5-updating.md)|
|:---|:---|

