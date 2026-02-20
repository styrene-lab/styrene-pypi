# Tech Debt: Post-Migration Cleanup

Remaining items from the styrene meta-package migration adversarial assessment.
None of these are blocking; all are cleanup/hardening.

## styrene-pypi

### Add CLAUDE.md
Minimal project instructions. Every other repo in the workspace has one.

### Add smoke test to publish workflow
`.github/workflows/publish.yml` builds and publishes without validation.
Add a step between build and publish:
```yaml
- name: Smoke test
  run: |
    pip install dist/*.whl
    python -c "import importlib.metadata; print(importlib.metadata.requires('styrene'))"
```

### Consider version pin strategy
Currently uses `>=` (loose). This is fine for now (matches ansible's approach),
but if styrened or styrene-tui ship a breaking major version, `pip install styrene`
could pull incompatible combinations. Revisit when any component hits 1.0.

## styrene-tui

### README code examples on main still reference old import paths
Lines 108, 239, 262, 274, 288, 311 use `from styrene.services.rpc_client`
and `from styrene.protocols.chat` — these are the TUI's own module paths
and may still be valid, but should be audited against the actual current
module structure. The feature/dashboard-mode branch likely has divergent
code that will resolve this on merge.

### Rebase feature/dashboard-mode onto main
The feature branch predates the distribution rename. After the rebase,
the branch will pick up the README/docs fixes and the pyproject.toml
rename. The README will have a merge conflict (both branches modified it)
that needs manual resolution.

## styrened

### Document meta-package in README
styrened's README only shows `pip install styrened`. Could add a one-liner:
"Or install the full stack: `pip install styrene`". Low priority since
`pip install styrened` still works and is the right choice for headless
deploys.
