![GitHub License](https://img.shields.io/github/license/voorz/OpenWrt-nikki?style=for-the-badge&logo=github) ![GitHub Tag](https://img.shields.io/github/v/release/voorz/OpenWrt-nikki?style=for-the-badge&logo=github) ![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/voorz/OpenWrt-nikki/total?style=for-the-badge&logo=github) ![GitHub Repo stars](https://img.shields.io/github/stars/voorz/OpenWrt-nikki?style=for-the-badge&logo=github)

English | [中文](README.zh.md)

# Nikki

Transparent Proxy with Mihomo on OpenWrt.

## About This Fork

This is a fork of [nikkinikki-org/OpenWrt-nikki](https://github.com/nikkinikki-org/OpenWrt-nikki) with one functional difference: it fixes the leftover core process bug reported upstream in [#819](https://github.com/nikkinikki-org/OpenWrt-nikki/issues/819). On `reload` and `stop`, the init script now makes sure the old mihomo process is gone (TERM, wait for exit, KILL as a last resort) instead of letting orphaned cores pile up until the router runs out of memory.

Everything else tracks upstream. The differences in distribution are:

- Packages are served from this fork's own feed at [voorz-nikki.pages.dev](https://voorz-nikki.pages.dev), signed with this fork's own key. Installing through the upstream feed or scripts would give you the unpatched upstream build.
- Builds cover only `aarch64_generic` and `aarch64_cortex-a53` on the `openwrt-24.10` SDK (`.ipk` / opkg only, no apk).

## Prerequisites

- OpenWrt >= 24.10
- Linux Kernel >= 5.13
- firewall4

## Feature

- Transparent Proxy (Redirect/TPROXY/TUN, IPv4 and/or IPv6)
- Access Control
- Profile Mixin
- Profile Editor
- Scheduled Restart

## Install & Update

### A. Install From Feed (Recommended)

1. Add Feed

```shell
# only needs to be run once
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/feed.sh | ash
```

2. Install

```shell
# you can install from shell or `Software` menu in LuCI
opkg install nikki
opkg install luci-app-nikki
opkg install luci-i18n-nikki-zh-cn
```

### B. Install From Release

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/install.sh | ash
```

## Uninstall & Reset

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/uninstall.sh | ash
```

## How To Use

See [Wiki](https://github.com/nikkinikki-org/OpenWrt-nikki/wiki)

## How does it work

1. Mixin and Update profile.
2. Run mihomo.
3. Set scheduled restart.
4. Set ip rule/route
5. Generate nftables and apply it.

Note that the steps above may change base on config.

## Compilation

```shell
# add feed
echo "src-git nikki https://github.com/voorz/OpenWrt-nikki.git;main" >> "feeds.conf.default"
# update & install feeds
./scripts/feeds update -a
./scripts/feeds install -a
# make package
make package/luci-app-nikki/compile
```

The package files will be found under `bin/packages/your_architecture/nikki`.

## Dependencies

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

## Contributors

[![Contributors](https://contrib.rocks/image?repo=voorz/OpenWrt-nikki)](https://github.com/voorz/OpenWrt-nikki/graphs/contributors)

## Special Thanks

- [@ApoisL](https://github.com/apoiston)
- [@xishang0128](https://github.com/xishang0128)
