# Conventions for eshop-node-api

What the code does not tell you at a glance. Moved here from pkhamdee/eshop-infra's `docs/agents/conventions.md` when
eshop-node-api got its own repository (ADR 0009); the system-wide conventions (local environment, deploy, human-only
steps) are still there.

- Node 24 runs `src/*.ts` directly (type stripping): no build step, imports end in `.ts`, `erasableSyntaxOnly`,
  so no enums or parameter properties.
- Ports as interfaces (`ImageStore`) with adapters (`folderImageStore`, `smbImageStore`). Tests (`node --test`)
  start the real service on port 0 via `test/harness.ts` and assert on HTTP only; `startSmbService()` puts
  `test/fake-smbclient/` (an ESM script: use `import`) on `PATH`. Extend that fake when the adapter sends a new
  smbclient command.
- SMB goes through the `smbclient` binary because pure-JS SMB libraries need NTLMv1/MD4. Use `ls`, not `allinfo`,
  to test existence: Samba without VSS answers `allinfo` with `NT_STATUS_INVALID_DEVICE_REQUEST`.
- `/internal/images/...` is never routed by the Gateway; through the Gateway that path returns the SPA's
  `index.html` (200 text/html), so check the content type when verifying image privacy.
- The share itself (mock Samba, one share per environment) is deployed by pkhamdee/eshop-infra
  (`../eshop-infra/deploy/thirdparty/samba/`).
