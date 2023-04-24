```bash
apt list --installed
apt list --upgradeable
apt list --all-versions

apt edit-sources

sudo apt build-dep package #安装相关的编译环境，这真是个神技能，有了它，编译安装都变得索然无味了
sudo apt --purge autoremove
apt-get clean && sudo apt-get autoclean  #清理无用的包

aptitude
apt-add-repository [options] repository   #修改软件源命令 (software-properties-common)
```


```bash
apt search package #搜索包 
apt show package #获取包的相关信息，如说明、大小、版本等  
apt depends package #了解使用依赖  
apt rdepends package #查看该包被哪些包依赖  
apt-cache pkgnames  #执行pkgnames子命令列出当前所有可用的软件包 
apt policy package #使用policy命令显示软件包的安装状态和版本信息。

sudo apt install package #安装包  
sudo apt install package=version #安装指定版本的包  
sudo apt install package --reinstall #重新安装包  
sudo apt -f install #修复安装, "-f = --fix-missing"  
sudo apt remove package #删除包
sudo apt purge package  #删除包，包括删除配置文件等
sudo apt autoremove #自动卸载所有未使用的软件包

sudo apt source package #下载该包的源代码   
sudo apt update #更新apt软件源信息  
sudo apt upgrade #更新已安装的包  
sudo apt dist-upgrade #升级系统  
sudo apt dselect-upgrade #使用dselect升级  
sudo apt build-dep package #安装相关的编译环境  
sudo apt clean && sudo apt autoclean #清理无用的包
sudo apt clean  #清理已下载的软件包，实际上是清楚/var/cache/apt/archives目录中的软件包
sudo apt autoclean  #删除已经卸载的软件包备份  
sudo apt-get check #检查是否有损坏的依赖
```


```bash

sudo dpkg -i <package.deb>    #安装包
sudo dpkg -r <package.deb>　  #删除包
sudo dpkg -p <package.deb>　  #彻底删除包(包括配置文件)
dpkg -l                       #列出当前已安装的包

```