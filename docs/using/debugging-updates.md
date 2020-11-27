| [docs](..)  / [using](.) / debugging-updates.md
|:---|

# 调试更新
以下提示将帮助您调试应用程序中的更新过程。
## Update.exe not found?

从Visual Studio执行MyApp会执行更新过程，你会从`UpdateManager`中得到以下异常:
~~~
Update.exe not found, not a Squirrel-installed app?
~~~


 `UpdateManager`
期望找到安装在EXE上一个目录下的`Update.exe` 应用程序(例如，默认Visual Studio项目的\bin目录)。

要解决这个问题，您可以简单地放置一个名为Update.exe的文件，或者您可以从 `MyApp\packages\squirrel.windows.1.2.2.tools`中复制`Squirrel.exe` 。工具目录，并将其重命名为Update.exe(这是实际的Update.exe包在Setup.exe内)。

从Visual Studio执行MyApp将导致它完成更新过程，你的\bin目录将类似于`%LocalAppData\MyApp%`安装目录:
![](images/debugging-update-dir.png)

**Tip:** If you want to ensure that the Update.exe is always available in your output directory, you can add the Update.exe file to the Visual Studio project and set its Properties > Copy To Output Directory to 'Copy if newer'. 

## Catching Update Exceptions

You can catch thrown exceptions and log the results. 

~~~cs
using (var mgr = new UpdateManager("C:\\Projects\\MyApp\\Releases"))
{
    await mgr.UpdateApp();
}
~~~

Alternatively, set up Splat Logging, see [here](https://github.com/Squirrel/Squirrel.Windows.Next/blob/6d7ae23602a3d9a7636265403d42c1090260e6dc/src/Update/Program.cs#L53) for an example.


---
| Return: [Table of Contents](../readme.md) |
|----|
