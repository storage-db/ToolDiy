# Docker 搭建 C 语言操作系统开发环境

## 预设开发环境简述

- ubuntu 22.04.2 LTS
- gcc 11.3.0
- GNU Make 4.3
- cmake 3.22.1
- QEMU emulator 7.0.0
- code-server 4.10.1
- code-server extensions

     - C/C++ 1.14.4
     - Chinese (Simplified) Language Pack 1.75.0

## 快速开始

安装 Docker Desktop，参见 [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/)。

运行 Docker Desktop，再打开 CMD 或者 PowerShell，执行

```
docker pull jklincn/c-os
```

镜像成功拉取后，执行

```
docker run -d --privileged -p 58888:8080 jklincn/c-os
```

这时使用浏览器打开 [http://localhost:58888](http://localhost:58888) 即可启动开发环境。

后续可以在 Docker Desktop 界面的 Containers 中控制已创建容器的暂停与开启。

>1. 主机映射端口 58888 可随意更换。服务端口 8080 可以通过修改 Dockerfile 更换。

>2. 如果镜像拉取缓慢，可以点击 Docker Desktop 界面右上角齿轮打开设置，在 Docker Engine 配置文件中添加国内源，再点击 `Apply & restart` 重启 Docker，再次尝试拉取。
>
       ```
       "registry-mirrors": [
           "http://hub-mirror.c.163.com",
           "https://docker.mirrors.ustc.edu.cn"
       ]
       ```

## Dockerfile

此处给出镜像的构建脚本，供有需求的同学参考与修改

```dockerfile
FROM ubuntu:22.04
SHELL ["/bin/bash", "-c"]

# 安装必要依赖与开发工具
RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    apt-get update && apt-get install -y \
    gcc-riscv64-unknown-elf gdb-multiarch dosfstools cmake \
    git wget python3 vim file curl \
    autoconf automake autotools-dev  libmpc-dev libmpfr-dev libgmp-dev \
    gawk build-essential bison flex texinfo gperf libtool patchutils bc \
    zlib1g-dev libexpat-dev \
    ninja-build pkg-config libglib2.0-dev libpixman-1-dev libsdl2-dev \ 
    && rm -rf /var/lib/apt/lists/*

# 安装 QEMU
ARG QEMU_VERSION=7.0.0
RUN cd /tmp && \
    wget https://download.qemu.org/qemu-${QEMU_VERSION}.tar.xz && \
    tar xf qemu-${QEMU_VERSION}.tar.xz && \
    cd qemu-${QEMU_VERSION} && \
    ./configure --target-list=riscv64-softmmu,riscv64-linux-user && \
    make -j && \
    make install && \
    cd .. && \
    rm -rf qemu-${QEMU_VERSION} qemu-${QEMU_VERSION}.tar.xz

# 安装 code-server 和扩展
ARG CODE_VERSION=4.10.1
RUN cd /usr/local/ && \
    wget https://github.com/coder/code-server/releases/download/v${CODE_VERSION}/code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    tar xf code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    ln -s  /usr/local/code-server-${CODE_VERSION}-linux-amd64/bin/code-server /usr/bin/code && \
    rm code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    wget https://github.com/microsoft/vscode-cpptools/releases/download/v1.14.4/cpptools-linux.vsix && \
    code --install-extension cpptools-linux.vsix && \
    rm cpptools-linux.vsix && \
    wget https://open-vsx.org/api/MS-CEINTL/vscode-language-pack-zh-hans/1.75.0/file/MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix && \
    code --install-extension MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix && \
    rm MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix

EXPOSE 8080/tcp
CMD ["code", "--auth", "none", "--bind-addr", "0.0.0.0:8080"]
```
