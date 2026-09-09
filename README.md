# btc-policy

A self-hosted Bitcoin **soft vault**, in Rust: a user hardware key plus a t-of-n federation of
policy-enforcing signer nodes (default 3-of-5), with a timelocked 2-of-3 recovery path. Every
node holds one multisig key and one policy engine, independently validates the exact PSBT it is
asked to sign, and refuses anything outside the vault's immutable policy. Theft needs the user key
AND a quorum of compromised nodes. It runs on today's consensus rules — standard P2WSH Miniscript,
no covenants, and no covenant upgrade path is planned.

What ships today: the node daemon (`vault-node`), the coordinator CLI (`btc-vault`: setup
ceremony, three regtest demos, the adversarial `attack` harness, and a signet spend driver), and
the pure policy crate (`policy-core`). The operator spend, refresh, pending, and recovery commands
are in progress; see the beads under `.beads/`.

## Where the spec lives

- [`CONTEXT.md`](CONTEXT.md) — the glossary; every term below is defined there.
- [`docs/adr/0012`](docs/adr/0012-model-b-spend-and-duress-architecture.md) and
  [`docs/adr/0013`](docs/adr/0013-concrete-protocol-schemas.md) — the authoritative spend-path,
  duress, and wire/config/manifest spec. The other ADRs record the decisions that led there.
- [`docs/THREAT-MODEL.md`](docs/THREAT-MODEL.md), [`docs/PROTOCOL-VECTORS.md`](docs/PROTOCOL-VECTORS.md)
  (frozen byte vectors, pinned by tests), [`docs/OPERATIONS-RUNBOOK.md`](docs/OPERATIONS-RUNBOOK.md),
  [`docs/SETUP-CEREMONY.md`](docs/SETUP-CEREMONY.md), [`docs/ROLLOUT-PLAN.md`](docs/ROLLOUT-PLAN.md).
- [`docs/DESIGN.md`](docs/DESIGN.md) is the July-2026 design of record, kept with dated
  supersession notes; where it disagrees with the ADRs, the ADRs win.
  [`IDEA.md`](IDEA.md) is the pre-project survey and is historical only.

## Try it

```
nix develop -c cargo run -p vault-cli -- demo theft-refused
```

needs a local `bitcoind`. `demo first-light`, `demo recovery-drill`, and `attack all` are the
other gates CI runs on every push (`.github/workflows/ci.yml`); `docs/TEST-PLAN.md` describes them.

## Reference repositories

Shallow clones of prior art live under `repos/` (Liana, Specter, libnunchuk, gdk, Keep, cb-mpc,
bdk, rust-miniscript, walletrs, sigvault-desktop, revaultd, simple-ctv-vault, mccv, HWI). They are
reading material for `IDEA.md`; none is a dependency of this workspace.
