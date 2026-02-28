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

Extract and move to your PATH:

```bash
tar xzf wigwam_*.tar.gz
sudo mv wigwam /usr/local/bin/
```

## Requirements

- [tmux](https://github.com/tmux/tmux) must be installed and a session must be running

## Usage

Start wigwam:

```bash
wigwam
```

This attaches to your first tmux session and starts a web server on `http://localhost:8080`. Open that URL in a browser to view your terminal.

### Options

```
  -t string          tmux target session (default: first session)
  -port int          server port (default 8080)
  -password string   auth password (default: auto-generated token)
  -local             run in local-only mode (no relay connection)
  -tunnel            expose via Cloudflare quick tunnel (local mode only)
  -tls-cert string   path to TLS certificate file
  -tls-key string    path to TLS private key file
  -version           print version and exit
```

### Examples

```bash
# Attach to a specific session
wigwam -t mysession

# Use a custom port and password
wigwam -port 3000 -password secret

# Local only with a Cloudflare tunnel for remote access
wigwam -local -tunnel
```

## License

MIT
