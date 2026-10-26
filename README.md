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

2. Install with the installer script:

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/install.sh | ash
```

The script installs the core, the LuCI app and the language packs matching your system, downloading each package file directly from this fork's feed. Install by file, not by name: some firmware bundles a third-party feed (for example Kwrt's kiddin9) whose upstream nikki can outrank this fork in a by-name `opkg install` — that is how routers ended up with the unpatched build. After installing, the script verifies the core version against the feed and holds the package, so a later by-name install or upgrade cannot silently replace it.

## Update

Re-run the installer:

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/install.sh | ash
```

It upgrades the packages in place, then repeats the version check and re-applies the hold.

## Uninstall

```shell
wget -O - https://github.com/voorz/OpenWrt-nikki/raw/refs/heads/main/uninstall.sh | ash
```

## Usage

See the [upstream wiki](https://github.com/nikkinikki-org/OpenWrt-nikki/wiki).
