中文 | [English](README.md)

# Nikki（fork）

在 OpenWrt 上用 Mihomo 做透明代理。这是 [nikkinikki-org/OpenWrt-nikki](https://github.com/nikkinikki-org/OpenWrt-nikki) 的 fork，只改了一处：`reload`/`stop` 时确保旧的 mihomo 进程真正退出（上游问题 [#819](https://github.com/nikkinikki-org/OpenWrt-nikki/issues/819)——否则残留进程会越积越多，直到路由器内存耗尽）。其余与上游保持一致。

安装包由本 fork 自己的 feed 提供：[voorz-nikki.pages.dev](https://voorz-nikki.pages.dev)。通过上游的 feed 或脚本安装，装到的是未修复的上游版本。

**适用范围：** OpenWrt 24.10、opkg，仅 `aarch64_generic` 与 `aarch64_cortex-a53`。要求 Linux 内核 >= 5.13、firewall4。

## 安装

1. 添加 feed（只需运行一次）：

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/feed.sh | ash
```

2. 用安装脚本安装：

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/install.sh | ash
```

脚本会按系统已装的语言，从本 fork 的 feed 逐个按文件下载并安装核心、LuCI 应用和语言包。按文件装，而不是按名装：某些固件自带第三方源（例如 Kwrt 的 kiddin9），其中的上游 nikki 在按名 `opkg install` 时可能压过本 fork——之前就有路由器这样装上了未修复的版本。装完后，脚本会校验已装核心的版本与 feed 一致，并把核心包 hold 锁定，使之后的按名安装或升级无法悄悄替换它。

## 更新

重跑安装脚本即可：

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/install.sh | ash
```

它会原地升级，随后重复版本校验并重新锁定。

## 卸载

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/uninstall.sh | ash
```

## 使用

见[上游 Wiki](https://github.com/nikkinikki-org/OpenWrt-nikki/wiki)。
