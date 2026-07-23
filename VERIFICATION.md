# Verification trail

Two independent GPT-5.5 Pro runs produced full proofs of the main theorem in `README.md`, via
different case-splits (one on the size of max(|x|,|y|), one on sign(x,y) then a gap parameter),
both landing on the identical exponent 18/19 and citing the identical two external theorems. That
convergence is real signal on the elementary bookkeeping but is *not* independent evidence for the
two external-theorem applications, since both proofs are hostage to the same two citations — same
reasoner, same crux, asked twice.

We then ran a third, adversarial pass: a fresh Pro session, explicitly instructed to attack rather
than confirm, targeted at four specific points. Below is what it found, and — separately, marked
"Claude" — what was checked independently against primary sources rather than taken on the
reasoner's word.

## Target 1 — does Heath-Brown's "apart from special solutions" clause really exclude every other
exceptional linear family, or could a non-cube c admit a hidden rational line on the surface?

**Pro's argument:** enumerate the 27 lines on the diagonal cubic surface K³+X³−Y³−cW³=0 by the
standard construction (pair coordinates, relate by a root of unity times a cube root of a
coefficient ratio). Since the coefficients are (1,1,1,−c), every pairing forces exactly one of its
two defining relations to require c or −c to be a rational cube; the other relation is always
trivially rational (ratio −1, not involving c). So c ∉ B ⟹ zero rational lines on the surface,
full stop.

**Claude, independently:** re-derived this from general diagonal-cubic-surface theory (not from
Pro's writeup) — for a diagonal surface with coefficients {α₀,…,α₃}, a rational line requires both
halves of a 2-2 coordinate split to have a rational cube-root ratio; with three coefficients equal
and one different, every possible split isolates the different one with exactly one of the equal
ones, so every split has exactly one relation requiring the odd coefficient to be a cube and one
that's automatic. Same conclusion, arrived at independently. **Holds.**

## Target 2 — is the Browning–Heath-Brown box theorem's implied constant really uniform across the
*unbounded family* of curves used here (coefficients growing with h), not just one fixed curve?

**Pro's argument:** walked back the flat "coefficient-independent" reading to the more careful
version — there is a log-height factor, but it's a fixed power of log(coefficient size), and the
coefficients here are only O_c(h²), so it's absorbed by X^ε regardless.

**Claude, independently:** chased the actual citation. Found it: D.R. Heath-Brown, "The density of
rational points on curves and surfaces," Ann. of Math. 155 (2002), arXiv:math/0405392 — this is
where the explicit determinant-method bound with a `(log‖F‖)^(2n−3)` factor lives (Theorem 14 in
the arXiv version, not "15" as first cited — a real but immaterial citation slip). Grepped the
actual PDF text to confirm the formula exists as stated: `k ≪_ε (V^d/T)^... V^ε (log‖F‖)^(2n−3)`.
One correction: Pro claimed "n=2 gives one power of log"; the paper's own worked example for plane
curves (n=3 in its indexing) gives `(log‖F‖)^3`, not ^1. This doesn't matter to the conclusion —
any *fixed* power of log X is o(X^ε) for any ε>0 — but it's a real instance of the reasoner
getting a citation detail wrong while the mathematical conclusion survived anyway. Also
independently recomputed the coefficient magnitudes: earlier (pre-adversarial-pass) Claude had
estimated O(d³) using the wrong intermediate representation (the K-substituted homogeneous curve);
the box-counting is actually applied to the *pre-substitution* curve, which has coefficients
O_c(h²) using a centered residue — Pro's version is the correct one, and it's a tighter bound than
Claude's original (mistaken) estimate, not a looser one. **Holds, with one corrected citation
detail that doesn't affect the exponent.**

## Target 3 — does the gap-parameter stratification actually catch every possible large-representation
family, or could a family escape by having its gap parameter grow with k in some untracked way?

**Pro's argument, re-derived from scratch on request:** the gap parameter (h or d, depending on
which proof) is *defined from* each individual solution, not searched for — the bound confining it
to the relevant range (≪_c X^(1−2η) or similar) is a pointwise algebraic inequality on every
solution in the relevant case, not a genericity or averaging claim. Every solution has a
well-defined gap value and falls into exactly one stratum. **Holds** — this is closer to
elementary logic than deep number theory once stated this way.

## Target 4 — the greedy construction needs finite avoidance for a *growing* sequence of target
sets C_j (|C_j| → ∞), but the bound's constant depends on C in an unstated way. Does that ever
threaten the construction?

**Pro's argument:** no — the construction is sequential. At stage j, C_j is already fixed and
finite *before* the threshold X_j is chosen; the constant can depend arbitrarily badly on C_j
without breaking anything, since X_j is picked afterward, specifically large enough. Standard
diagonal-argument logic. **Holds**, and this was really just a request to spell out logic that
was implicit but under-stated in the original write-ups.

## Context check: the Sekanina / Lean "probably negative" expectation

The DeepMind `formal-conjectures` Lean formalization
([source](https://github.com/google-deepmind/formal-conjectures/blob/main/FormalConjectures/ErdosProblems/477.lean))
states the cubic case as "Probably there is no such A for X³," citing Sekanina (1959). This looked
like a real headwind before checking closely.

**Pro's argument:** the Lean file's formal statement restricts to `{n | 0 < n}` — *positive* cubes
only — despite its docstring claiming n ∈ ℤ. Sekanina's actual result is about positive powers and
explicitly leaves k ≥ 3 open; there's no cube-specific obstruction there for the signed set
B = {k³ : k ∈ ℤ} that this proof addresses.

**Claude:** had already noticed the `{n | 0 < n}` restriction independently in an earlier pass
(before the adversarial round), for a different reason (checking whether the Lean formalization's
scope matched the problem's actual LaTeX source), but hadn't drawn out this specific implication.
Given both, the "probably negative" expert prior turns out to be about a materially different
(positive-only) set, not direct counter-evidence against this construction.

## What we did *not* do

- Re-derive the determinant method itself (the p-adic Lemma-1/Lemma-2 machinery in either Heath-Brown
  paper) from scratch. Everything above checks that the *cited statements* exist as claimed and that
  their *hypotheses* are met in this application — not that the underlying 15–46 page papers are
  themselves free of error.
- Get a genuinely different model lineage (non-OpenAI) to attempt refutation. Both the construction
  and the adversarial pass are GPT-5.5 Pro; Claude's role throughout was checking primary sources
  and re-deriving specific elementary claims independently, not an independent full read of the
  whole argument by a different reasoner.
- Formalize any part of this in Lean, though the problem statement is already formalized
  (linked above), which makes at least the elementary skeleton (§5's greedy argument, taking the
  two determinant-method bounds as imported axioms) a tractable target for anyone who wants to
  take it on.
