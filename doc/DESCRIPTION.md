# MTG - MTProto proxy for Telegram

MTG is a highly-opinionated, standalone MTProto proxy for Telegram. It provides a fast, lightweight proxy that helps bypass network restrictions by using domain fronting.

## Features

- **Domain fronting**: Auto-generates a secret tied to a real HTTPS domain (e.g. `google.com`), making the traffic look like normal HTTPS
- **Automatic IP blocklists**: Downloads and applies FireHOL-based blocklists to filter malicious traffic
- **Anti-replay protection**: Prevents replay attacks via built-in caching
- **Prometheus metrics**: Optional `/metrics` endpoint for monitoring
- **Minimal footprint**: Single binary, no runtime dependencies

## How it works

Once installed, the proxy runs on the chosen port. Users connect from Telegram using the generated secret. Traffic is tunneled through an HTTPS-looking connection to Telegram's data centers, bypassing deep-packet inspection.
