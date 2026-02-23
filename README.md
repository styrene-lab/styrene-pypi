# styrene

Meta-package for the Styrene mesh networking suite. Installs the full user-facing stack for [Reticulum](https://reticulum.network/) mesh networks.

## Install

```bash
pip install styrene           # full stack: daemon + TUI
pip install styrene[web]      # + FastAPI/Uvicorn HTTP API
pip install styrene[metrics]  # + Prometheus metrics
pip install styrene[yubikey]  # + YubiKey identity support
```

## What's Included

| Package | PyPI | Description |
|---------|------|-------------|
| [styrened](https://github.com/styrene-lab/styrened) | `pip install styrened` | Daemon, library, and TUI — RPC server, device discovery, auto-reply, mesh management UI |

## CLI Commands

After installing, two commands are available:

```bash
styrened   # Start the headless daemon
styrene    # Launch the terminal UI
```

## Individual Installation

Each component can be installed independently:

```bash
pip install styrened          # daemon/library only
pip install styrened[tui]     # daemon + TUI
```

## License

MIT
