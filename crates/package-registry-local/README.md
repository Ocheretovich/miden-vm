# miden-package-registry-local

Local filesystem-backed registry and CLI for publishing and inspecting Miden packages.

The local registry stores:

- index metadata under `$MIDEN_SYSROOT/etc/registry/index.toml`
- package artifacts under `$MIDEN_SYSROOT/lib/<digest>.masp`

The CLI currently supports:

- `publish <path>` to validate and publish an assembled `.masp`
- `list` to show all indexed packages and versions
- `show <package>` to inspect all indexed versions for a package

Publishing enforces the first-cut registry rules:

- each package semantic version maps to at most one canonical published artifact in the local
  registry
- the package must embed semantic version metadata
- every dependency in the package manifest must already exist in the registry by exact digest
- dependency requirements are persisted as exact resolved digests, not the original declared source
  requirements
