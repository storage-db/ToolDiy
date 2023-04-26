# pacman（Arch）包管理工具

Manjaro 换源

```shell
sudo pacman-mirrors -i -c China -m rank
sudo pacman -Syy
```


## 1. 更新系统

	命令	解释
	pacman -Syu	对整个系统进行更新（常用）
	pacman -Syy	强制更新
	pacman -Syudd	使用 -dd跳过所有检测

## 2. 搜索包

	命令	解释
	pacman -Ss keyword	在仓库中搜索含关键字的包（常用）pacman -Ss '^fcitx-'
	pacman -Qs keyword	搜索已安装的包（常用）pacman -Qs '^fcitx-'
	pacman -Qi package_name	查询本地安装包的详细信息
	pacman -Ql package_name	列出该包的文件
	pacman -Fs keyword	按文件名查找软件库
	pacman -Si package_name	显示远程软件包的详尽的信息
	pacman -Qii package_name	使用两个 -i 将同时显示备份文件和修改状态
	pacman -Ql package_name	要获取已安装软件包所包含文件的列表
	pacman -Fl package_name	查询远程库中软件包包含的文件
	pacman -Qk package_name	检查软件包安装的文件是否都存在
	pacman -Fo /path/to/file_name	查询文件属于远程数据库中的哪个软件包
	pacman -Qdt	要罗列所有不再作为依赖的软件包(孤立 orphans )
	pacman -Qet	要罗列所有明确安装而且不被其它包依赖的软件包
	pactree package_name	要显示软件包的依赖树
	whoneeds package_name	检查一个安装的软件包被那些包依赖pkgtoolsAUR中的whoneeds
	pactree -r package_name	检查一个安装的软件包被那些包依赖

## 3. 安装包

	命令	解释
	pacman -S package_name	执行 pacman -S firefox 将安装 Firefox（常用）
	pacman -Sy package_name	将在同步包数据库后再执行安装。
	pacman -Sv package_name	在显示一些操作信息后执行安装。
	pacman -U local_package_name	安装本地包，其扩展名为pkg.tar.gz或pkg.tar.xz
	pacman -U url	安装一个远程包（不在 pacman 配置的源里面）

## 4. 删除包

	命令	解释
	pacman -R package_name	该命令将只删除包，保留其全部已经安装的依赖关系
	pacman -Rs package_name	在删除包的同时，删除其所有没有被其他已安装软件包使用的依赖关系（常用）
	pacman -Rsc package_name	在删除包的同时，删除所有依赖这个软件包的程序
	pacman -Rd package_name	在删除包时不检查依赖

## 5. 其他用法

	pacman -Sw package_name	只下载包，不安装。
	pacman -Sc	清理未安装的包文件（常用）包文件位于 /var/cache/pacman/pkg/ 目录
	pacman -Scc	清理所有的缓存文件（常用）

# Manjaro软件管理

## 1. 切换国内最快的软件源

大多数 Linux 发行版都是来自国外，自然官方仓库地址也在国外，所以一般情况下安装完 Linux 发行版之后做的第一件事就是切换源为国内的源。源的切换操作，大部分发行版也都支持 GUI 切换，这里只列出在命令行下如何擦操作

## 1. 第一部分使用 pacman-mirrors 更新官方软件源

### 1.1 按照地区自动更新为最快最稳定的软件源镜像地址

`sudo pacman-mirrors --country China`

### 1.2. 恢复默认软件源操作

`sudo pacman-mirrors --interactive --default`


### 1.3 软件源更新之后，我们一般会进行系统更新

`sudo pacman -Syyu# 软件源更新完成之后进行系统软件更新操作`


### 1.4 查看所有可用的地区信息
`sudo pacman-mirrors -l`

参考翻译自： https://wiki.manjaro.org/index.php?title=Use_pacman-mirrors_to_Set_the_Fastest_Download_Server

## 2. 使用 pacman 管理软件

## 2. 第二部分使用 pacman 管理软件
### 2.1 同步并且更新你的系统
`sudo pacman -Syyu`

### 2.2 在软件仓库中搜索软件
`sudo pacman -Ss [software package name]`

### 2.3 查看已安装软件

`sudo pacman -Qs [software package name]`
`sudo pacman -Qi [software package name]`# 附带详细信息
`sudo pacman -Qii [software package name]`# 附带更加详细的包信息
`sudo pacman -Ql`# 列出所有安装的软件包

### 2.4 查看软件的详细依赖

`sudo pactree [software package name]`

### 2.5 查看系统中那些没有被使用软件依赖包（orphans）

`sudo pacman -Qdt`

### 2.6 自动移除那些系统中没有被使用的依赖包【类似于Debian下的 sudo apt autoremove --purge】

`sudo pacman -Rs $(pacman -Qdtq)`

### 2.7 下载并安装软件包

`sudo pacman -Syu [software package name]`# 从软件仓库安装
`yay -S [software package name]`# Packages from the AUR
`sudo pacman -U [/package_path/][software package name.pkg.tar.xz]`# 从本地安装

`pacman -U http://www.examplepackage/repo/examplepkg.tar.xz`# 从网络安装【非官方仓库】

### 2.8 卸载软件

`sudo pacman -R [software package name]`
`sudo pacman -Rs [software package name]`# 同时删除依赖
`sudo pacman -Rns [software package name]`# 删除软件及其依赖，还有pacman生成的配置文件，即更彻底的删除

### 2.9 清空缓存【默认情况下安装软件会先来缓存中查看是否已经下载过，没有再去下载，软件安装后通常下载缓存还在】

`sudo pacman -Sc`
`sudo pacman -Scc` # 更彻底的清理

关于 pacman 常用就这些了，更多请使用 man pacman OR pacman -h 去查看
参考翻译自： https://wiki.manjaro.org/index.php?title=Pacman_Overview
From < https://csdnimg.cn/release/phoenix/template/new_img/articleReadEyes.png> 
