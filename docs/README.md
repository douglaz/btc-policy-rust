# docs/

**The normative specification no longer lives here.** On 2026-09-09 it moved to its own
repository, `btc-policy-spec` (https://github.com/douglaz/btc-policy-spec), as a
language-neutral set with stable requirement identifiers and CI-run gates. This repository is
the Rust reference implementation of that specification.

Where each former document went:

| was here | now |
|---|---|
| `adr/0001` – `adr/0017` | `btc-policy-spec/docs/adr/` (same numbers, same files) |
| `THREAT-MODEL.md` | `12-security-requirements.md` |
| `PROTOCOL-VECTORS.md` | `08-wire-contract.md` (the vectors are executed by `tools/check_vectors.py`) |
| `SETUP-CEREMONY.md` | `09-manifest-config-ceremony.md` |
| `OPERATIONS-RUNBOOK.md`, `ROLLOUT-PLAN.md`, `UPGRADE-AND-ROTATION-POLICY.md`, `SBOM-AND-DEPENDENCY-POLICY.md` | `13-operations-and-rollout.md` |
| `../CONTEXT.md` (the glossary) | `CONTEXT.md` there; the copy here is a pointer |

The ADR numbers cited from code comments (`ADR-0012`, `ADR-0013 §4`, …) resolve in the spec
repository unchanged.

What stays here, as **implementation history** and not as specification:

- `DESIGN.md` — the July-2026 design of record, with dated supersession notes; not authoritative.
- `V0-PLAN.md` — the v0 build-order record; every task is done.
- `TEST-PLAN.md` — the reference implementation's own test plan, including the sixteen harness
  scenarios and the CI legs.
- `SIGNET-SPEND-RECORD.md` — the one real public-chain spend, 2026-07-27.
- `../IDEA.md` — the pre-project survey.

A requirement identifier in a commit message, a bead, or a code comment (`SPN-5`, `DUR-8`,
`WIR-27`) refers to the spec repository.
