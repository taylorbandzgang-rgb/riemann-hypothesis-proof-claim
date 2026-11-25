# The Riemann Hypothesis Proof Claim: What Was Claimed, What Was Checked, and What the Proof Says (So Far)

**Domenic Lipoma**, with Muse as research assistant · 25 November 2026

A human-readable reconstruction of what is publicly known about the claimed proof of the
Riemann hypothesis announced on 20 November 2026 by Levent Alpöge (built with Claude,
formalized in Lean), plus a scoped independent check the author ran himself.

## Read the paper

- [`paper.html`](paper.html) — the full 16-page paper as a single HTML file (open in any browser)
- The PDF version of the paper is distributed with the announcement post; it can be added here
  later with a web upload, since this push route only carries text files.

## What the paper finds

- **The statements match.** All five headline theorems in the published release are exactly
  the statements in the Mathlib-only challenge file, and the headline theorem's type is
  Mathlib's own `RiemannHypothesis`, not a local redefinition. Checked first-hand against the
  original release (commit `40e56bab026552e089d7afcfeff08d2defb9c005`).
- **One verified, unresolved question.** The definition `def anyGeometry : GeoP := fun _ _ _ => True`
  is literally in the original release — a geometry predicate that demands nothing. Whether it
  sits on the dependency path of the headline theorem was not checked here, and kernels check
  types, not intended content.
- **The ideas, as far as they are publicly known.** A Stepanov descendant: chaining theta lifts
  to manufacture multiplicity over the integers (chain length √X for a von Mangoldt sum of
  length X), with the Guinand–Weil explicit formula supplying the sign. How the chain actually
  produces the zero-free region is **not yet publicly explained**, and the paper says so rather
  than inventing a mechanism.
- **What confirmation still needs:** the final lake-comparator stage, human peer review (no
  human-readable proof exists yet to review), the anyGeometry question, and Clay's own process.

## Honest scope

This is **not** a peer-reviewed verification and does **not** reproduce the proof (about
17.4 million lines of Lean across ~175,187 files). No kernel replay was run here — that took
48–72 hours on university hardware. The scoped check covered the five headline statements
and one definition, nothing more. Section 6 of the paper is the author's own commentary in
his own framework (TAEFT), clearly marked, and is not part of the mathematics.

## Working notes

The full check trail is in [`notes/`](notes/):

- [`notes/SCOPED-CHECK.md`](notes/SCOPED-CHECK.md) — the statement comparison, hashes, and hard limits
- [`notes/IDEAS.md`](notes/IDEAS.md) — the proof's ideas as publicly known, with gaps marked
- [`notes/SOURCES.md`](notes/SOURCES.md) — every source, with URLs and access dates

## Related work

- [riemann-zero-check](https://github.com/taylorbandzgang-rgb/riemann-zero-check) — the author's
  independent numerical check of the first 1,000 zeta zeros (mpmath, 30-digit precision,
  50-digit cross-check), published 24 November 2026.
