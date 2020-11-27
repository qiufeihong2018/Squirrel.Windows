| [docs](.) / faq.md |
|:---|

# 常见问题(FAQ)
Squirrel.Windows常见问题。按下面的区域组织。
## 整合

1. **Squirrel.Windows 可以用在非.Net的应用程序上吗?**  
  是的，您可以按照入门指南中描述的方式打包非c#应用程序。有关其他自定义，请参见 [为非c#应用程序定制squirrel事件](using/custom-squirrel-events-non-cs.md).  
1. **如何将ClickOnce应用迁移到Squirrel?**  
  您可能需要查[ClickOnceToSquirrelMigrator](https://github.com/flagbug/ClickOnceToSquirrelMigrator)迁移助手。
1. **我如何确定我的应用程序是一个Squirrel应用程序?我提供了一个squirrel and non-squirrel安装版本，想知道哪个正在运行。**  
您可以检查父目录中的 `Update.exe` ，以确定该应用程序是否正在使用Squirrel([see #574](https://github.com/Squirrel/Squirrel.Windows/issues/574#issuecomment-176043311)).
   
```
var assembly = Assembly.GetEntryAssembly();   
var updateDotExe = Path.Combine(Path.GetDirectoryName(assembly.Location), "..", "Update.exe");
var isSquirrelInstall = File.Exists(updateDotExe);
```

## 包装

1. **我怎样才能知道释放出了什么问题?**  
   检查 `packages\Squirrel.Windows.VERSION\tools\SquirrelSetup.log` 用于在创建包时记录信息。
2. **我真的需要将所有松鼠dll添加到我的应用程序中吗?**

你必须将它们全部添加到NuGet包中，然而，[others](https://github.com/Squirrel/Squirrel.Windows/issues/531)已经使用[ILMerge](https://www.microsoft.com/en-us/research/people/mbarnett/#ilmerge)来生成一个单独的程序集。
## 分发

1. **我可以在IIS上分发更新文件吗?**  
是的，你可以查看[Microsoft IIS](using/microsoft-iis.md) 的详细信息。
## 安装   

1. **通过Setup.exe进行的初始安装失败。我怎么知道哪里出了问题?**  
   检查 `%LocalAppData%\SquirrelTemp\SquirrelSetup.log`以获得与初始安装相关的日志。
1. **安装程序不做任何事情。动画会闪烁，但应用程序永远不会启动。**  
  应用程序可能在第一次运行时崩溃(详细信息请参阅 [Debugging Installs](using/debugging-installs.md) )。
1. **安装程序在企业环境中似乎被阻塞了。我如何确认这一点?**  
  如果组策略不允许可执行文件的运行，Squirrel可能会被阻止安装`%LocalAppData%`. 在这种情况下，“安装失败”对话框上的“显示日志”按钮将失败，因为 `Update.exe` 不能运行去创建日志文件。
    你的应用程序`Setup.exe`  仍然应该复制文件到 `%LocalAppData%\SquirrelTemp` 作为预安装步骤。要验证组策略限制了您，请从命令行执行 `Update.exe`，如下所示:
   ```
   C:\>%LocalAppData\MyApp\Update.exe
   This program is blocked by group policy. For more information, contact your system administrator.    
   ```
   最好的做法是请求将Squirrel和您的应用程序的可执行文件由您的公司领主白名单。
1. **没有为我的应用程序创建快捷方式**   
   验证NuGet包元数据id属性中没有。 [空格或[点]](https://github.com/Squirrel/Squirrel.Windows/issues/530) in it.
1. **我可以为Setup.exe安装应用程序使用不同的名称吗?**  
   是的，您可以将`Setup.exe`重命名为任何您想要的名称(例如
 `MyAppSetup.exe`) ([see #611](https://github.com/Squirrel/Squirrel.Windows/issues/611))
1. **病毒扫描程序在MyApp.exe或Update.exe上返回误报。我能做什么?**   
   [Application Signing](using/application-signing.md) will help. In addition, you can submit false positives to the various antivirus authors (e.g., [Symantec](https://submit.symantec.com/false_positive/), [Microsoft](https://www.microsoft.com/security/portal/Submission/Submit.aspx), [AVG](http://www.avg.com/submit-sample), [Comodo](https://www.comodo.com/home/internet-security/submit.php), [McAfee](https://support.mcafeesaas.com/MCAFEE/_cs/AnswerDetail.aspx?aid=65), [List of Submission Locations](http://www.techsupportalert.com/content/how-report-malware-or-false-positives-multiple-antivirus-vendors.htm), [see #218](https://github.com/Squirrel/Squirrel.Windows/issues/218#issuecomment-166406180)).

申请签名会有帮助。此外，您可以向各种杀毒软件作者(例如，赛门铁克、微软、AVG、Comodo、McAfee)提交误报，提交位置列表见#218)。
1. **为什么我的应用程序图标在安装后损坏?**  

在[NuGet Package Metadata](using/nuget-package-metadata.md)中指定的应用程序图标必须是icon (.ICO)类型，而不是图像文件(source: [issue #745](https://github.com/Squirrel/Squirrel.Windows/issues/745))
## 更新

1. **如何确定MyApp中的UpdateManager出了什么问题?**  
您可以设置您的 `\bin`目录，这样您就可以在Visual Studio调试器中执行MyApp，并简单地单步执行更新过程，还可以捕获异常并记录结果(详细信息请参阅调试更新)
2. **我分发了一个坏了的Update.exe副本。我该如何解决这个问题?**  
 副本，该副本在初始安装时成功，但由于某种原因没有执行您想要的操作。要解决这个问题，你可以强制更新`Update.exe` ，方法是在你的应用程序更新包中包含一个`Squirrel.exe` 的副本。如果Squirrel看到这个，它会将这个最新版本复制到本地应用程序安装中。
3. **如何在加载dll时替换它们?不可能的!**  
 你不能。那么，你该怎么做呢?ClickOnce使用的基本技巧是，您有一个包含exe和dll的文件夹，以及一个应用程序快捷方式。当ClickOnce去更新它的东西时，它会建立一个全新的二进制文件文件夹，然后它所做的最后一件事就是重写应用程序的快捷方式来指向新的文件夹。
4. **我之前的应用程序版本在更新后仍然存在。Squirrel不清理旧版本吗?**  
   应用程序的当前版本和前一个版本在清理时不会被删除 (see [issue #589](https://github.com/Squirrel/Squirrel.Windows/issues/589)).
5. **更新后如何持久化[.NET Application Settings](https://docs.microsoft.com/en-us/dotnet/framework/winforms/advanced/application-settings-overview)应用程序设置?**

   See (https://github.com/Squirrel/Squirrel.Windows/issues/198#issuecomment-299262613) 如果您想继续使用.net应用程序设置，那么有一个简单的解决方案。或者，考虑使用一种解决方案，它允许您控制保存设置的位置，并将设置存储在`%LOCALAPPDATA%`下特定于应用程序的位置。
---
| Return: [Table of Contents](readme.md) |
|:---|
