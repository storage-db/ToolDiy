# Rust-based operating system development environment using Docker

## Development environment configuration

- ubuntu 22.04.2 LTS
- GNU Make 4.3
- QEMU emulator 7.0.0
- rustc nightly-latest
- rustup latest
- cargo nightly-latest
- code-server 4.10.1
- code-server 扩展

     - rust-analyzer 0.3.1435
     - Chinese (Simplified) Language Pack 1.75.0

## Quick Start

### Install Docker Desktop

See [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/)

### Build Image

Create a folder in any path, create a new `dockerfile` file in it, and write the following contents

```dockerfile
FROM ubuntu:22.04
SHELL ["/bin/bash", "-c"]

# Install necessary dependencies and development tools
RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    apt-get update && apt-get install -y \
    gcc-riscv64-unknown-elf gdb-multiarch dosfstools cmake \
    git wget python3 vim file curl \
    autoconf automake autotools-dev  libmpc-dev libmpfr-dev libgmp-dev \
    gawk build-essential bison flex texinfo gperf libtool patchutils bc \
    zlib1g-dev libexpat-dev \
    ninja-build pkg-config libglib2.0-dev libpixman-1-dev libsdl2-dev \ 
    && rm -rf /var/lib/apt/lists/*

# Install QEMU
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

# Install code-server and extensions
ARG CODE_VERSION=4.10.1
RUN cd /usr/local/ && \
    wget https://github.com/coder/code-server/releases/download/v${CODE_VERSION}/code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    tar xf code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    ln -s  /usr/local/code-server-${CODE_VERSION}-linux-amd64/bin/code-server /usr/bin/code && \
    rm code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    wget https://openvsxorg.blob.core.windows.net/resources/rust-lang/rust-analyzer/linux-x64/0.3.1435/rust-lang.rust-analyzer-0.3.1435@linux-x64.vsix && \
    code --install-extension rust-lang.rust-analyzer-0.3.1435@linux-x64.vsix && \
    rm rust-lang.rust-analyzer-0.3.1435@linux-x64.vsix && \
    wget https://open-vsx.org/api/MS-CEINTL/vscode-language-pack-zh-hans/1.75.0/file/MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix && \
    code --install-extension MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix && \
    rm MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix

WORKDIR /root
# Install rust
ARG RUST_VERSION=nightly
ENV RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
ENV RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
RUN mkdir .cargo && \
    echo '[source.crates-io]' >> .cargo/config && \
    echo 'registry = "https://github.com/rust-lang/crates.io-index"' >> .cargo/config && \
    echo 'replace-with = "ustc"' >> .cargo/config && \
    echo '[source.ustc]' >> .cargo/config && \
    echo 'registry = "git://mirrors.ustc.edu.cn/crates.io-index"' >> .cargo/config && \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs -o rustup-init && \
    chmod +x rustup-init && \
    ./rustup-init -y --default-toolchain ${RUST_VERSION} --target riscv64imac-unknown-none-elf && \
    rm rustup-init && \
    source $HOME/.cargo/env && \
    cargo install cargo-binutils && \
    rustup component add llvm-tools-preview && \
    rustup component add rust-src

EXPOSE 8080/tcp
CMD ["code", "--auth", "none", "--bind-addr", "0.0.0.0:8080"]
```

Open CMD or PowerShell in the folder path and execute

```
docker build -t os "."
```

If the final output the following information shows that image builds successfully

```
=> exporting to image
=> => exporting layers
=> => writing image sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
=> => naming to docker.io/library/os
```

### Run Development Environment

Open CMD or PowerShell at any path, execute

```
docker run -d --privileged -p 58888:8080 os
```

Open [http://localhost:58888](http://localhost:58888) in browser to start development environment

PS: The service port and host mapping port can be freely changed

## Others

### Image build failed or slowly

Image build generally takes several minutes, mainly depending on the network speed

You can pull the image directly

```
docker pull jklincn/rust-os
```

