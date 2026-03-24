---
description: Create YunoHost packaging for MTG
---

# Create YunoHost Packaging for MTG Proxy

Follow these instructions to create or maintain the YunoHost application package for the MTProto proxy (`mtg`).

## Context and References
When iterating on or rebuilding this YunoHost application, use the following resources as your ground truth reference:
- YunoHost Packaging Documentation: https://doc.yunohost.org/en/dev/packaging/
- YunoHost Example App structure: https://github.com/YunoHost/example_ynh
- MTG Main Repository: https://github.com/9seconds/mtg
- MTG Supported Config Options: https://github.com/9seconds/mtg/blob/master/example.config.toml

## Core Requirements
1. **Domain-Independence**: MTG operates as a proxy server mapping directly to a specific port. Do not implement NGINX mappings or depend on YunoHost domains (`type = "domain"`) inside `manifest.toml`. Treat it as a system-independent service.
2. **Release Artifacts**: Always build against the latest compiled binary published on https://github.com/9seconds/mtg/releases. Map `$YNH_ARCH` to the right asset (`amd64` to `linux-amd64`, `armhf` to `linux-arm-7`, `arm64` to `linux-arm64`, `i386` to `linux-386`).
3. **Installation Questions**: Parse configuration answers via YunoHost `manifest.toml`. You must ask for:
   - Proxy Port (type `string`, default: 3128)
   - Frontend Domain or MTProto Secret
   - DNS IP resolver
   - Prometheus metrics toggle
4. **Secret Generation**: If the user provides a frontend domain (eg. `google.com`) during install, use the binary utility `mtg generate-secret` to create a valid secret key automatically.
5. **System Integration**: Secure the setup using `ynh_system_user_create`, register the process using a `systemd` template (`ynh_add_systemd_config`), and enforce firewall access automatically (`yunohost firewall allow`).

## Routine Steps
If you are instructed to execute this workflow, you should:
1. Initialize the correct YunoHost folder structure (`manifest.toml`, `conf/`, `scripts/`).
2. Update the `manifest.toml` structure to declare necessary arguments.
3. Write/update the lifecycle bash scripts (`install`, `remove`, `upgrade`, `restore`, `backup`), verifying the proper usage of `/usr/share/yunohost/helpers` API.
4. Set up `conf/systemd.service` to start `mtg run` natively on boot.
5. Make sure all scripts are executable (`chmod +x`).
