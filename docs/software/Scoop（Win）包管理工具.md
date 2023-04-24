# scoop

> scoop必要组件： 7zip git innounp lessmsi dark sudo aria2
> scoop我的CLI软件：ffmpeg 、pandoc
>
> main：https://github.com/ScoopInstaller/Scoop



一、安装scoop
- 将scoop安装到自定义目录

```powershell
- $env:SCOOP='D:\Software\Scoop' # 先添加用户级别的环境变量 SCOOP
- [environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')

- Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
#下载安装Scoop（使用$env:SCOOP安装路径）
- scoop install <软件名> 安装到自定义目录
- scoop install <软件名@版本号>  安装特定版本的软件

- scoop install aria2
- Scoop bucket add extras
```

二、配置scoop
- scoop源配置: `scoop config SCOOP_REPO https://gitee.com/squallliu/scoop`

软件仓库bucket源：
软件源使用git版本管理，因此可以使用修改远程仓库的地址修改源地址加快速度。

```shell
cd $env:SCOOP\buckets\Main      
git remote set-url origin http://hub.fastgit.org/ScoopInstaller/Main

cd $env:SCOOP\buckets\Extras
git remote set-url origin https://hub.fastgit.org/ScoopInstaller/Extras
```



- aria2相关配置
```
aria2-enabled (默认值: true)
aria2-retry-wait (默认值: 2)
aria2-split (默认值: 5)
aria2-max-connection-per-server (默认值: 5)
aria2-min-split-size (默认值: 5M)
```


全局安装
- $env:SCOOP_GLOBAL='D:GlobalScoopApps'
- [environment]::setEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'Machine')
- scoop install -g <软件名>   安装到默认全局目录


三、常用bucket
```powershell
#scoop bucket remove main
scoop bucket add main 'https://github.com/ScoopInstaller/Main'
scoop bucket add extras 'https://github.com/ScoopInstaller/scoop-extras'
scoop bucket add versions 'https://github.com/ScoopInstaller/Versions'
scoop bucket add jetbrains 'https://github.com/Ash258/Scoop-JetBrains'
scoop bucket add java 'https://github.com/ScoopInstaller/Java'
scoop bucket add dorado https://github.com/chawyehsu/dorado
scoop bucket add scoopet https://github.com/ivaquero/scoopet

#scoop bucket fastgit镜像
scoop bucket add main 'https://hub.fastgit.org/ScoopInstaller/Main'
scoop bucket add extras 'https://hub.fastgit.org/ScoopInstaller/scoop-extras'
scoop bucket add versions 'https://hub.fastgit.org/ScoopInstaller/Versions'
scoop bucket add jetbrains 'https://hub.fastgit.org/Ash258/Scoop-JetBrains'
scoop bucket add java 'https://hub.fastgit.org/ScoopInstaller/Java'
scoop bucket add dorado 'https://hub.fastgit.org/chawyehsu/dorado'
scoop bucket add scoopet 'https://hub.fastgit.org/ivaquero/scoopet'
```

在软件安装过程中通常会自动添加main bucket，可以通过scoop bucket rm main删除之后重新添加。之后修改链接可以使用如下内容：

```powershell
 cd $env:SCOOP\buckets\Main      这是一个git管理的文件夹
 git remote set-url origin https://hub.fastgit.org/ScoopInstaller/Main
```





安装（ 使用 powershell）
	1. 在 PowerShell 中输入下面内容，保证允许本地脚本的执行：（仅第一次安装前需要执行）
	set-executionpolicy remotesigned -scope currentuser

	2. 然后执行下面的命令安装 Scoop：（稍微卡顿一些，等等就好）
	iex (new-object net.webclient).downloadstring('https://get.scoop.sh')


安装位置说明

卸载（软件的使用权归自己所有，一言不合即卸载）
注意： scoop 管理的软件都会卸载！！！
scoop uninstall scoop

手动删除 scoop 文件（当前用户目录下，同安装目录）

help 查看支持的命令：scoop help


查找软件：scoop search xxx软件包


安装软件：scoop install xxx软件包


卸载软件：scoop  uninstall xxx软件

