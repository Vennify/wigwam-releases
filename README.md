# wigwam

Access your tmux sessions from the browser — or your phone.

Wigwam runs a lightweight daemon alongside tmux and serves a web UI over WebSocket. View and interact with your terminal from any device — your phone, tablet, or another machine.

## Install

### Homebrew (macOS & Linux)

```bash
brew install Vennify/wigwam/wigwam
```

### Download binary

Grab the latest release for your platform from [Releases](https://github.com/Vennify/wigwam-releases/releases).

```bash
tar xzf wigwam_*.tar.gz
sudo mv wigwam /usr/local/bin/
```

## Requirements

- [tmux](https://github.com/tmux/tmux) must be installed and a session must be running

## Quick Start

```bash
wigwam
```

On first run, your browser opens to sign in. Once authenticated, you get a shareable URL to your terminal session. The token is saved so future runs connect automatically.

That's it — open the URL on any device to view and interact with your tmux session.

## Modes

### Remote (default)

By default, wigwam connects through a relay server. On first run it opens your browser to authenticate, then gives you a public URL you can access from anywhere.

```bash
# Start wigwam (opens browser to sign in on first run)
wigwam
```

### Local

For local-only use, pass `-local`. The web UI is served on `localhost` and nothing leaves your machine.

```bash
# Serve on localhost only
wigwam -local

# Serve on localhost with a temporary Cloudflare tunnel for remote access
wigwam -local -tunnel
```

The `-tunnel` flag generates a random public Cloudflare URL — useful for quick sharing without an account. Requires [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/).

## CLI Commands

```bash
wigwam              # start the daemon
wigwam status       # show daemon status, relay connection, session count
wigwam login        # authenticate with the relay (skips if already connected)
wigwam logout       # disconnect from relay and clear saved tokens
wigwam key          # show encryption key, file path, and QR code image path
wigwam service install   # install as a system service (systemd/launchd)
wigwam service uninstall # remove the system service
wigwam hooks install     # install Claude Code notification hooks
wigwam version      # print version
```

## Encryption

All traffic through the relay is end-to-end encrypted by default. The daemon generates an AES-256 session key on first run and a QR code you can scan from the mobile app.

```bash
# Show your encryption key and QR image path
wigwam key

# Modes: off, flex, secure, any (default: any)
wigwam -crypto secure       # require encryption — reject unencrypted clients
wigwam -crypto off          # disable encryption entirely

# Rotate the encryption key
wigwam -crypto-rotate
```

## Options

```
  -port int            server port (default 8080)
  -local               local-only mode (no relay)
  -tunnel              expose via Cloudflare quick tunnel (local mode only)
  -password string     set a custom auth password
  -crypto string       encryption mode: off, flex, secure, any (default "any")
  -crypto-rotate       generate a new encryption key
  -auto-update         automatically download and install daemon updates
  -tls-cert string     path to TLS certificate file
  -tls-key string      path to TLS private key file
  -relay-url string    relay server URL
  -relay-token string  auth token for relay (or set WIGWAM_RELAY_TOKEN)
```

## Mobile App

Wigwam has companion apps for iOS and Android. Scan the QR code from `wigwam key` to pair your device.

## License

MIT
