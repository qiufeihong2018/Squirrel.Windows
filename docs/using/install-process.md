| [docs](..)  / [using](.) / install-process.md
|:---|

# 安装过程

本节详细介绍安装过程。
## Setup.exe 

`Setup.exe`是一个c++引导程序应用程序，用于在用户的本地系统上安装应用程序。它是生成的 `Squirrel --releasify` 程序.

The `Setup.exe` 文件包括 `Update.exe`应用程序和要安装的MyApp包的最新版本。由于`WriteZipToSetup.exe` 工具将适当的文件注入到exe中，可以提供一个单独的可执行文件。

此外， `Setup.exe` 还将确保用户的计算机上安装了.NET 4.5。
## 安装位置

`Setup.exe`和MyApp中的 `UpdateManager`必须能够向应用程序安装位置写入文件和执行文件。为了确保所有类型用户的权限，选择用户的应用程序数据目录作为安装位置(i.e., `%LocalAppData%\MyApp`).。
安装根目录只需要包含两种类型的文件夹:
* **Packages** - 用于下载和组装更新包文件的文件夹。
* **App Folders** - 给定版本的MyApp的“已安装”应用程序文件。

```
\%LocalAppData%\MyApp
   \packages
      MyApp-1.0.0.nupkg
      MyApp-1.0.1-delta.nupkg
      MyApp-1.0.1.nupkg   
   \app-1.0.0
      MyApp.exe
   \app-1.0.1
      MyApp.exe
```

包目录实际上是不可变的，它只是由我们下载的包组成。使用用户的本地应用程序数据目录意味着我们需要对每个用户的安装目录进行写访问。

**注意:** 
有关确保将应用程序推给企业环境中的所有用户的更多信息，请参阅[Machine-wide Installs](machine-wide-installs.md) 。
## 安装过程概述

The `Setup.exe` 应用程序预设如下:

1. **Ensures .NET Framework Installed** - 确定.NET框架是否可用，如果不可用 `/installfx45`重新启动，下载并启动 .NET 框架安装程序。
1. **Create `%LocalAppData%\MyApp` Directory** - 为要安装的MyApp创建一个目录。
2. **Extracts `Update.exe`** - 将Update.exe应用程序解压缩到应用程序目录 directory (`%LocalAppData%\MyApp`).
3. **Extracts `MyApp.1.0.0-full.nupkg`** - 将MyApp的完整应用程序包解压到  `%LocalAppData%\MyApp\packages\temp` directory.
4. **Executes `Update.exe` to Finish Install** - 使用`/install`开关执行`Update.exe`应用程序，以完成应用程序安装，然后启动应用程序。
    1. **复制MyApp到app-1.0.0目录** - 将完整版本的MyApp文件复制到应用程序子目录(e.g., `MyApp\app-1.0.0`). 
    2. **Launch MyApp** - 在安装过程结束时，更新程序将启动新安装的MyApp版本。
6. **MyApp创建快捷方式** -应用程序的第一次执行将导致在桌面和Windows开始菜单上创建MyApp的快捷方式。

## Desktop & Windows Start Shortcuts

By default, application shortcuts are created on the desktop and the Windows Start menu that point to the `Update.exe` application with additional arguments pointing to the correct application to execute.

**`MyApp.lnk` (Application Shortcut)**

* **Target:** `C:\Users\kbailey\AppData\Local\MyApp\Update.exe --processStart MyApp.exe`
* **Start in:** `C:\Users\kbailey\AppData\Local\MyApp\app-1.0.0`


## See Also

* [Loading GIF](loading-gif.md) - specify a "loading" image during initial install of large applications.
* [Machine-wide Installs](machine-wide-installs.md) - generating an MSI file suitable for installation via Group Policy.
* [NuGet Package Metadata](nuget-package-metadata.md) - overview of the NuGet metadata and its uses by Squirrel.
* [Naming Conventions](naming.md) - A more complete view of how Squirrel names everything.

---
| Return: [Table of Contents](../readme.md) |
|----|

