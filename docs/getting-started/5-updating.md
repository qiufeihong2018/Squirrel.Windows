| [docs](..) / [getting-started](.) / 5-updating.md |
|:---|

# 步骤 5. 更新
 更新过程使用 `Squirrel --releasify`过程生成的更新文件。这包括发布文件以及版本化的完整和增量包。查找分布式更新文件的位置在MyApp代码中提供给 `UpdateManager` (see code in [Integrating: Basic Updating](1-integrating.md)). 

将MyApp更新为新版本是安装MyApp后集成、打包和发布的高潮。这个过程将导致您重新访问打包和分发步骤。

要发布新的更新，您必须首先构建、打包并发布更新后的应用程序。

### 构建

1. **更新 MyApp 版本** - 更新应用的版本。
 
   	**`Properties\AssemblyInfo.cs`**
   
   	~~~cs
  	[assembly: AssemblyVersion("1.0.1")]
	[assembly: AssemblyFileVersion("1.0.1")]
   	~~~
2. **选择 Release** - 选择你构建的配置到 `Release`.
3. **构建 MyApp** -  构建您的应用程序，以确保将最新的更改包含在我们将要创建的包中。
### 包装

使用 [NuGet Package Explorer](https://npe.codeplex.com/) 请填写以下内容
1. **打开以前的NuGet包** - 打开之前为MyApp版本1.0.0创建的NuGet包。
2. **更新版** - 更新元数据中的版本。
4. **取代释放文件** - 下面替换已更改的文件 `lib\net45`.  您可以简单地拖放任何更改过的特定于程序的文件(例如， `MyApp.exe` 文件是示例中惟一更新过的文件)。
5. **保存NuGet包文件为新版本** -使用“另存为…”功能来保存新版本的软件包 `MyApp.1.0.1.nupkg`.

### Releasifying
 使用新的MyApp.1.0.1执行`Squirrel.exe --releasify` 命令去使用新的`MyApp.1.0.1.nupkg` 包。
~~~powershell
PM> Squirrel --releasify MyApp.1.0.1.nupkg
~~~ 

**注意:**
如果你得到一个错误声明`...'Squirrel' is not recognized...` 然后，您可能只需要重新启动Visual Studio，这样包管理器控制台就已经加载了所有的包工具。这种行为已经在VS 2013和2015的社区版上看到。
#### Releasify 输出

 在打包了新的MyApp 1.0.1版本后，`Releases` 目录更新如下:
* **更新设置应用程序** - `Setup.exe`应用程序已经更新，包括最新的MyApp 1.0.1版本包。
* **更新后的文件** - 
 `RELEASES` 文件已被追加，以包含新创建的完整和增量包。
## 发布新版本

`Releases` 目录现在包含要分发给用户的更新文件。
**`Releases` Directory**

![](images/1.5-releases-directory.png)

`RELEASES` 文件包含每个包的SHA1散列、文件名和文件大小。应用程序更新过程利用这些信息。
**`RELEASES` File**

~~~
E3F67244E4166A65310C816221A12685C83F8E6F MyApp-1.0.0-full.nupkg 600725
0D777EA94C612E8BF1EA7379164CAEFBA6E24463 MyApp-1.0.1-delta.nupkg 6030
85F4D657F8424DD437D1B33CC4511EA7AD86B1A7 MyApp-1.0.1-full.nupkg 600752
~~~


## 应用更新

在[Step 1. Integrating](1-integrating.md)中。集成后，我们将MyApp配置为在每次执行MyApp时在后台查找并安装任何更新。在MyApp示例中，指定了文件系统上的`Releases`目录的路径。
### 更新过程概述

`UpdateManager`在每次执行MyApp时执行以下步骤(see [Update Process](../using/update-process.md) for details):
UpdateManager检查发布位置上的发布文件是否有任何更新。
下载所有更新包，并准备执行新的MyApp。
应用的快捷方式被更新，旧版本的MyApp被清理。
### MyApp Example
在提供更新之后，我第一次运行MyApp时，应用程序像正常一样执行。
![](images/1-MyApp.png)

在后台，MyApp已经获得并应用了安装目录中的更新。

![](images/1.5-local-app-data-dir.png)

下一次执行MyApp时，它将是新安装的版本。

![](images/1.5-MyApp.png)

---
| Previous: [4. Installing](4-installing.md) | Return: [Table of Contents](../readme.md)|
|:---|:---|

