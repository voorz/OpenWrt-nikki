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

2. 安装（一条命令，LuCI 应用会自动带上核心）：

```shell
opkg install luci-app-nikki luci-i18n-nikki-zh-cn
```

不需要中文界面可去掉第二个包。也可以在 LuCI 的「软件包」页面中安装。

## 更新

```shell
opkg update
opkg install luci-app-nikki luci-i18n-nikki-zh-cn
```

## 卸载

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/uninstall.sh | ash
```

## 使用

见[上游 Wiki](https://github.com/nikkinikki-org/OpenWrt-nikki/wiki)。
