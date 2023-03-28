# RustSBI

官网：<https://github.com/rustsbi>

RustSBI是RISC-V下可用的SBI固件实现，它拥有“独立包”和“原型设计系统”。
RISC-V SBI是RISC-V下不可或缺的固件接口，它提供了足以操作系统使用的基本功能；
更多的功能性接口应当通过其它的工业标准实现。

## 独立包

独立包是分别实现RustSBI的项目，每个不同的主板都拥有不同的仓库和解决方案。
这些方案包括但不限于：

- [rustsbi-k510](https://github.com/Gstalker/rustsbi-k510)
- [rustsbi-d1](https://github.com/rustsbi/rustsbi-d1)
- [rustsbi-hifive-unmatched](https://github.com/rustsbi/rustsbi-hifive-unmatched)
- [rustsbi-qemu](https://github.com/rustsbi/rustsbi-qemu)
- [rustsbi-k210](https://github.com/rustsbi/rustsbi-k210)

这些解决方案的文档和下载链接都在各自的仓库中。

## 原型设计系统

RustSBI原型设计系统提供了从SBI到UEFI、LinuxBoot的完整解决方案，
它拥有一个图形化的编译界面，能在不同的主板上运行。

为了编译原型设计系统，复制仓库后使用以下的命令：

```
cargo termconfig
```

在图形界面配置完毕后，配置文件将保存到`Xtask.toml`文件中，以供编译过程阅读。

接下来，我们可以选择仅编译或者编译并烧录。使用以下的命令编译：

```
cargo make
```

或者，使用以下的命令直接编译和烧录到目标主板：

```
cargo flash
```

RustSBI原型设计系统的链接：<https://github.com/rustsbi/standalone>
