# Scoped independent check — Riemann hypothesis Lean proof (Alpöge, 2026-11-20)

Checked by: Muse, for Domenic Lipoma. Date: 2026-11-25 (all fetches).
Question asked: does the statement proved in the published export match
Mathlib's `RiemannHypothesis` definition on the headline theorems?

## What was fetched first-hand

All three files below were fetched with the GitHub connector from the
`original` branch of Deicyde/riemann-hypothesis (now
leanprover-community/riemann-hypothesis), commit
`40e56bab026552e089d7afcfeff08d2defb9c005` — the unmodified copy of the
first publicly released version, per the repo README.

### 1. src/Statements.lean — file SHA 1cd1bce93344065936b2b392b23306254e0785ef

```lean
import Mathlib

def RiemannZetaZerosOnLine : Prop :=
  ∀ s : ℂ, riemannZeta s = 0 → (¬∃ n : ℕ, s = -2 * ((n : ℂ) + 1)) → s ≠ 1 → s.re = 1 / 2
def DirichletLNonvanishingRightOfHalf : Prop :=
  ∀ (N : ℕ) [NeZero N] (χ : DirichletCharacter ℂ N) (s : ℂ),
    1 / 2 < s.re → (χ ≠ 1 ∨ s ≠ 1) → DirichletCharacter.LFunction χ s ≠ 0
def DirichletLZerosOnLine : Prop :=
  ∀ (N : ℕ) [NeZero N] (χ : DirichletCharacter ℂ N) (s : ℂ),
    0 < s.re → s.re < 1 → DirichletCharacter.LFunction χ s = 0 → s.re = 1 / 2
def PrimitiveDirichletLZerosOnLine : Prop :=
  ∀ (N : ℕ) [NeZero N] (χ : DirichletCharacter ℂ N), χ.IsPrimitive →
    ∀ s : ℂ, 0 < s.re → s.re < 1 → DirichletCharacter.LFunction χ s = 0 → s.re = 1 / 2
```

16 lines, imports only Mathlib. This is the whole GRH statement file.

### 2. src/Main.lean — file SHA dbd5db70bc11b35f18fa5751216ab335321e7bfc

```lean
import Statements
import Supplements.Kernels.MainTheoremsAll

theorem riemannHypothesis : RiemannHypothesis := rhOfAll

theorem riemannZeta_eq_zero_re : RiemannZetaZerosOnLine := rhOfAll

theorem LFunction_ne_zero_of_half_lt_re : DirichletLNonvanishingRightOfHalf := allChi

theorem LFunction_eq_zero_re : DirichletLZerosOnLine := claimAll.2.1

theorem LFunction_eq_zero_re_of_isPrimitive : PrimitiveDirichletLZerosOnLine := critAll
```

Key fact: `theorem riemannHypothesis : RiemannHypothesis` — the theorem's
TYPE is the name `RiemannHypothesis`. That name is not defined anywhere in
this project; it is imported from Mathlib. (An independent Nov 20 inspection
by zharf.ai also found no local redefinition of `RiemannHypothesis` or of
`riemannZeta`.)

### 3. src/Development/AbelianVarietyTheory/Definitions/AutomorphicMembership/OverIx.lean — file SHA c5fd1ea624b8f2b29dc0f84e3261431f0e679c5c

Contains, verbatim:

```lean
abbrev GeoP : Type 1 := ∀ D : D7, Formalism.L2.Pj.Core D → DivX D → Prop
def geoOf (Q : ∀ D : D7, GlobalTheory.ShFam.KitClass D) : GeoP := fun D J X =>
  (∃ c : ℕ, 0 < c ∧ GlobalTheory.ShFam.IsGeoOf (Q D) J c X) ∧ GlobalTheory.ShFam.Pad.HasTrueSurf X
def anyGeometry : GeoP := fun _ _ _ => True
```

This confirms Nielsen's central claim FIRST-HAND from the original release:
`anyGeometry` is literally `fun _ _ _ => True` — a geometry predicate that
demands nothing — sitting six lines below `geoOf`, which demands a real
geometric witness (some positive `c` with `IsGeoOf` plus a true surface).
The same file's `OAt` structure takes a `Γ : GeoP` parameter and has a
`geo : Γ ...` field, so whichever predicate is passed in is what the
"geometry" field means. If `anyGeometry` is passed, that field is trivially
satisfied.

## Term-by-term comparison against the challenge statements

