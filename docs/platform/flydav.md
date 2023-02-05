# FlyDav

## 简介

[FlyDav](https://github.com/pluveto/flydav) 是一个轻量级的开源 webdav 服务器

-   优点
    -   完美兼容 WebDav 协议
    -   支持无配置运行，双击即可开启 WebDav 服务器
    -   完全开源，提供中英文文档
    -   极简，大小 10MB 以内，跨平台
    -   安全，不存储明文密码，隔离不同目录

-   缺点
    -   不支持 SSL
    -   不支持细粒度权限管理

## 部署

最简部署：

1. 首先从 [发布页](https://github.com/pluveto/flydav/releases) 下载 FlyDav。
2. 运行 `./flydav -H 0.0.0.0` 来启动服务器。然后你要输入默认用户 `flydav` 的密码。
3. 在你的 webdav 客户端（比如 RaiDrive）中打开 `http://YOUR_IP:7086/webdav`。

完整部署可参阅文档。
