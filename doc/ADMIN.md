## Configuration

The configuration file is at `/etc/mtg/mtg.toml`. Key settings:

- `secret` — The MTProto secret. Changing this requires restarting the service.
- `bind-to` — The port the proxy listens on.
- `[network] dns` — The DNS resolver used for IP resolution.
- `[stats.prometheus]` — Enable/disable the Prometheus metrics endpoint.

After editing the config file, restart the service:
```bash
sudo systemctl restart mtg
```

## Getting the connection link for Telegram

After installation, find your proxy settings:
```bash
sudo cat /etc/mtg/mtg.toml
```

Use the `secret` and your server's public IP + port to connect from Telegram:
**Settings → Data and Storage → Proxy Settings → Add Proxy → MTProto**