查看软件官方页：scoop home xxx软件

查看软件详情

查看安装的软件列表：scoop list


更新软件：`scoop update`

查看软件列表：`scoop export >> xxx.txt`

查看 官方支持的 bucket：`scoop bucket known`

查看 bucket 命令帮助：`scoop bucket help`

添加 bucket：`scoop bucket add xxxbucket`

删除 bukcet：：`scoop bucket rm xxx仓库`






常用命令说明

```
alias       Manage scoop aliases # 管理指令的替身
bucket      Manage Scoop buckets # 管理软件仓库
cache       Show or clear the download cache # 查看与管理缓存
checkup     Check for potential problems # 做个体检
cleanup     Cleanup apps by removing old versions # 清理缓存与旧版本软件包
config      Get or set configuration values # 配置Scoop
create      Create a custom app manifest # 创建自定义软件包
depends     List dependencies for an app # 查看依赖
export      Exports (an importable) list of installed apps # 导出软件包列表
help        Show help for a command # 显示帮助指令
hold        Hold an app to disable updates # 禁止软件包更新
home        Opens the app homepage # 打开软件包主页
info        Display information about an app # 显示软件包信息
install     Install apps # 安装软件包的指令
list        List installed apps # 列出所有已安装软件包
prefix      Returns the path to the specified app # 查看软件包路径
reset       Reset an app to resolve conflicts # 恢复软件包版本
search      Search available apps # 搜索软件包
status      Show status and check for new app versions # 查看软件包更新状态
unhold      Unhold an app to enable updates # 启动软件包更新
uninstall   Uninstall an app # 卸载软件包的指令
update      Update apps, or Scoop itself # 更新软件包
virustotal  Look for app hash on virustotal.com # 查看哈希值
which       Locate a shim/executable (similar to 'which' on Linux) # 查看可执行程序路径
```



## Scoop技巧和知识

已剪辑自: https://blog.csdn.net/weixin_39986178/article/details/110900876

本文列举了Scoop各种使用技巧和相关知识。包含：
	• Scoop 的设计与实现理念；
	• 自定义Scoop安装路径；
	• Scoop潜在错误排查；
	• 如何在Scoop中进行断点续传；
	• 更新或禁用软件更新；
	• Scoop中的别名；
	• 如何在同一程序的不同版本之间切换，比如切换不同版本的JDK；
	• 等等各种实用技巧
本文首发于我的个人博客： 你需要掌握的Scoop技巧和知识 www.thisfaner.com 


scoop config SCOOP_REPO https://gitee.com/squallliu/scoop
config已经配置的设置会写进配置文件


Scoop 包管理工具介绍
Windows 下常用的包管理工具有：
	• Scoop
	• Chocolatey

相比于Chocolatey，Scoop则更专注于开源的命令行工具，使用 Scoop 安装的应用程序通常称为"便携式"应用程序，需要的权限更少，对系统产生的副作用也更少，所以我这里选择了使用 Scoop。
注意：对于像 VirtualBox、Docker for Windows ，输入法等这些需要高权限的软件还是通过在官网下载安装包进行安装。

Scoop 安装与配置
要求：
	• PowerShell >= 5.0 (如果是 Window10 则默认满足此条件)
	• 请确保已允许PowerShell执行本地脚本，可以使用下面的命令开启：

	1. set-executionpolicy remotesigned -scope currentuser
	2. 
	3. # 或者 （但是它没有上面的命令安全）
	4. set-executionpolicy Unrestricted -scope currentuser

安装路径：
	• 用户级别安装的程序 和 Scoop 本身默认安装于 C:Users<user>scoop
	• 全局安装的程序（所有用户可用，使用--global或 -g 选项）位
于C\ProgramData\scoop路径中。可以通过更改对应的环境变量更改这些路径 。

