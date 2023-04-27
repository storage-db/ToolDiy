# Scoop(Win)

> scoop 必要组件： 7zip git innounp lessmsi dark sudo aria2
>
> main : https://github.com/ScoopInstaller/Scoop

## 一、安装 scoop
- 将 scoop 安装到自定义目录

```powershell
# 设置自定义安装路径：D:\Software\Scoop
$env:SCOOP='D:\Software\Scoop';[environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')

# 允许执行本地脚本
set-executionpolicy remotesigned -scope currentuser

# 从 github 下载并安装 scoop
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```

## 二、配置scoop
- scoop 源配置: `scoop config SCOOP_REPO <URL>`

**软件仓库 bucket 源：软件源使用 git 版本管理，因此可以使用修改远程仓库的地址修改源地址加快速度。**

```shell
cd $env:SCOOP\buckets\Main      
git remote set-url origin <URL>

cd $env:SCOOP\buckets\Extras
git remote set-url origin <URL>
```

- 修改 buckets git 仓库链接：

```powershell
 cd $env:SCOOP\buckets\Main      这是一个 git 管理的文件夹
 git remote set-url origin https://hub.fastgit.org/ScoopInstaller/Main
```

- aria2 相关配置
```
aria2-enabled (默认值: true)
aria2-retry-wait (默认值: 2)
aria2-split (默认值: 5)
aria2-max-connection-per-server (默认值: 5)
aria2-min-split-size (默认值: 5M)
```


## 三、常用 bucket
```powershell
#scoop bucket remove main
scoop bucket add main 'https://github.com/ScoopInstaller/Main'
scoop bucket add extras 'https://github.com/ScoopInstaller/scoop-extras'
scoop bucket add versions 'https://github.com/ScoopInstaller/Versions'
scoop bucket add jetbrains 'https://github.com/Ash258/Scoop-JetBrains'
scoop bucket add java 'https://github.com/ScoopInstaller/Java'
scoop bucket add dorado https://github.com/chawyehsu/dorado
scoop bucket add scoopet https://github.com/ivaquero/scoopet
```

1. 查看支持的命令：scoop help
2. 查找软件：scoop search xxx 软件包
3. 安装软件：scoop install xxx 软件包
4. 卸载软件：scoop  uninstall xxx 软件
5. 查看软件官方页：scoop home xxx 软件
6. 查看安装的软件列表：scoop list
7. 更新软件：`scoop update`
8. 查看软件列表：`scoop export >> xxx.txt`
9. 查看 官方支持的 bucket：`scoop bucket known`
10. 查看 bucket 命令帮助：`scoop bucket help`
11. 添加 bucket ：`scoop bucket add xxxbucket`
12. 删除 bukcet ：`scoop bucket rm xxx 仓库`

常用命令说明

```powershell
alias       Manage scoop aliases # 管理指令的替身
bucket      Manage Scoop buckets # 管理软件仓库
cache       Show or clear the download cache # 查看与管理缓存
checkup     Check for potential problems # 做个体检
cleanup     Cleanup apps by removing old versions # 清理缓存与旧版本软件包
config      Get or set configuration values # 配置 Scoop
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

## 卸载Scoop

`scoop uninstall scoop`：这将卸载 Scoop 和所有与 Scoop 一起安装的程序!

The scoop 配置文件保存在  `~/.config/scoop/config.json`
buckets 源配置文件保存在 `SCOOP\apps\scoop\current\buckets.json`

```json
{
	"main": "https://github.com/ScoopInstaller/Main",
	"extras": "https://github.com/ScoopInstaller/Extras"
}
```

## Scoop 技巧和知识

链接: https://blog.csdn.net/weixin_39986178/article/details/110900876

相比于 Chocolatey ， Scoop 则更专注于开源的命令行工具，使用 Scoop 安装的应用程序通常称为"便携式"应用程序，需要的权限更少，对系统产生的副作用也更少，所以我这里选择了使用   Scoop。
注意：对于像 VirtualBox、Docker for Windows ，输入法等这些需要高权限的软件还是通过在官网下载安装包进行安装。