Reference: the five statements as quoted on Sutherland's verification page
(https://math.mit.edu/~drew/grh/, "below exactly as they appear in the
challenge file, which imports only Mathlib").

| # | Challenge statement (Sutherland) | Project source (fetched) | Match? |
|---|---|---|---|
| 1 | `theorem riemannHypothesis : RiemannHypothesis`, with `RiemannHypothesis` = Mathlib's def | Main.lean line 5: `theorem riemannHypothesis : RiemannHypothesis := rhOfAll` | YES — the type is Mathlib's name, not a local definition |
| 2 | `riemannZeta_eq_zero_re : ∀ s, riemannZeta s = 0 → (¬∃ n, s = -2 * ((n : ℂ) + 1)) → s ≠ 1 → s.re = 1 / 2` | Statements.lean `RiemannZetaZerosOnLine` — identical text | YES — identical |
| 3 | `LFunction_ne_zero_of_half_lt_re : ∀ N [NeZero N] χ s, 1/2 < s.re → (χ ≠ 1 ∨ s ≠ 1) → LFunction χ s ≠ 0` | Statements.lean `DirichletLNonvanishingRightOfHalf` — identical text | YES — identical |
| 4 | `LFunction_eq_zero_re : ∀ N [NeZero N] χ s, 0 < s.re → s.re < 1 → LFunction χ s = 0 → s.re = 1 / 2` | Statements.lean `DirichletLZerosOnLine` — identical text | YES — identical |
| 5 | `LFunction_eq_zero_re_of_isPrimitive : ∀ N [NeZero N] χ, χ.IsPrimitive → ∀ s, 0 < s.re → s.re < 1 → LFunction χ s = 0 → s.re = 1 / 2` | Statements.lean `PrimitiveDirichletLZerosOnLine` — identical text | YES — identical |

## Mathlib's definition itself

`RiemannHypothesis` in `Mathlib/NumberTheory/LSeries/RiemannZeta.lean`:

```lean
/-- A formal statement of the **Riemann hypothesis** – constructing a term of this type is worth a
million dollars. -/
def RiemannHypothesis : Prop :=
  ∀ (s : ℂ) (_ : riemannZeta s = 0) (_ : ¬∃ n : ℕ, s = -2 * (n + 1)) (_ : s ≠ 1), s.re = 1 / 2
```

This exact text is quoted identically by SEVEN independent sources:
Sutherland (MIT verification page), Rubinstein (Waterloo verification page),
the Hertaspace independent-verification repo (citing line 185 at the pinned
commit), the CocoSgt mirror (same), safeguard.sh, the arXiv paper by
Loeffler formalizing zeta/L-functions in Lean, and the Lean community blog
(which links the name to Mathlib's official docs page for the file, which I
opened: the file's docs page lists `riemannZeta`, the functional equation
and the trivial zeros).

LIMITATION, stated plainly: I could NOT pull the definition out of Mathlib's
own repository with the tools available here. The GitHub connector's tree
fetch fails on that path and its code search returns nothing for this repo.
So the definition text above rests on seven-way independent corroboration,
not on my own read of Mathlib's source. What I DID read first-hand is the
project side: Main.lean shows the theorem's type is the imported Mathlib
name, and Statements.lean shows the other four statements import only
Mathlib. That is the same comparison the comparator tools perform, and both
comparator and con-leche --compare confirm the match.

## Hashes cross-checked

| Item | Hash | Sources agreeing |
|---|---|---|
| Source archive lean.tar.gz (239,275,554 bytes, 14 parts) | sha256 `9631b4f020199e580ba86178cb56c6e9b09f690c2369a80dc4334aa93f49c7fc` | Sutherland; Rubinstein (downloaded twice, two machines); zharf.ai (independently downloaded and hashed) |
| Exported proof, unpacked (61,570,595,788 bytes) | sha256 `5ea74b91…244e` (full: 5ea74b912147c5c93cc2b6d70cc727cf908df2f62ac6a20480a3fa02f6be244e) | Sutherland (published export = sandboxed rebuild, byte-identical) |
| Challenge export, unpacked (350,862,970 bytes) | sha256 `bd484ac9…b2b9` | Sutherland (matches Deicyde CI) |
| Main.olean | sha256 `9146dfb4148e24d2252e04c50742f3e49dd126dfcc5006d10bf5f873ddf796ad` | Sutherland; Rubinstein |
| Lean / Mathlib pinned | Lean v4.33.1 (commit 819816b2); Mathlib tag v4.33.1 (commit 0df444a3) | Sutherland; Rubinstein |

## What was NOT checked (hard limits)

- The full 61.5 GB export was NOT downloaded. It needs ~70 GB disk and
  ~100 GB RAM to check; this sandbox has 78 GB free and 6 GB RAM.
- NO kernel replay was run. Lean's default kernel took ~48 h and the
  paranoid kernel ~72 h, single-threaded, on MIT hardware (peak memory
  82.6–98.8 GiB). Not feasible here. Do not claim otherwise.
- NO comparator run was performed here. Comparator v4.33.0's pass and
  con-leche/con-ron --compare acceptances are Sutherland's and Rubinstein's
  results, reported as theirs.
- Whether `anyGeometry` is actually ON the dependency path of
  `riemannHypothesis` was NOT checked. Rubinstein's dependency-closure run
  says the main theorem depends on 1,478,198 declarations and `sorryAx` is
  not among them; I did not check whether `anyGeometry` is among them.
- `geoDegenerate` and the `setDiv`/`hExpl6` height step from Nielsen's paper
  were NOT verified first-hand from source (only via Nielsen's paper and the
  DEV audit's quotes). The `anyGeometry` definition itself WAS verified
  first-hand (above).

## Verdict

- The statements MATCH. All five headline statements in the published
  release are exactly the statements in the Mathlib-only challenge file,
  and the headline theorem's type is Mathlib's own `RiemannHypothesis`.
  No discrepancy was found in the statements. No local redefinition of the
  hypothesis or of zeta was found in the files I read.
- The anyGeometry definition IS present in the original release, exactly as
  Nielsen claims. That is a real, first-hand finding, and it is a question
  about the proof's content, not about its statements: the kernels check
  that a term has its declared type; they do not check whether a definition
  called "geometry" carries geometric content. That question is unresolved
  as of 2026-11-25.
