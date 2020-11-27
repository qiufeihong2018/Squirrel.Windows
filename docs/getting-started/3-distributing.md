| [docs](..) / [getting-started](.) / 3-distributing.md |
|:---|

# Step 3. 分发

 在打包MyApp进行分发之后，使用 `Releases` 目录中的各种文件将MyApp分发给用户。
* **设置应用程序** - the `Setup.exe`  应用程序提供给新用户以安装当前版本的MyApp(详细信息请参阅[Installing](4-installing.md) )。
* **更新文件** - 
RELEASES` 文件以及版本化的完整包和增量包由更新过程使用(详细信息请参阅更新)。
## 本地文件分布


为简单起见，这个入门指南使用本地文件系统位置进行更新。该位置在提供给UpdateManager的更新位置中定义(请参阅集成:[Integrating: Basic Updating](1-integrating.md)中的代码)。

这通常是不实际的更新，除非您的所有用户都可以访问类似的网络路径，文件可以轻松地放置在其中。


---
| Previous: [2. Packaging](2-packaging.md) | Next: [4. Installing](4-installing.md)|
|:---|:---|

