# YunoHost MTG Proxy

This repository contains the YunoHost packaging for [MTG](https://github.com/9seconds/mtg), a highly-opinionated MTPROTO proxy for Telegram.

## Features

- **Domain-less installation**: This package runs as a standalone global YunoHost system service and does not depend on a YunoHost web domain or NGINX configuration.
- **Auto-fetching**: The installation automatically detects your server's architecture (`amd64`, `armhf`, `arm64`, `i386`) and downloads the latest binary directly from the official MTG GitHub releases.
- **Customizable**: Prompted configurations at install time based on `example.config.toml` (port, secret/domain generation, DNS, Prometheus).
- **Auto-generation of Secret**: You can either supply an existing MTProto secret (starting with `ee...`) or just enter a domain for domain fronting (e.g., `google.com`), and the install script will generate the secret for you.

## How to Install

You can install this app using the YunoHost admin panel or the command line.

### Via Command Line

```bash
yunohost app install https://github.com/YourUsername/mtg_ynh
```

### Installation Options

During installation, you will be asked the following questions:
- **Port**: The port to bind the proxy to (Default: `3128`).
- **MTProto Secret**: Your proxy secret. If you do not have one, you can enter a public domain name (e.g., `google.com` or `storage.googleapis.com`) and the script will automatically generate a secure secret for domain fronting.
- **DNS IP**: The DNS resolver IP to use (Default: `1.1.1.1`).
- **Prometheus Logs**: Enable Prometheus metrics (Default: `false`).

## Updating

The package upgrade script natively checks the MTG GitHub repository and fetch the latest binary release avoiding the need for a package update from the packager on each MTG release. Simply run through the YunoHost upgrade process or command line:
```bash
yunohost app upgrade mtg -u https://github.com/YourUsername/mtg_ynh
```

## Logs and Management

You can manage the proxy service via standard systemd commands if needed:
```bash
systemctl status mtg
systemctl restart mtg
```

Configuration is stored in `/etc/mtg/mtg.toml`. The binary itself is located under `/opt/mtg/mtg`.

## References
- [YunoHost App Packaging Documentation](https://doc.yunohost.org/en/dev/packaging/)
- [YunoHost Example App](https://github.com/YunoHost/example_ynh)
- [MTG Official Repository](https://github.com/9seconds/mtg)


Created with help of antigravity.