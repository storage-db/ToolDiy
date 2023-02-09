![fzf.png](https://raw.githubusercontent.com/junegunn/i/master/fzf.png)

## 简介

仓库地址：<https://github.com/junegunn/fzf>

FZF 是一款使用 Go 编写的交互式 CLI ，可用来查找任何列表内容、文件、历史指令、进程、host 名、书签或 Git commit 等内容。

![image-20230209215751132](https://pic.skihome.xyz/2023/02/09/63e4fbe7685d2.webp)

## 安装

### macOS

对于 macOS ，推荐使用 Homebrew 进行安装：

```bash
brew install fzf
```

### Linux

在 Linux 发行版上，可使用不同的包管理器进行安装，例如：

**Debian/Ubuntu(Apt)**：

```bash
sudo apt install fzf
```

**ArchLinux(Pacman)**：

```bash
sudo pacman -S fzf
```

### Windows

*并不推荐在 Windows 中使用 FZF 。Windows 可使用 [Everything](https://www.voidtools.com/zh-cn/) 进行搜索。*

Windows下可使用 Scoop 进行安装使用。

```bash
scoop install fzf
```

## 简单使用

### 文件搜索

直接执行 FZF ，打开文件搜索功能。

```bash
fzf
```

在此模式下，用户可输入特定的文件或目录名，FZF 将会在**当前目录**下执行查找，并显示出**指定文件或目录**的**相对路径**。

使用快捷键 `Ctrl+J` 或 `Ctrl+N` 可向下滚动列表； `Ctrl+K` 或 `Ctrl+P` 可向下滚动列表。
使用 `Enter` 选中条目并退出 FZF，`Ctrl+C` 、`Ctrl+G` 或 `Esc` 可退出 FZF 而不进行选择。

### 作为 Vim 插件

FZF 可作为 Vim 的插件使用，方便快速查找需要编辑的文件。

在本例中，使用 vim-plug 插件管理器进行安装：
编辑 `~/.vimrc` 文件，在 `call plug#begin()` 下添加如下行：

```bash
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
```

重新加载 `.vimrc` 文件：

```bash
source ~/.vimrc
```

打开 vim ，并执行 `:PlugInstall` 用于安装插件。

## 更多信息

### 优点

1. 本工具使用 Go 编写，不需其他依赖
2. 性能强悍，搜索效率高
3. 功能丰富，可视化界面(TUI)易于操作
4. 可对接诸多工具(例Vim、tmux 等)