将 Scoop 安装到自定义目录 :
打开 PowerShell 先配置环境变量 SCOOP，再运行 iex
	• $env:SCOOP='D:Scoop'
	• # 先添加用户级别的环境变量 SCOOP
	• [environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')
	
	• #下载安装
	
	• #然后下载安装 Scoop （如果使用默认安装路径则直接运行下面的命令）
	• iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
	
	• #或者使用下面的命令安装：
	• iwr -useb get.scoop.sh | iex


配置全局安装路径 （可选，建议不改）
	• $env:SCOOP_GLOBAL='D:GlobalScoopApps'
	
	• [environment]::setEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'Machine')
	
	相当于在系统变量中设置： SCOOP_GLOBAL=D:GlobalScoopApps；默认是在 C:ProgramDatascoop。 

为什么需要全局安装？

对于那些需要管理员权限的程序需要进行全局安装。我当前遇到的是当使用 Scoop 安装字体时需要使用全局安装，因为字体需要给所有用户使用。
初次安装 Scoop 后，建议安装的程序：
	• # 但 scoop 进行全局安装时需要使用到 sudo 命令
	• scoop install sudo
	
	• # scoop下载程序时支持使用 aria2 来加速下载
	• scoop install aria2

我们可以发现，下载的过程中自动下载了依赖 7-zip。 在安装方面，它利用了 7zip 去解
压安装包/压缩包，因此它对绿色软件有天生的友好属性 。不仅如此，下载之后的内容会自
动将加入到（Path）环境变量中，十分方便。
补充： 初次安装之后我们可以通过运行 scoop checkup 来检测当前潜在问题，然后根据提示进行修正。
	• # 检测本人当前环境存在的问题
	• $ scoop checkup
	
可以看到存在三个警告（WARN），一个错误（ERROR），并给出了解决对应问题的命令：
	• 前两个警告（WARN）提示：杀毒软件 Windows Defender 有可能会使得下载变慢或阻止安装
	• 第三个警告（WARN）提示：Windows中的 NTFS 中默认不允许大于 260 个字符（byte）的文件全路径存在的限制还未解除。（可能需要添加sudo才能运行给出的命令）
	• 最后一个错误提示（ERROR）：需要安装 dark 才能解压使用 WiX Toolset 创建的安装包。

Scoop 的设计与实现理念 ：
	• 分离用户数据：默认将程序的 用户数据 存储到 persist 目录中，这样当用户日后升级该程序后之前的用户配置依然可用。（但是对于部分程序支持的不是很完善）
	• shim软链接： scoop 会自动在 scoop 应用安装路径下的 shims 文件夹下为新安装的程序添加对应的 .exe 文件，而 shims 文件夹提前就已被添加到 PATH 环境变量中，所以程序一旦安装就可以直接在命令行中运行。
	• 对于 GUI 程序 ，scoop 还会自动为其在开始菜单中添加快捷方式 ，路径：C:Users<user>AppDataRoamingMicrosoftWindowsStart MenuProgramsScoop Apps


Scoop 常用命令
	1. scoop help #查看帮助
	2. scoop help <某个命令> # 具体查看某个命令的帮助
	3. 
	4. scoop install <app>   # 安装 APP
	5. scoop uinstall <app>  # 卸载 APP
	6. 
	7. scoop list  # 列出已安装的 APP
	8. scoop search # 搜索 APP
	9. scoop status # 检查哪些软件有更新
	10. 
	11. scoop update # 更新 Scoop 自身
	12. scoop update appName1 appName2 # 更新某些app
	13. scoop update *  # 更新所有 app （前提是需要在apps目录下操作）
	14. 
	15. scoop bucket known #通过此命令列出已知所有 bucket（软件源）
	16. scoop bucket add bucketName #添加某个 bucket
	17. 
	18. scoop cache rm <app> # 移除某个app的缓存


安装卸载软件
	1. # 安装之前，通过 search 搜索 APP, 确定软件名称
	2. scoop search  xxx
	3. 
	4. # 安装 APP
	5. scoop install AppName
	6. 
	7. # 安装特定版本的 APP；语法 AppName@[version]，示例
	8. scoop install git@2.23.0.windows.1
	9. 
	10. # 卸载 APP 
	11. scoop uninstall #卸载 APP


