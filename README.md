# btc-policy

The Rust **reference implementation** of a self-hosted Bitcoin soft vault: a user hardware key
plus a `t`-of-`n` federation of policy-enforcing signer nodes (default 3-of-5), with a
timelocked 2-of-3 recovery path and a silent duress response. Every node holds one multisig key
and one policy engine, independently validates the exact PSBT it is asked to sign, and refuses
anything outside the vault's immutable policy. Theft needs the user key AND a quorum of
compromised nodes. It runs on today's consensus rules — standard P2WSH Miniscript, no covenants,
and no covenant upgrade path is planned.

## The specification

The language-neutral specification lives in its own repository,
**[btc-policy-spec](https://github.com/douglaz/btc-policy-spec)**: seventeen numbered
requirement documents with stable identifiers, the glossary, the ADRs, and gates that execute
the wire contract's byte vectors on every push. Read its `executive-summary.md` first and its
`16-open-findings.md` before building anything. This repository is evidence for that
specification, not authority over it: where the two disagree, one is wrong and the finding goes
there.

What ships here: the node daemon (`vault-node`), the coordinator CLI (`btc-vault`: setup
ceremony, three regtest demos, the adversarial `attack` harness, a signet spend driver), and the
pure policy crate (`policy-core`). The operator spend, refresh, pending, and recovery commands
are in progress; see the beads under `.beads/` and finding `F10` in the spec.

`docs/` here holds implementation history only — the July-2026 design of record, the v0 build
plan, this repository's test plan, and the signet spend record. `docs/README.md` maps each
former document to its new home.

## Try it

```
nix develop -c cargo run -p vault-cli -- demo theft-refused
```

needs a local `bitcoind`. `demo first-light`, `demo recovery-drill`, and `attack all` are the
other gates CI runs on every push (`.github/workflows/ci.yml`); `docs/TEST-PLAN.md` describes
them.

## Reference repositories

Shallow clones of prior art live under `repos/` (Liana, Specter, libnunchuk, gdk, Keep, cb-mpc,
bdk, rust-miniscript, walletrs, sigvault-desktop, revaultd, simple-ctv-vault, mccv, HWI). They are
reading material for `IDEA.md`; none is a dependency of this workspace.
