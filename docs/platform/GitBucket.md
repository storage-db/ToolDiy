# GitBucket

## 简介

[GitBucket](https://gitbucket.github.io/)
是一个非常好的免费开源，易部署的开源Git平台，同时拥有诸多优势，虽然也有弊端。

-   优点

    -   完全开源，没有任何限制；

    -   运行在JVM平台上，非常容易部署；

    -   类似于GitHub的界面，操作容易；

    -   丰富的插件，使得扩展非常容易；

    -   提供了大量兼容GitHub的API；

-   缺点

    -   有点残废的权限管理（权限没有依照公开，私有库区分）；

    -   开发语言为Scala，对于非Scale用户自己写插件有一定门槛；

    -   由于作者暂未完成平台升级，暂时无法部署在除Tomcat之外的Servlet容器。

## 部署

1.  下载 [Release](https://github.com/gitbucket/gitbucket/releases)
    里面的war到你的服务器；

2.  `java -jar gitbucket.war` 启动。（笔者用的是JDK17）；

3.  (可选)将启动端口反向代理到子域名。
