# os开发环境和工具介绍

```sh
# (ubuntu) 安装QEMU7.0依赖包
sudo apt install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev \
        gawk build-essential bison flex texinfo gperf libtool patchutils bc \
        zlib1g-dev libexpat-dev pkg-config  libglib2.0-dev libpixman-1-dev libsdl2-dev \
        git tmux python3 python3-pip ninja-build
# 在开发目录执行安装
mkdir dev
pushd dev
wget https://download.qemu.org/qemu-7.0.0.tar.xz
tar -xf qemu-7.0.0.tar.xz
cd qemu-7.0.0
./configure --target-list=x86_64-softmmu,aarch64-softmmu,riscv64-softmmu --enable-debug
make -j$(nproc)
make install
popd
# 配置环境变量
vi ~/.bashrc
export PATH=$PATH:/path/to/qemu-7.0.0/build 
# 配置后更新系统路径
source ~/.bashrc 
# 检测qemu版本(以riscv64 为例上诉配置已将x86_64 aarch64 riscv64安装好均可以检测版本)
qemu-system-riscv64 --version
# 配置rust环境
curl https://sh.rustup.rs -sSf | sh
# 配置环境变量
source $HOME/.cargo/env
# 检测版本
rustc --version
# rust相关软件包安装
rustup target add riscv64gc-unknown-none-elf
cargo install cargo-binutils
rustup component add llvm-tools-preview
rustup component add rust-src
```

## 常见问题及解决办法

```sh
# centos 依赖安装
sudo yum install autoconf automake libmpc-devel mpfr-devel gmp-devel gawk bison flex \
                texinfo patchutils gcc gcc-c++ zlib-devel expat-devel git
# gcc版本过低导致的qemu编译失败(也可以直接官网更高版本安装)
yum install centos-release-scl
scl enable devtoolset-8 bash
# 查看gcc版本
gcc -v
```

## 配置rust下载镜像

```sh
vi ~/.cargo/config
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"
```
