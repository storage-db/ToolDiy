WinGet（Windows 程序包管理器：Windows Package Manager）是微软为 win10 开发的一款开源的软件包管理器，于 2020年5月的 Microsoft Build 开发者大会上 首宣。

前提：Windows 10 1709 及以上版本
当前 WinGet 支持的安装程序类型尚不多，除了EXE、MSIX、MSI三种之外，还能够在自定义配置后下载部分微软应用商店的程序。

下载、安装和验证

你可以在 Github Release下载.appxbundle格式的文件，双击打开并运行。

如果出现「此电脑不支持打开该类型文件」的提示，则可在Win + I 进入设置 -> 更新和安全 -> 开发者选项 -> 打开开发人员模式。

输入winget可以查看简略帮助文档；输入winget -v查看版本信息

基本使用

显示简略帮助文档：winget -?（-?可选）；查看特定命令的详细帮助文档：winget [] -?，如winget install -?显示软件详细信息：winget show 搜索软件：winget search 安装软件：winget install 

是的，如你所见，WinGet 并没有自动开启卸载、升级等功能，这也是其在发布之后很长时间不温不火的重要原因。

但是不要着急，截止到2021/03/25发布的最新预览版v0.2.10771，WinGet 实验性功能（需要用户自启）的数量已经增加到了八个，其中就包括uninstall、upgrade、list等重要功能，以及支持安装 Microsoft Store 上的应用程序！

如果想要开启实验功能，可以在终端输入winget settiings，打开 WinGet 配置文件settings.json增加以下内容：

"experimentalFeatures": { "uninstall": true, "upgrade": true, "list": true, "experimentalMSStore": true},

如果想要更改 winget 显示的进度条视觉效果，可以在setting.json里增加：
"visual": { "progressBar": "accent"},# 三种样式可选：accent(默认值)、 retro、 rainbow

winget list > winget.txt 同样支持一键导出软件列表，方便备份和换机重装。

下载 Microsoft Store 软件

实验功能开启"experimentalMSStore": true之后，winget 可以下载 MStore 的软件了（不过目前支持的并不多）。

winget source list查看软件源列表，发现除了winget源之外，MSStore 源已经添加上了。部分商店内软件可以正常下载安装了。


卸载其他源安装的软件

winget 可以卸载winget list 显示出的所有软件。包括电脑上的大多数软件，如Windows系统自带的、手动安装的、Chocolatey 安装的部分等。唯一不足的是，卸载时会被弹出的卸载窗口打断，降低了自动化的一致性。

winget卸载弹窗

winget可以卸载多种类型的软件程序