更新软件
包含：如何禁用更新
	1. scoop update # 更新 Scoop 自身
	2. 
	3. scoop update appName1 appName2 # 更新某些app
	4. 
	5. # 更新所有 app （可能需要在apps目录下操作）
	6. scoop update *
	7. 
	8. # 禁止某程序更新
	9. scoop hold <app>
	10. # 允许某程序更新
	11. scoop unhold <app>


清除缓存与旧版本
	1. # 查看所有以下载的缓存信息
	2. scoop cache show
	3. 
	4. # 清除指定程序的下载缓存
	5. scoop cache rm <app>
	6. 
	7. # 清除所有缓存
	8. scoop cache rm *
	9. 
	10. # 删除某软件的旧版本
	11. scoop cleanup <app>
	12. 
	13. # 删除全局安装的某软件的旧版本
	14. scoop cleanup <app> -g
	15. 
	16. # 删除过期的下载缓存
	17. scoop cleanup <app> -k

别名
注意：请在 Powershell 中运行下面的命令
	1. # 可用操作
	2. scoop alias add|list|rm [<args>]
	3. 
	4. ## 添加别名，格式：
	5. scoop alias add <name> <command> <description>
	6. 
	7. # 示例：（注意：必须在 Powershell中运行）
	8. scoop alias add st 'scoop status' '检查更新'
	9. # 检查已添加的别名
	10. scoop alias list -v
	11. 
	12. Name Command      Summary
	13. ---- -------      -------
	14. st   scoop status 检查更新
	15. 
	16. # 测试已添加的别名 st
	17. scoop st
	18. 
	19. 
	20. # 另一个示例：
	21. scoop alias add rm 'scoop uninstall $args[0]' '卸载某 app'


在同一程序的不同版本之间切换
使用命令：
scoop reset [app]@[version]
示例：
	1. scoop reset idea-ultimate-eap@201.6668.13
	2. 
	3. scoop reset idea-ultimate-eap@201.6073.9
	4. 
	5. # 切换到最新版本
	6. scoop reset idea-ultimate-eap
对应版本的程序需要已经安装于本地系统中；所以在你清除某个软件的旧版本时考虑一下自己是否还会再次使用到此旧版本。
另外 idea-ultimate-eap 切换过程可能需要更长时间。

其它命令
	1. # 显示某个app的信息
	2. scoop info <app>
	3. 
	4. # 在浏览器中打开某app的主页
	5. scoop home <app>
	6. 
	7. # 比如
	8. scoop home git


添加软件源 Bucket
Scoop 可安装的软件信息存储在 Bucket（翻译为：桶）中，也可以称其为软件源。Scoop 默认的 Bucket 为 main ；官方维护的另一个 Bucket 为 extras，我们需要手动添加。
	• # bucket的用法
	• scoop bucket add|list|known|rm [<args>]

添加 extras :
	scoop bucket add extras
我们也可以添加第三方 bucket ，示例：
	scoop bucket add dorado https://github.com/h404bi/dorado
并且明确指定安装此 bucket （软件源）中的的程序：
	• scoop install dorado/<app_name>
	• # 下面是dorado中特有的软件，测试其是否添加成功
	• scoop search trash


推荐的 Bucket（软件源）：
	• extras：Scoop 官方维护的一个仓库，涵盖了大部分因为种种原因不能被收录进主仓库的常用软件（在我看来是必须要添加的）。地址：lukesampson/scoop-extras
	• nirsoft：是一个 NirSoft 开发的小工具的安装合集。NirSoft 制作了大量的小工具，包括系统工具、网络工具、密码恢复等等，孜孜不倦、持续更新。 
	
		• Bucket 地址：kodybrown/scoop-nirsoft
		• NirSoft 官网地址：NirSoft
	
	• dorado（添加了一些国内的app，比如 qqplayer ️）h404bi/dorado
	• ash258：Ash258/scoop-Ash258
	• java：添加后可以通过它安装各种 jdk 、 jre
	• nerd-fonts ：包含各种字体
	
	1. # 先添加bucket
	2. scoop bucket add extras
	3. scoop bucket add nirsoft
	4. scoop bucket add dorado https://github.com/h404bi/dorado
	5. scoop bucket add Ash258 'https://github.com/Ash258/Scoop-Ash258.git'
	6. scoop bucket add nerd-fonts
	7. # 对于开发人员，可添加下面的两个
	8. scoop bucket add java
	9. scoop bucket add versions


