# eshop-node-api

eShop's image service: Node 24 + Express + TypeScript (run directly by Node), serving Product and Lot photos from the SMB share through `smbclient`. One of eShop's service repositories (ADR 0009). The system lives in `pkhamdee/modernapp`, cloned
beside this one as `../modernapp` (its `scripts/clone-all.sh` clones this one): the glossary, ADRs, the one issue
tracker, deploy manifests, the smoke test, the gates and releases.

## Commands (Node 24)

- `npm ci`, then `npm run dev` (folder store in `.local-share`, port 8081), `npm run lint` (oxlint and `tsc`),
  `npm test` (`node --test`; quote globs in zsh: `node --test 'test/**/*.test.ts'`).
- The whole system around it, built from your clones: `../modernapp/scripts/gates/temporary-copy.sh build`, then
  `up` (`../modernapp/docs/setup.md`, "Developing").

## Where things are

- Domain terms: `../modernapp/GLOSSARY.md`; decisions: `../modernapp/docs/adr/`. Skills that mention `GLOSSARY.md`
  or `docs/adr/` mean those.
- Conventions for this code: `docs/conventions.md`.
- How a merge here reaches dev, QA and prod: `../modernapp/docs/git-workflow.md`, "Service repositories".

## Rules

- Issues are in `pkhamdee/modernapp`: reference them as `pkhamdee/modernapp#N` in commits and PRs.
- Every merge must work with the other services' `main` (the temporary copy checks it): a change across services
  ships expand-then-contract, never as two PRs that only work together.
- Before a step touching secrets, repo settings or a PR merge, read "Human-only steps" in
  `../modernapp/docs/agents/conventions.md`.
