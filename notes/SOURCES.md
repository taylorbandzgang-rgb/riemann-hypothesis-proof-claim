# Source log — Riemann hypothesis proof claim

Every substantive claim in the paper traces to one of these sources.
Accessed 2026-11-25 (all times UTC) unless noted. No source, no claim.

## Primary sources (the claim and the code)

| # | Source | URL | Accessed | What it establishes |
|---|---|---|---|---|
| S1 | Alpöge, "Remark" (4-page announcement PDF) | https://alpo.ge/remark.pdf | 2026-11-25 03:32 | The claim itself; the proof sketch (Stepanov descendant, theta-lift chain length √X, 20-step timeline Oct 6–Nov 16); "250,000+ pages was a joke" footnote context; Alpöge's own caveats |
| S2 | Deicyde/riemann-hypothesis, `original` branch, commit 40e56bab026552e089d7afcfeff08d2defb9c005 | https://github.com/Deicyde/riemann-hypothesis | 2026-11-25 03:32–03:35 | First-hand fetch: src/Main.lean, src/Statements.lean, src/Development/.../OverIx.lean (see SCOPED-CHECK.md for SHAs) |
| S3 | Lean community blog — "Lean verification of the Riemann Hypothesis" (joint statement, Lean FRO + Mathlib Initiative, 2026-11-21 13:55 UTC) | https://leanprover-community.github.io/blog/ | 2026-11-25 03:34 | "Full confidence"; "We hereby certify that both the statement and the proof of the Riemann Hypothesis are correct"; the four Xena criteria |
| S4 | Sutherland (MIT), "RH Lean proof: verification files", last updated 2026-11-25 22:05 UTC | https://math.mit.edu/~drew/grh/ | 2026-11-25 19:33 | Full check table; five statements verbatim; Mathlib def verbatim; hashes; lake comparator FINISHED — "Your solution is okay!", exit 0 at 21:49 UTC 25 Nov, all checks finished, nothing pending; shorter Lean proof published 25 Nov (separate page, not reviewed); Robin1984 arithmetic consequences; caveats |
| S5 | Rubinstein (Waterloo), "GRH Lean Check", all checks complete 2026-11-21 10:10 UTC | https://mrubinst.github.io/grh-lean-verification/ | 2026-11-25 03:32 | Independent verification: statements read by hand; dependency closure 1,478,198 declarations, no sorryAx; top-level structure (rhOfAll → allChi → everyCharacter); CritLine.lean functional-equation step read by hand |
| S6 | Mathlib docs — Mathlib.NumberTheory.LSeries.RiemannZeta | https://leanprover-community.github.io/mathlib4_docs/Mathlib/NumberTheory/LSeries/RiemannZeta.html#RiemannHypothesis | 2026-11-25 03:34 | The file exists in Mathlib's official docs; documents riemannZeta, the functional equation, trivial zeros (definition text itself corroborated via S4/S5 + others, see SCOPED-CHECK.md) |

## The critique

| # | Source | URL | Accessed | What it establishes |
|---|---|---|---|---|
| C1 | Nielsen, J. L., "The Invalidity of Alpöge's Proof of the Riemann Hypothesis" (PhilArchive, 2026-11-20/21) | https://philarchive.org/archive/NIEIOT-2 | via search 2026-11-25 03:32 | anyGeometry := True; geoDegenerate; setDiv/hExpl6 height by rfl; "manufactured witness" argument; status: unresolved, not peer-reviewed |
| C2 | DEV audit (frankchu), "GRH proof's geometry is `fun _ _ _ => True`, in 24 files" | https://dev.to/frankchu/grh-proofs-geometry-is-fun-true-in-24-files-2n2b | via search 2026-11-25 03:32 | Independent walk of the tarball confirming the anyGeometry definition verbatim; GeoCl closure; notes Nielsen also filed against Masullo the same day |

## Reputable coverage (for context, reactions, and what is still unknown)

| # | Source | URL | Accessed |
|---|---|---|---|
| R1 | Scientific American, Howlett (2026-11-20) + Moskowitz (2026-11-21, updated) — claim and confirmation | https://www.scientificamerican.com/article/anthropic-mathematician-claims-to-prove-riemann-hypothesis-most-famous-problem-in-all-of-math/ and https://www.scientificamerican.com/article/the-ai-riemann-hypothesis-proof-is-almost-certainly-true-independent-mathematicians-attest/ | via search 2026-11-24 |
| R2 | Wikipedia, "Alpöge proof of the Riemann hypothesis" (crawled 2026-11-24 01:14 UTC) | https://en.wikipedia.org/wiki/Alp%C3%B6ge_proof_of_the_Riemann_hypothesis | 2026-11-25 03:32 |
| R3 | explainx.ai tracker, "Riemann Hypothesis Proof Claim: Claimed vs Verified" (latest update 2026-11-24 07:00 UTC) | https://explainx.ai/blog/levent-alpoge-anthropic-riemann-hypothesis-claude-lean-proof-claimed-vs-verified-2026 | 2026-11-25 03:34 |
| R4 | Quanta Magazine, Kakaes (2026-11-20) — verification race; Masullo human draft | via Wikipedia refs | 2026-11-25 |
| R5 | Nature, Castelvecchi (2026-11-20) — reactions | via Wikipedia refs | 2026-11-25 |
| R6 | Wall Street Journal (2026-11-23) — claim, certification | https://www.wsj.com/tech/ai/anthropic-mathematician-says-claude-has-solved-the-most-famous-problem-in-math-9361920b | via search 2026-11-24 |

