![GitHub License](https://img.shields.io/github/license/voorz/OpenWrt-nikki?style=for-the-badge&logo=github) ![GitHub Tag](https://img.shields.io/github/v/release/voorz/OpenWrt-nikki?style=for-the-badge&logo=github) ![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/voorz/OpenWrt-nikki/total?style=for-the-badge&logo=github) ![GitHub Repo stars](https://img.shields.io/github/stars/voorz/OpenWrt-nikki?style=for-the-badge&logo=github)

中文 | [English](README.md)

# Nikki

在 OpenWrt 上使用 Mihomo 进行透明代理。

## 关于本 Fork

本仓库是 [nikkinikki-org/OpenWrt-nikki](https://github.com/nikkinikki-org/OpenWrt-nikki) 的 fork，只有一处功能差异：修复了上游 [#819](https://github.com/nikkinikki-org/OpenWrt-nikki/issues/819) 报告的残留核心进程问题。init 脚本在 `reload` 和 `stop` 时会确保旧的 mihomo 进程退出（先 TERM、等待退出、最后 KILL 兜底），而不是放任孤儿进程堆积直至路由器内存耗尽。

其余与上游保持一致。分发方式的区别：

- 安装包由本 fork 自己的软件源 [voorz-nikki.pages.dev](https://voorz-nikki.pages.dev) 提供，使用本 fork 自己的密钥签名。通过上游的源或脚本安装，得到的将是不带修复的上游版本。
- 仅构建 `aarch64_generic` 和 `aarch64_cortex-a53`，基于 `openwrt-24.10` SDK（仅 `.ipk` / opkg，不提供 apk）。

## 环境要求

- OpenWrt >= 24.10
- Linux Kernel >= 5.13
- firewall4

## 功能

- 透明代理 (Redirect/TPROXY/TUN, IPv4 和/或 IPv6)
- 访问控制
- 配置文件混入
- 配置文件编辑器
- 定时重启

## 安装和更新

### A. 从软件源安装（推荐）

1. 添加源

```shell
# 只需运行一次
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/feed.sh | ash
```

2. 安装

```shell
# 你可以从 shell 执行命令安装或者从 LuCI 的`软件包`菜单安装
opkg install nikki
opkg install luci-app-nikki
opkg install luci-i18n-nikki-zh-cn
```

### B. 从发行版安装

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/install.sh | ash
```

## 卸载并重置

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/uninstall.sh | ash
```

## 如何使用

查看 [Wiki](https://github.com/nikkinikki-org/OpenWrt-nikki/wiki)

## 如何工作

1. 混入并更新配置文件。
2. 启动 Mihomo。
3. 设置定时重启。
4. 配置 IP 规则/路由。
5. 生成防火墙配置并应用。

注意上述步骤可能因配置而变动。

## 编译

```shell
# 添加源
echo "src-git nikki https://github.com/voorz/OpenWrt-nikki.git;main" >> "feeds.conf.default"
# 更新并安装源
./scripts/feeds update -a
./scripts/feeds install -a
# 编译
make package/luci-app-nikki/compile
```

编译结果可以在`bin/packages/your_architecture/nikki`内找到。

## 依赖

- ca-bundle
- curl
- yq
- firewall4
- ip-full
- kmod-inet-diag
- kmod-nft-socket
- kmod-nft-tproxy
- kmod-tun
- kmod-dummy

## 贡献者

[![贡献者](https://contrib.rocks/image?repo=voorz/OpenWrt-nikki)](https://github.com/voorz/OpenWrt-nikki/graphs/contributors)

## 特别感谢

- [@ApoisL](https://github.com/apoiston)
- [@xishang0128](https://github.com/xishang0128)