bucket 更新时遇到问题
情况是这样：当我运行 scoop update 进行更新时提示： extras bucket 更新失败。
于是我将其删除后再添加，提示成功，但是它却把 main bucket 给删除了。通过"scoop status"检查状态时出现 "These app manifests have been removed"并且下面列出了已被移除的软件名单。 那么如何解决此问题？
	我们需要重新添加 main bucket ：
	scoop bucket add main #添加 main bucket

网络问题导致app安装失败
一个示例：
	scoop install mediainfo
当安装 mediainfo 时由于网络问题，安装包无法下载，从命令行输出信息中可以看到如下
内容
	1. ERROR Download failed! (Error 1) An unknown error occurred
	2. ERROR https://mediaarea.net/download/binary/mediainfo/19.09/MediaInfo_CLI_19.09_Windows_x64.zip
	3.    referer=https://mediaarea.net/download/binary/mediainfo/19.09/
	4.    dir=D:ScoopApplicationscache
	5.    out=mediainfo#19.09#https_mediaarea.net_download_binary_mediainfo_19.09_MediaInfo_CLI_19.09_Windows_x64.zip
	6. 
	7. ERROR & 'D:ScoopApplicationsappsaria2currentaria2c.exe' --input-file='D:ScoopApplicationscachemediainfo.txt'

我们可以发现文件的下载路径和下载后的文件名称，这里 out= 后面的压缩包就是下载后文件的名称，(也可以在 scoop 的 cache 目录下的 mediainfo.txt 文件中找到下载路径与文件名称)然后我们可以尝试在浏览器或其他下载程序中（可以 fq 的程序中）下载该程序，下载完成后再更改文件名并将其放入 scoop 的 cache 目录，最后再次运行scoop install mediainfo 即可安装。

如何利用 aria2 进行断点续传？
先看具体示例：
	• # 更新 vscode
	• scoop update vscode-portable

scoop 更新 vscode 时下载到 80%的时候 失败了（安装时处理方法也一样）。我们需要在提示中找到如下内容：
	1. 'D:ScoopApplicationsappsaria2currentaria2c.exe' --input-file='D:ScoopApplicationscachevscode-portable.txt' 
	2. --user-agent='Scoop/1.0 (+http://scoop.sh/) PowerShell/5.1 (Windows NT 10.0; Win64; x64; Desktop)' 
	3. --allow-overwrite=true --auto-file-renaming=false 
	4. --retry-wait=2 --split=5 --max-connection-per-server=5 
	5. --min-split-size=5M --console-log-level=warn --enable-color=false 
	6. --no-conf=true --follow-metalink=true --metalink-preferred-protocol=https 
	7. --min-tls-version=TLSv1.2 --stop-with-process=15584 --continue
我们从上面的信息中提取出下面的命令；若要进行断点续传，只需再次执行下面的命令即可：
aria2c.exe --input-file='D:ScoopApplicationscachevscode-portable.txt'

当提示下载完成后，我们需要再次运行 scoop 对应的 app 更新命令（或安装命令），即可完成 app 更新（或安装）：
scoop update vscode-portable

安装和切换JDK、Python的版本
这里需要使用 scoop reset 它的作用是：重置一个应用程序来解决冲突。
命令格式为：
	scoop reset <java>[@<version>]
