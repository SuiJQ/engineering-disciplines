# Engineering Disciplines

A collection of **reusable software-engineering disciplines** distilled from hard-won lessons on a long-lived, high-stakes project (a party-government document drafting harness). Each entry is a self-contained, cross-project methodology — not tied to any specific codebase — for the kind of problems that quietly eat engineering time.

Packaged as an **instruction-style agent skill**: a `SKILL.md` index maps common situations to the right reference, and each reference carries concrete steps, failure modes, and provenance.

## What's inside

**`references/procedure/`** — runbooks with ordered steps (施工法):

| Entry | Use when… |
|---|---|
| `unwired-parts-audit-runbook` | Hunting "parts are written but never wired up" defects |
| `wiring-defects-need-assembly-root-observation` | A parameter gets dropped mid-assembly while tests stay green |
| `invariants-as-executable-assertions` | A rule lives in docs, enforced only by human discipline |
| `audit-effort-goes-to-checking-promises` | Auditing a mature module — check promises, not just code |
| `land-decisions-to-single-authority` | Decisions exist only in chat/commits, with unresolvable IDs |
| `large-file-edit-recovery-discipline` | Doing structural moves / regex rewrites over big files |
| `auto-fix-must-be-visible` | Auto-fixers / gates mutate the thing they're checking |
| `falsification-backup-taken-before-edit` | Running falsification experiments on criteria |
| `bind-commitment-to-artifact` | Output stops at "I'll write it now." with no file produced |
| `four-perspective-ab-axis-verification` | End-to-end verification needing variable separation |
| `hard-constraint-validation-state-update-fix` | A gate fires too early because state isn't populated yet |

**`references/wiki/`** — distilled experience / judgment rules (经验规则):

| Entry | Use when… |
|---|---|
| `criteria-credibility-three-failure-modes` | A criterion is green but untrusted (miswritten / not running / missed scope) |
| `criteria-check-provenance-not-shape` | A criterion checks the shape of a result, not where it came from |
| `criteria-must-assert-behavior-differences` | A criterion must be falsifiable and assert observable behavior |
| `cjk-blind-tests-falsely-green` | Chinese-related matching is tested only on ASCII |
| `docs-and-ledgers-are-not-source-of-truth` | A "source of truth" STATUS file is lying |
| `idempotency-identity-and-skip-readback` | Idempotency/resume: ledger ID and lookup ID are each built by hand |
| `three-layers-intent-tool-name-program-wiring` | A capability needs intent + tool name + wiring to actually happen |
| `truncate-by-token-budget-not-count` | Truncation caps must be expressed in token budget, not item count |
| `historical-defect-precise-reproduction-identification` | Symptoms match a past incident exactly — likely a recurrence |
| `memory-gate-zero-destructive-intro` | Adding a new state field to an existing system |
| `pytest-tests-package-import-fix` | pytest `ModuleNotFoundError: No module named 'tests'` |

## Usage as an agent skill

1. Match the current situation against the index in `SKILL.md`.
2. Open the referenced entry under `references/procedure/` or `references/wiki/`.
3. Follow the `Steps` (for runbooks) or adopt the judgment rules (for experience entries). Each entry documents its failure modes and the evidence it came from.

## License

GPL-3.0. These disciplines were distilled from the development experience of the [gov-document-harness](https://github.com/SuiJQ/gov-document-harness) project; the content is provided as methodology documentation rather than product code.