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
| [styrened](https://github.com/styrene-lab/styrened) | `pip install styrened` | Headless daemon and shared library — RPC server, device discovery, auto-reply |
| [styrene-tui](https://github.com/styrene-lab/styrene-tui) | `pip install styrene-tui` | Terminal UI client for mesh management (Imperial CRT aesthetic) |

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
pip install styrene-tui       # TUI + styrened (as dependency)
```

## License

MIT