安装和切换不同的 JDK 版本：
	1. PS C:> scoop bucket add java
	2. 
	3. PS C:> scoop install oraclejdk
	4. Installing 'oraclejdk' (12.0.2-10) [64bit]
	5. 
	6. PS C:> scoop install zulu6
	7. Installing 'zulu6' (6.18.1.5) [64bit]
	8. 
	9. PS C:> scoop install openjdk10
	10. Installing 'openjdk10' (10.0.1) [64bit]
	11. 
	12. PS C:> java -version
	13. openjdk version "10.0.1" 2018-04-17
	14. OpenJDK Runtime Environment (build 10.0.1+10)
	15. OpenJDK 64-Bit Server VM (build 10.0.1+10, mixed mode)
	16. 
	17. PS C:> scoop reset zulu6
	18. Resetting zulu6 (6.18.1.5).
	19. Linking ~scoopappszulu6current => ~scoopappszulu66.18.1.5
	20. 
	21. PS C:> java -version
	22. openjdk version "1.6.0-99"
	23. OpenJDK Runtime Environment (Zulu 6.18.1.5-win64) (build 1.6.0-99-b99)
	24. OpenJDK 64-Bit Server VM (Zulu 6.18.1.5-win64) (build 23.77-b99, mixed mode)
	25. 
	26. PS C:> scoop reset oraclejdk
	27. 
	28. PS C:> java -version
	29. java version "12.0.2" 2019-07-16
	30. Java(TM) SE Runtime Environment (build 12.0.2+10)
	31. Java HotSpot(TM) 64-Bit Server VM (build 12.0.2+10, mixed mode, sharing)

安装和切换不同的 Python 版本：
	1. $ scoop bucket add versions # add the 'versions' bucket if you haven't already
	2. 
	3. $ scoop install python27 python
	4. python --version # -> Python 3.6.2
	5. 
	6. # switch to python 2.7.x
	7. $ scoop reset python27
	8. python --version # -> Python 2.7.13
	9. 
	10. # switch back (to 3.x)
	11. $ scoop reset python
	12. python --version # -> Python 3.6.2



Scoop 文件夹结构（知识补充）

	• Scoop
		• apps # 软件文件夹，所有非全局安装的软件都在这
			§ appname/current # 当前软件版本对应的文件夹的软链接，如果你对某个软件设置调用该文件夹下的软件（例如 maven 环境设为 current 目录，那么这个指向的软件永远都会是最新版本）
		• buckets # 软件源文件夹，所有软件的下载地址等元数据都保存在这里，内部文件夹都是由 git 形成的，因此也可以采用 git pull 来更新源。
		• cache # 软件安装包所在位置，如果遇到软件下载缓慢的情况，也可以用其他工具下载对应软件，然后修改文件名放置到这个目录下进行安装。
		• persist # 永久配置文件夹，大部分的软件的配置都会存到这个目录下，以保证软件最新版用的都是原来的配置。
		• shims # 软件二进制的超链接，基本所有的命令行工具都会在这个文件夹内建立一个超链接，目的是为了防止环境变量 PATH 受到过多污染。
————————————————
版权声明：本文为CSDN博主「Apple_Coco」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Apple_Coco/article/details/113281197


卸载scoop

scoop uninstall scoop
这将卸载Scoop和所有与Scoop一起安装的程序!

在注册表中是由scoop根目录安装的软件路径信息
在文件系统中scoop只存在于预设好的SCOOP='C:\Users\<user>\scoop'目录
环境变量中“<user>\Path\C:\Users\Mxun\scoop\shims"
其它的文件都是指向SCOOP文件夹的链接

The scoop 配置文件保存在  ~/.config/scoop/config.json
buckets源配置文件保存在 SCOOP\apps\scoop\current\buckets.json
	
	{"main": "https://github.com/ScoopInstaller/Main",
	"extras": "https://github.com/ScoopInstaller/Extras"}


​	
国内的scoop源： https://gitee.com/glsnames

	scoop bucket add scoopMain https://gitee.com/glsnames/scoop-main.git
	scoop bucket rm scoopMain
	scoop install scoopMain/<app_name>


将Scoop安装到自定义目录(命令行方式)
之前我们已卸载了scoop 我们现在重新安装并自定义目录。
注意：必须powershell（管理员） 打开。
$env:SCOOP='D:\Software\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')


2. 将Scoop配置为将全局程序安装到自定义目录 SCOOP_GLOBAL(命令行方式)
$env:SCOOP_GLOBAL='F:\GlobalScoopApps'
[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL, 'Machine')



Scoop is already installed. Run ‘scoop update’ to get the latest version.

判断应该是出现了安装损坏或当时安装的时候出错，直接删除安装目录即可，（键入y），并再次执行安装命令，即可成功。

