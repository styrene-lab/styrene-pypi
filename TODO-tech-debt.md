# Tech Debt: Post-Migration Cleanup

Remaining items from the styrene meta-package migration adversarial assessment.
None of these are blocking; all are cleanup/hardening.

## styrene-pypi

### Version sync workflow
`.github/workflows/sync-version.yml` polls PyPI every 6 hours for new stable
styrened releases. Manual override via `workflow_dispatch` with optional version
input. Future: add `repository_dispatch` trigger from styrened's Argo
release-build.yaml for near-instant sync (schedule polling remains as safety net).

**One-time setup required:**
- Add `sync-version.yml` as a second trusted publisher at
  pypi.org/manage/project/styrene/settings/publishing/
- Ensure `pypi` environment exists on `styrene-lab/styrene-pypi`

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
