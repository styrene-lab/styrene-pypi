# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A **PyPI meta-package** (`pip install styrene`) that installs the full Styrene mesh networking stack. There is no source code — just `pyproject.toml` declaring a dependency on `styrened[tui]`, plus optional extras (`[web]`, `[metrics]`, `[yubikey]`) that pass through to styrened's own extras.

## Build and Publish

```bash
# Build sdist + wheel
pip install build
python -m build

# Smoke test the built wheel
pip install dist/*.whl
python -c "import importlib.metadata; print(importlib.metadata.requires('styrene'))"
```

Publishing happens via GitHub Actions (`.github/workflows/publish.yml`) on release creation or manual dispatch. Uses PyPI trusted publishing (OIDC, no API token).

## Version Management

Version lives in `pyproject.toml` `[project] version`. Bump it, tag, create a GitHub release — the workflow handles the rest. Dependency pins use `>=` (loose) intentionally; tighten if a component ships a breaking major version.

## Relationship to Other Repos

This package owns the `styrene` name on PyPI. The actual code lives in:
- **styrened** (`styrene-lab/styrened`) — daemon + library + TUI (via `[tui]` extra)
