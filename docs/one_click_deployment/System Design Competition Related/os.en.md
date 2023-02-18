# os Introduction to development environment and tools
```sh 
        # (ubuntu) install package
        sudo apt install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev \
                gawk build-essential bison flex texinfo gperf libtool patchutils bc \
                zlib1g-dev libexpat-dev pkg-config  libglib2.0-dev libpixman-1-dev libsdl2-dev \
                git tmux python3 python3-pip ninja-build
        # install QEMU
        mkdir dev
        pushd dev
        wget https://download.qemu.org/qemu-7.0.0.tar.xz
        tar -xf qemu-7.0.0.tar.xz
        cd qemu-7.0.0
        ./configure --target-list=x86_64-softmmu,aarch64-softmmu,riscv64-softmmu --enable-debug
        make -j$(nproc)
        make install
        popd
        # Configure environment variables
        vi ~/.bashrc
        export PATH=$PATH:/path/to/qemu-7.0.0/build 
        # Update the system path after configuration
        source ~/.bashrc 
        # test qemu
        qemu-system-riscv64 --version
        # install rust 
        curl https://sh.rustup.rs -sSf | sh
        # Update the system path after configuration
        source $HOME/.cargo/env
        # test rust
        rustc --version
        # rust related package installation
        rustup target add riscv64gc-unknown-none-elf
        cargo install cargo-binutils
        rustup component add llvm-tools-preview
        rustup component add rust-src
```
# Common problems and solutions
```sh

        # (centos) install package
        sudo yum install autoconf automake libmpc-devel mpfr-devel gmp-devel gawk bison flex \
                    texinfo patchutils gcc gcc-c++ zlib-devel expat-devel git
        # gcc version is too low
        yum install centos-release-scl
        scl enable devtoolset-8 bash
        # test gcc
        gcc -v

```

# Configure rust download mirror

```sh
        vi ~/.cargo/config
        [source.crates-io]
        registry = "https://github.com/rust-lang/crates.io-index"
        replace-with = 'ustc'
        [source.ustc]
        registry = "git://mirrors.ustc.edu.cn/crates.io-index"`
```
