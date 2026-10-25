English | [中文](README.zh.md)

# Nikki (fork)

Transparent proxy with Mihomo on OpenWrt. This is a fork of [nikkinikki-org/OpenWrt-nikki](https://github.com/nikkinikki-org/OpenWrt-nikki) with one fix: on `reload`/`stop`, the init script makes sure the old mihomo process is actually gone (upstream [#819](https://github.com/nikkinikki-org/OpenWrt-nikki/issues/819) — otherwise orphaned cores pile up until the router runs out of memory). Everything else tracks upstream.

Packages are served from this fork's own feed at [voorz-nikki.pages.dev](https://voorz-nikki.pages.dev). Installing through the upstream feed or scripts gives you the unpatched build.

**Scope:** OpenWrt 24.10, opkg, `aarch64_generic` and `aarch64_cortex-a53` only. Requires Linux kernel >= 5.13 and firewall4.

## Install

1. Add the feed (only needs to be run once):

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/feed.sh | ash
```

2. Install (one command — the LuCI app pulls in the core automatically):

```shell
opkg install luci-app-nikki luci-i18n-nikki-zh-cn
```

Drop the second package if you don't need the Chinese UI. Installing from LuCI's *Software* page works too.

## Update

```shell
opkg update
opkg install luci-app-nikki luci-i18n-nikki-zh-cn
```

## Uninstall

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/uninstall.sh | ash
```

## Usage

See the [upstream wiki](https://github.com/nikkinikki-org/OpenWrt-nikki/wiki).
