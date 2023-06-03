# windows环境部署

本文向大家介绍自己的windows环境如何部署该项目

 > 注意：这里需要用到python环境,本人是`python3.10`

## 下载 ToolDiy

```
git clone https://github.com/cargo-youth/ToolDiy.git
```
## 安装 mkdocs

```
下载链接：pip install mkdocs
```
## 安装网站主题

本站主题是material，使用下面命令进行安装即可。
```
pip install mkdocs-material
```

## 安装其它依赖

```
pip install pymdown-extensions
pip install mkdocs-awesome-pages-plugin
```

## 安装i18n

这里是个坑，我安装的时候，直接安装`pip install i18n`不行，你需要专门安装mkdocs下的i18n,然后问的chatGPT,他给我提供的解决方案是`pip install mkdocs-i18n-plugin`;可惜不对，最后在谷歌上找到下面命令，就对了。
```
pip install mkdocs-static-i18n
```

## 运行项目

```
mkdocs serve
```

## 构建静态网站文件

```
mkdocs build
```


















