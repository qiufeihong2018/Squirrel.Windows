| [docs](..)  / [using](.) / update-process.md
|:---|


# 更新程序
每次执行应用程序时，`UpdateManager`会执行以下步骤:
1. **检查更新** - 下载发行版位置的 `RELEASES` 文件，并与本地 `RELEASES` 文件进行比较，以检查是否有更新。
2. **下载并验证更新包** - 如果有一个新版本， `UpdateManager`决定是下载deltas还是最新的完整包(通过计算哪一个需要较少的下载)来更新到当前版本。这些包与`RELEASES` 文件中的SHA1进行比较，以进行验证。
3. **从Deltas构建完整的包** - 如果已经下载了delta包，那么将从以前的完整包和下载的delta文件创建一个新的完整包。
3. **安装新版本** - 从完整包中提取当前版本的MyApp，并基于版本号(例如app-1.0.1)将其放在新的 `%LocalAppData%\MyApp` 安装目录中。
4. **更新快捷方式** - 桌面和Windows开始菜单快捷方式指向新MyApp版本更新(通过——`--processStart` 命令行参数传递给`Update.exe`)。
5. **前一个版本清理** - o下一次启动MyApp时，除当前版本和前一个版本外的所有应用都将被删除(例如更新到app-1.0.5后，app-1.0.4将保留，但app-1.0.3及前一个版本将被删除) - see [issue #589](https://github.com/Squirrel/Squirrel.Windows/issues/589)). 

## 回滚

目前，没有内置回滚到以前版本的支持。

## See Also

* [Update Manager](update-manager.md) - reference guide for the `UpdateManager`. 
* [Debugging Updates](debugging-updates.md) - tips on debugging your Squirrel application.


---
| Return: [Table of Contents](../readme.md) |
|----|

