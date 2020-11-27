| [docs](..) / [getting-started](.) / 2-packaging.md |
|:---|

# 步骤 2. 打包

打包是构建、打包和准备发布MyApp发布包的过程。

## 构建

准备分发应用程序的第一步是构建应用程序。

1. **设置 MyApp 版本** - 设置初始应用程序版本。

   	**`Properties\AssemblyInfo.cs`**
   
   	~~~cs
  	[assembly: AssemblyVersion("1.0.0")]
	[assembly: AssemblyFileVersion("1.0.0")]
   	~~~
2. **选择 Release** - 选择你构建的配置到 `Release`.
3. **构建 MyApp** - 构建您的应用程序，以确保将最新的更改包含在我们将要创建的包中。

## 包装

Squirrel使用 [NuGet](https://www.NuGet.org/) 用于将应用程序文件和各种应用程序属性(例如，应用程序名称、版本、描述)捆绑在一个发布包中。

[NuGet Package Metadata](../using/nuget-package-metadata.md)部分提供了关于使用NuGet和`.nuspec` 文件自动打包应用程序的额外细节。我们将使用[NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)手动创建一个NuGet包。
1. **创建一个新的NuGet包** - 第一步是创建一个新的NuGet包。
2. **编辑元数据** - 更新包元数据为MyApp。
   * **Id** - 应用程序名称(无空格)
   * **版本** - 在`Properties\Assembly.cs`中指定的版本
   * **依赖** - Squirrel不期望包中有任何依赖项(应该显式地将所有文件添加到包中)
3. **Add lib & net45** - 文件夹和`net45`文件夹添加到项目中。无论您的应用程序是否是`net45`应用程序，Squirrel都期望提供一个`lib / net45`目录。
4. **添加发布文件** - 添加MyApp执行`bin\Release` 所需的所有文件(包括Squirrel所需的各种文件)。
   * **包括MyApp文件:**  MyApp.exe。任何MyApp.exe需要的非标准.net dll。
   * **包括Squirrel文件** Squirrel.dll, Splat.dll, NuGet.Squirrel.dll, Mono.Cecil.\*, DeltaCompressionDotNet.\*, ICSharpCode.SharpZipLib.\*
   * **不包括:** *.vshost.\*, *.pdb files 
5. **保存NuGet包文件** - 
 保存NuGet包文件到你以后可以轻松访问的地方(例如，`MyApp.sln` 目录)。遵循给定的命名格式(例如 `MyApp.1.0.0.nupkg`)。
![](images/1.2-nuget-package-explorer.png)

## Releasifying


发布是准备`MyApp.1.0.0.nupkg`的过程。nupkg分布。
### 使用 Releasify

You use the `Squirrel.exe` tool that was included in the Squirrel.Windows package you installed in the `MyApp.sln` previously. 
您可以使用松鼠中包含的Squirrel.exe工具。你安装在 `MyApp.sln` 之前。
Use the [Package Manager Console](https://docs.NuGet.org/consume/package-manager-console) to execute `Squirrel.exe --releasify` command.

~~~powershell
PM> Squirrel --releasify MyApp.1.0.0.nupkg
~~~ 

**提示:** 
如果您得到一个错误声`...'Squirrel' is not recognized...` …然后，您可能只需要重新启动Visual Studio，这样`Package Manager Console` 就已经加载了所有的包工具。
### Releasify 输出

The `Squirrel --releasify` 命令完成以下操作:

* **创建发布目录** - 创建一个发布目录(在MyApp中，默认的 `MyApp.sln`)。
* **创建Setup.exe** - 创建一个Setup.exe文件，其中包含要安装的应用程序的最新版本。
* **创建 `RELEASES` 文件** - 创建一个文件，提供更新过程中MyApp将使用的所有发布文件的列表
* **创建 `MyApp.1.0.0-full.nupkg`** -将您创建的包复制到`release`目录。
* **创建 `MyApp.*.*.*-delta.nupkg`** - i如果您正在发布一个更新，releasify会创建一个增量文件包来减小更新包的大小(请参阅 [Updating](5-updating.md) 以获得详细信息)。

**`C:\Projects\MyApp\Releases`**

![](images/1.2-releases-directory.png)

## See Also

* [Visual Studio Build Packaging](../using/visual-studio-packaging.md) 包——将NuGet打包集成到您的Visual Studio构建过程中，包括打包和发布。

---
| Previous: [1. Integrating](1-integrating.md) | Next: [3. Distributing](3-distributing.md)|
|:---|:---|
