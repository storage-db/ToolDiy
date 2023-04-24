# Chocolatey（WIN）

>本文介绍了 Chocolatey 的安装与使用过程。这篇文章不是为普通用户编写的，而是给需要统一开发环境的开发人员写的
>
>为什么要用 Chocolatey
>
>如果使用过 Linux 一定熟悉一行代码进行软件的搜索，安装，更新，卸载等所有操作。而 Windows 中的也有包管理器 Chocolatey 。虽然没有 Linux 里的包管理器那么强大，但让 Windows  安装软件方便了很多。

## Chocolatey 的安装
- 方法一：以管理员身份打开 cmd.exe （很重要），执行以下代码
```cmd
 @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

- 方法二：以管理员身份打开 powershell.exe ，执行以下代码

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

- 方法三：直接打开 https://chocolatey.org/install.ps1 ，复制内容到本地新建 install.psl 文件，执行安装。
	
在有的时候，因为电脑安装防火墙的原因，可能会导致前两个方法出现问题，但是方法三不存在此问题，最好用 powershell.exe 来执行 install.psl 脚本，可以看到安装的完整过程。


## Chocolatey 的使用
Chocolatey 运行需要的环境：
- Windows 7+ / Windows Server 2003+
- PowerShell v2+
- .NET Framework 4+ （不用安装，安装脚本时会自动安装）


### 安装软件

```powershell
choco install -y git 
choco install -y python 
choco install -y chromium
cinst -y nodejs.install
...
```

choco 和 cinst 都是安装命令， -y 避免对协议的二次确认，可以在官网 https://chocolatey.org/packages 查找确认自己要安装的包。

### 查找软件

1. choco search cntlm 搜索软件是否存在，包名是什么。
2. choco info cntlm 查看软件详细信息。

### 升级软件

`choco upgrade git`

### 卸载软件

`choco uninstall git`


### 配置统一环境

```xml
choco install dev-package.config
dev-package.config:
<?xml version="1.0" encoding="utf-8"?>
    <packages>
      <package id="jdk8" />
      <package id="googlechrome" version="71.0.3578.98" />
      <package id="vscode" />
      <package id="7zip" />
    </packages>
```

文件名称随意，但是扩展名必须是 .config 。通过 .config 的方式，就可以配置一个团队统一的开发环境，软件和版本都可以统一。这样可以为开发带来很多好处，避免由于开发环境不一样引起的各种不同错误。
通过传统方式安装软件，如果配置了环境变量，例如 JAVA_HOME ， PATH 等等，都需要重启命令行工具，甚至要等一会才能生效。 Chocolatey 提供了一个 refreshenv 命令，可以快速生效环境变量。

### 更改本地仓库

- 方法一： cmd.exe 管理员模式下执行以下指令
    setx ChocolateyInstall D:\Chocolatey /M
- 方法二： powershell.exe 管理员模式下执行以下指令
    & setx.exe ChocolateyInstall D:\Chocolatey /M
    设定成功提示：
    成功: 已经存储指定的值

## 卸载Chocolatey

卸载 Chocolatey 只需要删除它安装的文件夹，并删除对应的环境变量即可。对于使用 Chocolatey 安装的其它软件，如果也需要卸载的话，需要先手动卸载。

1. 删除环境变量 ChocolateyInstall 对应的安装文件夹，默认是 C:\ProgramData\chocolatey 
2. 删除环境变量 ChocolateyInstall
3. 删除环境变量 ChocolateyToolsLocation ，部分工具软件安装的位置，删除需谨慎
4. 删除环境变量 ChocolateyLastPathUpdate
5. 更新环境变量 PATH ，去掉 Chocolatey 相关的配置



## 总结

Chocolatey 更注重的是整个团队的软件配置统一，统一用某一个软件，统一用某一个版本，统一安装配置(包括安装路径)。在实际开发中，太多次因为安装路径引起问题，例如路径里有空格或中文等等。最好就用默认安装路径。
