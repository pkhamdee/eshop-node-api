# eshop-node-api

eShop's image service: Node 24 + Express + TypeScript (run directly by Node), serving Product and Lot photos from the SMB share through `smbclient`. One of eShop's service repositories (ADR 0009). The system lives in `pkhamdee/eshop-infra`, cloned
beside this one as `../eshop-infra` (its `scripts/clone-all.sh` clones this one): the glossary, ADRs, the one issue
tracker, deploy manifests, the smoke test, the gates and releases.

## Commands (Node 24)

- `npm ci`, then `npm run dev` (folder store in `.local-share`, port 8081), `npm run lint` (oxlint and `tsc`),
  `npm test` (`node --test`; quote globs in zsh: `node --test 'test/**/*.test.ts'`).
- The whole system around it, built from your clones: `../eshop-infra/scripts/gates/temporary-copy.sh build`, then
  `up` (`../eshop-infra/docs/setup.md`, "Developing").

## Where things are

- Domain terms: `../eshop-infra/GLOSSARY.md`; decisions: `../eshop-infra/docs/adr/`. Skills that mention `GLOSSARY.md`
  or `docs/adr/` mean those.
- Conventions for this code: `docs/conventions.md`.
- How a merge here reaches dev, QA and prod: `../eshop-infra/docs/git-workflow.md`, "Service repositories".

## Rules

- Issues are in `pkhamdee/eshop-infra`: reference them as `pkhamdee/eshop-infra#N` in commits and PRs.
- Every merge must work with the other services' `main` (the temporary copy checks it): a change across services
  ships expand-then-contract, never as two PRs that only work together.
- Before a step touching secrets, repo settings or a PR merge, read "Human-only steps" in
  `../eshop-infra/docs/agents/conventions.md`.
