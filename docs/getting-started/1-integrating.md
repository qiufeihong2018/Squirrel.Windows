| [docs](..) / [getting-started](.) / 1-integrating.md |
|:---|



# 步骤 1. 集成

第一步是配置MyApp与Squirrel.Windows一起工作。这需要您安装Squirrel。Windows NuGet包到`MyApp.sln`。
## 安装 Squirrel.Windows
这是安装松鼠最简单的方法。在加载MyApp解决方案后，Windows正在使用Visual Studio中的[Package Manager Console](https://docs.NuGet.org/consume/package-manager-console) 。
~~~powershell
PM> Install-Package Squirrel.Windows
~~~

### Squirrel.Windows 的引用

该包将安装许多依赖包以及用于准备发布MyApp的工具。MyApp项目的解决方案资源管理器中的引用现在看起来如下(和Squirrel一样)。1.2.2 Windows版本):
![](images/1.1-post-package-install.png)

**提示:** 或者，您可以使用“管理NuGet包”GUI来安装Squirrel。(在Visual Studio的解决方案资源管理器中右键单击您的项目，并选择“管理NuGet包…”)。
## 基本的更新

对于基本示例，我们将使用来自本地文件系统的MyApp更新，而不是通过web分发文件。有关分发更新文件的其他选项，请参阅[Packaging](2-packaging.md) 。

### 基本的Squirrel.Windows更新代码

下面的代码被添加到MyApp `Program.cs`中，当你使用该应用程序时，它会在后台检查、下载和安装任何新的MyApp版本。

**`Program.cs`**

~~~cs
using Squirrel;
using System.Threading.Tasks;
~~~

**`static async Task Main()`**

~~~cs
using (var mgr = new UpdateManager("C:\\Projects\\MyApp\\Releases"))
{
    await mgr.UpdateApp();
}
~~~


上面的代码演示了在异步任务中使用`UpdateApp()` 方法的最基本的更新机制。它所采取的行动将在[Updating](5-updating.md)一节中进一步讨论。

**注意:** 您为`UpdateManager`提供的路径是发布文件所在目录的路径(默认情况下也命名为 `RELEASES` )，而不是实际的发布`RELEASES`文件。

**提示:** 提示:默认情况下，更新MyApp的文件将与MyApp放在同一个目录中。发布目录下的sln文件 (e.g., `C:\Projects\MyApp\Releases`)。

**Tip:** In this example we simply put the code in the `Program.cs` file. For a production application, place the update code later in start-up process so as to avoid slowing down your program start. 

**提示:** 
如果你尝试通过Visual Studio调试应用程序，你会得到一个 `Update.exe not found, not a Squirrel-installed app?`。可以通过在bin目录中放置一个Update.exe的副本来解决这个问题(see [Debugging Updates: Update.exe not found?](../using/debugging-updates.md) section for details)。
---
| Previous: [Getting Started Guide](0-overview.md) | Next: [2. Packaging](2-packaging.md)|
|:---|:---|