## The dependency audits (added 2026-11-25)

| # | Source | URL | Accessed | What it establishes |
|---|---|---|---|---|
| A1 | Riemann Hypothesis Rosetta — "Where `anyGeometry` occurs in the checked RH proof" | https://github.com/dial481/riemann-hypothesis-rosetta/blob/main/results/anygeometry.md | 2026-11-25 04:23 UTC | anyGeometry eight dependency edges below riemannHypothesis on a kernel-checked path; strict geometry (geoOf, IsGeoOf, HasTrueSurf) has zero kernel presence; 29 direct referrers, 48 dependents |
| A2 | Rosetta — anygeometry-path.tsv (edge-by-edge data) | https://github.com/dial481/riemann-hypothesis-rosetta/blob/main/results/anygeometry-path.tsv | 2026-11-25 04:23 UTC | The eight value edges, with source file and line for each step; path is shortest |
| A3 | James Shore — rh-proof-dependencies, dataset v0.2.1 | https://github.com/james-shore/rh-proof-dependencies | 2026-11-25 04:23 UTC | Kernel edge table the Rosetta path is checked against |
| A4 | Harry Tong — rh-verification audit | https://github.com/harrytong/rh-verification/blob/main/stage1/code/RH_critics_dependency_findings.md | via Rosetta 2026-11-25 | Independent confirmation: anyGeometry in all five compiled dependency closures, second eight-edge path |
| A5 | "Is the Riemann Hypothesis really solved?" FAQ | https://riemannhypothesissolved.com/faq/ | via search 2026-11-24 | Bailey (MathOverflow) and Bloom (X): definitions irrelevant if the term has the correct type; Alpöge (24 Nov 2026, X): "It literally checked out days ago?" |
| A6 | Zeng, Z. — Independent audit of the "anyGeometry := True" objection (ArtificialZeng/Riemann-hypothesis-Auditing, PR #1, 23 Nov 2026) | https://github.com/ArtificialZeng/Riemann-hypothesis-Auditing/pull/1 | 2026-11-25 13:40 UTC | Verdict "the objection does not hold"; geometry slot write-only; 30 of 1,468,418 declarations depend on anyGeometry; hygiene counts; conescan + con-leche evidence |
| A7 | explainx.ai tracker, "Riemann Hypothesis Proof Claim: Claimed vs Verified" (update of 25 Nov 2026) | https://explainx.ai/blog/levent-alpoge-anthropic-riemann-hypothesis-claude-lean-proof-claimed-vs-verified-2026 | 2026-11-25 | Adriazola 287-page manuscript (24 Nov 2026): working document, no correctness guarantee, §19 open hypotheses, §17.4.3 K1 bound uncertified |

## Domenic's own work (cited in the paper)

| # | Source | URL |
|---|---|---|
| D1 | Domenic Lipoma, independent numerical check of the first 1,000 zeta zeros (mpmath, 30-digit, 50-digit cross-check) | https://github.com/taylorbandzgang-rgb/riemann-zero-check |
| D2 | Domenic Lipoma, "The Eternal Fluctuation Theorem — Toy Effective Field Theory in a Toroidal Astroid Universe, Draft v1.2" (TAEFT white paper) | ~/workspace/own-brain/corpus/taeft-white-paper.txt (local file; Gemini share, fetched 2026-11-16) |

## Notes on conflicts

- Press tone vs. verification tracker: Scientific American's updated headline
  ("the proof is true, independent mathematicians confirm") is stronger than
  the trackers. The explainx tracker and Sutherland's page are more careful:
  kernels accept, comparator passes, but the final lake-comparator stage was
  still running and the anyGeometry question is open. The paper follows the
  tracker, not the headline.
- The "250,000 pages" figure: Alpöge's remark.pdf footnote jokes about it;
  on 2026-11-23 he said on X it was a joke. No such document exists.
- Masullo's rival draft (~940 pages, posted by Ravi Vakil 2026-11-20) is a
  separate, unfinished, unverified human manuscript. It is not the Lean proof
  and is not treated as one anywhere in the paper.
