# eunomia-bpf: 简化和增强 eBPF 与 CO-RE[^1] 和 WebAssembly[^2]

[![Actions Status](https://github.com/eunomia-bpf/eunomia-bpf/workflows/Ubuntu/badge.svg)](https://github.com/eunomia-bpf/eunomia-bpf/actions)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/eunomia-bpf/eunomia-bpf)](https://github.com/eunomia-bpf/eunomia-bpf/releases)
[![codecov](https://codecov.io/gh/eunomia-bpf/eunomia-bpf/branch/master/graph/badge.svg?token=YTR1M16I70)](https://codecov.io/gh/eunomia-bpf/eunomia-bpf)
[![DeepSource](https://deepsource.io/gh/eunomia-bpf/eunomia-bpf.svg/?label=active+issues&show_trend=true&token=rcSI3J1-gpwLIgZWtKZC-N6C)](https://deepsource.io/gh/eunomia-bpf/eunomia-bpf/?ref=repository-badge)
[![CodeFactor](https://www.codefactor.io/repository/github/eunomia-bpf/eunomia-bpf/badge)](https://www.codefactor.io/repository/github/eunomia-bpf/eunomia-bpf)

**一个编译器和运行时框架，以帮助您尽可能轻松地构建和分发 eBPF 程序。**

## 介绍

`eunomia-bpf` 是一个动态加载库/运行时和编译工具链框架，旨在帮助您更轻松地构建和分发 eBPF 程序。

使用 eunomia-bpf，您可以：

- 简化编写 eBPF 程序：
  - 简化构建 CO-RE[^1] `libbpf` eBPF 应用程序：[仅编写 eBPF 内核代码](https://github.com/eunomia-bpf/eunomia-bpf/tree/master/documents/introduction.md#simplify-building-co-re-libbpf-ebpf-applications)，并自动从内核中使用 `perf event` 或 `ring buffer` 自动输出采样数据到内核态。
  - [自动采样](https://github.com/eunomia-bpf/eunomia-bpf/tree/master/documents/introduction.md#automatically-sample-the-data-and-print-hists-in-userspace) 来自 hash mpas 的数据，并在用户空间中打印 `hists`（直方图等信息）。
  - [自动生成](https://github.com/eunomia-bpf/eunomia-bpf/tree/master/documents/introduction.md#automatically-generate-and-config-command-line-arguments) 并配置 eBPF 程序的 `命令行参数`。
  - 您可以同时使用 `BCC` 和 `libbpf` 等多种格式编写内核部分。
- 使用 `Wasm`[^2] 构建 eBPF 程序：参见 [`Wasm-bpf`](https://github.com/eunomia-bpf/wasm-bpf) 项目
  - 在使用 C/C++、Rust、Go…等多种语言，使用 Wasm-bpf 库和工具链来使用 Wasm 编写和运行 eBPF，覆盖从tracing、networking、security到其他用例。
- 简化分发 eBPF 程序：
  - 一个[工具](ecli/)用于将预编译的 eBPF 程序作为 Wasm `OCI` 镜像推送、拉取或运行
  - 在不需要重新编译 eBPF 程序、不限制架构和内核版本的情况下，在[`1` 行 bash](https://github.com/eunomia-bpf/eunomia-bpf/tree/master/documents/introduction.md#dynamic-load-and-run-co-re-ebpf-kernel-code-from-the-cloud-with-url-or-oci-image)中从 `云端存储库` 或 `URL` 运行 eBPF 程序。
  - [动态加载](bpf-loader)带有 `JSON` 配置文件或 `Wasm` 用户态控制和数据处理模块的 eBPF 程序。

更多信息请参见 [documents/introduction.md](https://github.com/eunomia-bpf/eunomia-bpf/tree/master/documents/introduction.md)。

[^1]: CO-RE：[Compile Once – Run Everywhere](https://facebookmicrosites.github.io/bpf/blog/2020/02/19/bpf-portability-and-co-re.html)

[^2]: WebAssembly 或 Wasm：https://webassembly.org/

## eunomia-bpf 提供了大量教程和示例应用，帮助入门 eBPF 程序开发

- Github 模板：[eunomia-bpf/ebpm-template](https://github.com/eunomia-bpf/ebpm-template)
- 示例 bpf 程序：[examples/bpftools](https://github.com/eunomia-bpf/eunomia-bpf/tree/master/examples/bpftools/)
- eBPF 开发教程：[eunomia-bpf/bpf-developer-tutorial](https://github.com/eunomia-bpf/bpf-developer-tutorial)

您可以使用一行 bash 从云端下载预编译的 eBPF 程序并将其运行到内核中：

```bash
# 从 https://github.com/eunomia-bpf/eunomia-bpf/releases/latest/download/ecli 下载 ecli 运行时
$ wget https://aka.pw/bpf-ecli -O ecli && chmod +x ./ecli
$ sudo ./ecli https://eunomia-bpf.github.io/eunomia-bpf/sigsnoop/package.json # 从 url 运行预编译的 ebpf 代码
$ sudo ./ecli sigsnoop:latest # 直接使用名称运行，并从我们的仓库下载最新版本 bpf 工具
```
