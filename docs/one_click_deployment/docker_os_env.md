# Windows 下使用 Docker 搭建操作系统 C 语言 Web 开发环境

## 开发环境配置

- ubuntu 22.04.2 LTS
- gcc 11.3.0
- GNU Make 4.3
- cmake 3.22.1
- QEMU emulator 7.0.0
- code-server 4.10.1
- code-server 扩展
   * C/C++ 1.14.4
   * Chinese (Simplified) Language Pack 1.75.0

## 快速开始

### 安装 Docker Desktop

参见 [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/)

### 构建镜像

在任意位置创建一个文件夹，在其中新建 `dockfile` 文件，写入以下内容

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
RUN wget https://download.qemu.org/qemu-${QEMU_VERSION}.tar.xz && \
    tar xf qemu-${QEMU_VERSION}.tar.xz && \
    cd qemu-${QEMU_VERSION} && \
    ./configure --target-list=riscv64-softmmu,riscv64-linux-user && \
    make -j && \
    make install

# 安装 code-server 和 cpptools 插件以及中文语言包
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

在该文件夹路径下打开 CMD 或者 PowerShell，执行

```
docker build -t os "."
```

如果最终输出如下信息，则表明镜像构建成功

```
=> exporting to image
=> => exporting layers
=> => writing image sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
=> => naming to docker.io/library/os
```

### 运行开发环境

在任意位置打开 CMD 或者 PowerShell，执行

```
docker run -d --privileged -p 58888:8080 os
```

在使用浏览器打开 http://localhost:58888 即可启动开发环境。

服务端口和主机映射端口均可自由更换。

## 其他说明

### 镜像构建失败或者很慢

镜像构建一般需要几分钟的时间，主要取决于网络速度。

如果被经典的网络连接问题所束缚，也可以选择直接拉取已构建好的镜像（换国内源可以加快速度）

```
docker pull jklincn/c-os
```

