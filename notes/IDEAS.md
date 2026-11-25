# The ideas of the proof — as far as they are publicly known (2026-11-25)

Source: Alpöge's remark.pdf (S1) unless noted. Where the public record
does not explain something, it is marked NOT YET PUBLICLY EXPLAINED.
Nothing here is a guess presented as the proof's method.

## The problem in one paragraph

RH says every nontrivial zero of the Riemann zeta function ζ(s) has real
part exactly 1/2. The zeros control the primes: RH is equivalent to the
sharpest possible error term in the prime number theorem,
π(x) = li(x) + O(√x log x). The Generalized RH (GRH) says the same for
every Dirichlet L-function L(s, χ). The checked proof covers Dirichlet
L-functions only — not Dedekind zeta functions, not Hecke or automorphic
L-functions in general (S4, Scope section).

## The top-level shape (Rubinstein, S5 — read by hand)

```
Main.riemannHypothesis
 └ rhOfAll        = Formalism.VW.rh_of_every allChi
    └ allChi      = UpperTheory.FinalTheorems.everyCharacter
                    (no zeros of L(s,χ) for Re s > 1/2)
       └ everyCharacter_of_row ... (175,187 modules underneath)
```

So the proof's spine is: prove no L-function zero lies to the RIGHT of the
critical line (Re s > 1/2), then use the functional equation — applied to
χ⁻¹ at 1 − s — to fold that into "every zero in the strip lies ON the
line". That last step lives in Formalism/GammaFactorNonvanishing/CritLine.lean
and is a short, standard argument; Rubinstein read it. Everything hard is
in proving the no-zeros-to-the-right statement.

## The core idea (Alpöge's own words, S1)

1. **A descendant of Stepanov.** Over function fields (curves over finite
   fields), Stepanov proved the Riemann hypothesis with a divisor argument
   that uses MULTIPLICITY — roughly, differentiating. Alpöge: "multiplicity
   is hard to find over the integers, corresponding to something like
   differentiating whole numbers." The whole proof is, in his words, a
   descendant of Stepanov's argument that finds multiplicity over the
   integers anyway.
2. **Chaining theta lifts to manufacture multiplicity.** The toy setting
   gave "simple, new, Fourier-analytic ideas" that led to chaining theta
   lifts "if we were to have the same tricks recur but work in a natively
   automorphic manner." The line Alpöge says should make mathematicians
   fall out of their chairs: for the von Mangoldt sum of length X, the
   suggested length of the chain of theta lifts, "in view of each mimicking
   multiplicity, was √X."
3. **The lifts.** Iterated theta lifts U(X₀) → U(X₁) → … → U(Xm) between
   totally definite unitary groups; π ↦ π ⊞ μⱼ[t] "wins multiplicity_m".
   Norms of the lifts, level, and cancellation of order-m terms with proven
   divisibility via Chowla–Selberg, Weyl, and Siegel mass. A seesaw: the
   period of the iterated lift is a Bessel period independent of the Hecke
   characters (Rallis).
4. **The sign.** The Guinand–Weil explicit formula had the sign. A variance
   test-function trick; the sum Λ(n)·n⁻¹-type von Mangoldt sums; the quadric
   x₁·x₂ + … + x_{k−1}·x_k; Bertini giving a definite sign from middle
   cohomology; iterating Parseval k times; opposite signs meaning no
   cancellation of inverse roots. "QED; vectorize to go up dimensions."
5. **The supporting cast (from the 20-step timeline in S1).** Stepanov
   determinant (Oct 6); Dp ≡ 0 on a CM curve for p inert; qN = Mk + R with
   the sixfold cover of GL₅ and automorphy of μ; a determinant giving W ≥ 0
   ("Stepanov with multiplicity one again; bootstrap!!"); the switch to Λ
   (Oct 20); determinants for W(·) containing GGP periods; Bost slope
   inequality; Iwasawa tower via analogy to pigeonhole on F_qⁿ/F_q; relative
   trace formula; fighting a weakening of Vandiver for classes in
   H¹ that couldn't be killed by twisting; covolumes, theta series index,
   congruences between lifts and forms; GRH on Nov 16.

Alpöge's own warning about the timeline (S1, footnote 4): the parts where
Claude is the expert and he is not are "sort of paraphrasing a 'slop'
summary, which might make zero sense." He also says he "may have baked lots
of strange suboptimal choices into the argument, and expect short arguments
to follow fairly quickly."

## What mathematicians who have looked say

- Terence Tao (preliminary review, via R2): the proof "appears to use the
  full power of modern developments on the Langlands program and arithmetic
  geometry."
- Filippo Nuccio (via R2): "it basically contains all number theory
  produced in the last 50 years, in all branches of the discipline."
- Thomas Bloom (via R2): more algebraic in approach than OpenAI's analytic
  proof of the quasi-Riemann hypothesis.
- Andrew Granville (via R2): criticized the clarity of the 4-page sketch
  and its timing (one day after Anthropic's IPO).
- Maksym Radziwiłł (via R2): noted the lack of human understanding in the
  formalization, in contrast to what a traditional proof is expected to be.
- Alpöge himself (S1; X 2026-11-23 via R2): "The Lean is full of garbage
  obviously, but compiles"; he has not mastered the neighbourhood around the
  mathematics and intends to understand and impart it.

## What is NOT yet publicly explained

- NO human-readable account of the proof exists as of 2026-11-25. A
  complete prose proof has not been published; Alpöge says he intends to
  write one.
- HOW the theta-lift chain actually produces the zero-free region — the
  mechanism, not the slogan — is NOT YET PUBLICLY EXPLAINED. The remark.pdf
  gives the shape (Stepanov → multiplicity → lifts → sign → QED) and a
  compressed timeline, not a readable argument.
- Whether the proof can be "massively simplified, likely immediately"
  (Alpöge's own prediction) is untested.
- The source has NO comments (15,531,759 non-blank lines, zero comments,
  per the independent spec record) — the code does not explain itself.

## An independent check that the statements have classical content

Sutherland (S4): combining the proof with Robin1984 (an independent
formalization of Robin-type criteria) yields three theorems with no
hypotheses and NO mention of zeta zeros at all — Robin's inequality,
Lagarias's inequality, and a cyclotomic corrected ideal Robin statement.
These were verified the same way (comparator, con-leche, con-ron, nanoda;
Robin1984's own lake comparator passed 2026-11-24 05:09 UTC). This matters
because it shows the proved statements are not empty formalism: they imply
concrete inequalities about divisor sums that anyone can state in plain
arithmetic. (It does not by itself answer the anyGeometry question, which
is about definitions on the dependency path inside the main proof.)
