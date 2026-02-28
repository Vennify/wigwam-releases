# wigwam

Access your tmux sessions from the browser.

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

# Attach to a specific tmux session
wigwam -t mysession
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

## Options

```
  -t string          tmux target session (default: first session)
  -port int          server port (default 8080)
  -local             local-only mode (no relay)
  -tunnel            expose via Cloudflare quick tunnel (local mode only)
  -password string   set a custom auth password
  -tls-cert string   path to TLS certificate file
  -tls-key string    path to TLS private key file
  -version           print version and exit
```

## License

MIT
