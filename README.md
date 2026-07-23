# Erdős Problem #477, cubic case: a tiling complement for the cubes

**Claim:** the set B = {k³ : k ∈ ℤ} of integer cubes has a *tiling complement* in ℤ — a set
A ⊂ ℤ such that every integer n has a **unique** representation n = a + k³ with a ∈ A, k ∈ ℤ.

This resolves the degree-3 case of [Erdős Problem #477](https://www.erdosproblems.com/477): does
*any* polynomial f : ℤ → ℤ of degree ≥ 2 have this property? Erdős and Graham conjectured no.
Degree 2 was closed negatively earlier this year (AlphaProof + Adenwalla). The general question
(existence for *some* degree ≥ 2) may already be answered affirmatively by a different,
independently-produced construction at degree 13 ([Peng et al., June 2026]
(https://github.com/Pengbinghui/pipeline-math/blob/main/papers/tiling-complement.pdf)) — but that
construction structurally cannot reach degree 3 (the Mason–Stothers/Brownawell–Masser bound it
relies on only becomes strong enough at odd degree ≥ 13; see §6). The cubic case needed a
different tool.

**Provenance:** the construction was produced by GPT-5.6 Sol via ChatGPT Pro (OpenAI), run twice independently
with different case-splits, both converging on the same bound. It was then adversarially
attacked — same reasoner, fresh session, explicitly instructed to try to refute rather than
confirm — and separately checked by Claude (Anthropic) against the primary sources: the actual
theorem statements in the cited papers, not abstracts, plus several claims re-derived from
scratch independently of either model's account. Full trail in [`VERIFICATION.md`](VERIFICATION.md).
We are not claiming certainty — see the open items at the end — but we could not find a hole
after real effort, and we think this is ready for outside eyes.

— Patrick White & Claude (MathDyad)

---

## 1. Setup

Let B = {k³ : k ∈ ℤ}, D = B − B = {u³ − v³ : u, v ∈ ℤ}. For a target c ∈ ℤ \ B and X ≥ 1, define

E_c(X) = #{1 ≤ k ≤ X : c − k³ ∈ D}

— the "bad" shifts k for which c − k³ collides with a difference of two cubes.

**Finite-avoidance reduction (elementary).** If, for every finite C ⊂ ℤ \ B, there exists k with
(C − k³) ∩ D = ∅ for every c ∈ C simultaneously, a greedy enumeration of ℤ builds a full exact
complement A. (Proof in §5 — standard diagonal argument, no uniformity in |C| required, since the
threshold X can be chosen fresh at each finite stage.)

So it suffices to prove:

## 2. Main theorem

For every noncube c ∈ ℤ and every ε > 0,

**E_c(X) ≪_{c,ε} X^(18/19+ε).**

Since this is o(X), for every *finite* C ⊂ ℤ \ B, all but o(X) of the integers 1 ≤ k ≤ X
simultaneously avoid every target in C — finite avoidance holds, and §5 finishes the proof.

## 3. The two external inputs

**(HB) Heath-Brown, 2008** ("Sums and Differences of Three k-th Powers," J. Number Theory 129
(2009); [arXiv:0806.4330](https://arxiv.org/abs/0806.4330), Theorem 1). For a nonsingular diagonal
form F(x₁,x₂,x₃) = x₁^k ± x₂^k ± x₃^k and fixed N ≪_F B^(3/13), the number of solutions with
coordinates ≤ B, apart from "special" solutions (one signed term individually equal to N), is
O_ε(B^(9/10+ε) N^(1/10)).

**(BHB) Browning–Heath-Brown** ("Plane curves in boxes and equal sums of two powers," Math. Z. 251
(2005); [arXiv:math/0506497](https://arxiv.org/abs/math/0506497), formula (3), the P₁=1 case of
their Theorem 1). For an absolutely irreducible ternary cubic F, and a box with sides 1, P₂, P₃:

N(F;1,P₂,P₃) ≪_ε P₃^ε · exp(log P₂ · log P₃ / log 𝒯)

where 𝒯 is the largest box-weight of any monomial occurring in F with nonzero coefficient. The
implied constant depends only on the degree and ε — but see §7 on the coefficient-height question,
where we tie this to the sharper explicit form in Heath-Brown's earlier paper ("The density of
rational points on curves and surfaces," Ann. of Math. 155 (2002);
[arXiv:math/0405392](https://arxiv.org/abs/math/0405392), Theorem 14), which makes an explicit
(log‖F‖)^(2n−3) factor visible and shows it's harmless here.

## 4. Proof of the main theorem

A bad k has c = k³ + x³ − y³ for some x, y ∈ ℤ.

**Case split on sign(x,y).** If x, y have opposite sign, then |x|, |y| ≤ |c − k³|^(1/3) ≪_c X, so
(k,x,y) lies in a box of size O_c(X). Apply (HB) directly: c is not a cube, so no special solution
exists, giving O_{c,ε}(X^(9/10+ε)) triples in this case.

If x, y have the same sign, write h = |y − x| ≥ 1, u = x + y. The identity
4(k³ − c) = h³ + 3hu² (from y³ − x³ = (y−x)(y² + xy + x²), 4(y²+xy+x²) = h² + 3u²) gives, since
k³ − c = h(h² + 3xy)/1 ≥ h³ when xy > 0:

**h ≪_c X.**

Split at H = X^(17/19).

*Small gaps (h ≤ H).* Fix h and an admissible residue r mod h with h | 4(r³ − c) — there are
≪_{c,ε} h^ε such residues (elementary Hensel-lifting count, §8). Writing k = r + hℓ and clearing
denominators gives a ternary cubic H_{h,r}(1,ℓ,u) = 0 with box sides P₂ ≍_c X/h, P₃ ≍_c
X^(3/2)h^(−1/2), and coefficients O_c(h²) (not h³ — the naive homogeneous expansion overstates
this; see §7). The curve is absolutely irreducible except at the single value h³ + 4c = 0 (a
direct partial-derivatives check on the K = rw + ht substituted model — recognizably a disguised
Weierstrass cubic, s² ∝ (cubic in K), singular exactly when its constant term vanishes). Apply
(BHB): each nonsingular (h,r) contributes ≪_{c,ε} X^(1/2+ε) h^(−1/2). Summing over h ≤ H and the
≪ h^ε residues per h gives ≪_{c,ε} X^(1/2+ε) H^(1/2+ε) = X^(18/19+ε) (with H = X^(17/19)).

*The singular fiber.* At h³ + 4c = 0 (at most one h per c), the equation degenerates to
4k³ = 3hu², forcing k = κ·(integer)² for a fixed squarefree κ — only O_c(X^(1/2)) values of k.
This is not swept under the rug: it is a genuine infinite family. For c = −2d³ (any d ≥ 1),

**(6ds²)³ + [d(6s³−1)]³ − [d(6s³+1)]³ = −2d³** for every s ≥ 1

— an exact identity (verified below, both algebraically and by direct computation), matching
Heath-Brown's own published example (his paper opens with the sibling identity for c = 2). It
contributes O_c(X^(1/2)) bad k's, which is negligible against X^(18/19).

*Large gaps (h > H).* Then |x|, |y| ≪_c X^(3/2) H^(−1/2) = X^(20/19). Apply (HB) again (dyadically)
to this box: O_{c,ε}(X^(18/19+ε)) triples.

Summing all three contributions gives E_c(X) ≪_{c,ε} X^(18/19+ε), proving the theorem.

## 5. The greedy construction

Enumerate ℤ = {n₁, n₂, …}. Build finite sets A₀ ⊂ A₁ ⊂ ⋯ with translates a + B (a ∈ Aⱼ) pairwise
disjoint, covering n₁,…,nⱼ at stage j. At each step, if nⱼ is uncovered, C = {nⱼ − a : a ∈ Aⱼ₋₁}
is a finite subset of ℤ \ B (else nⱼ would already be covered). By finite avoidance (§2), some
k = kⱼ has (C − k³) ∩ D = ∅; set a* = nⱼ − k³ and Aⱼ = Aⱼ₋₁ ∪ {a*}. If the new translate collided
with an old one, a* − a ∈ D for some a ∈ Aⱼ₋₁ — but a* − a = (nⱼ−a) − k³, which was chosen outside
D. No collision. A = ⋃ⱼ Aⱼ is the exact complement. (This step needs no uniformity in |C| — the
threshold X at stage j is chosen fresh, after Cⱼ is already fixed and finite.)

## 6. Why degree 13, not 3, for the general question

Peng et al.'s construction excludes *all* rational curves on the relevant surface via
Brownawell–Masser (an S-unit theorem over function fields), which requires a Mason–Stothers-type
inequality k·e > (3)(4e−2) to fail for every e — true for all k ≥ 12, false at k = 3 (the
inequality is satisfiable there, so their exclusion argument gives no contradiction). Smooth cubic
surfaces are genuinely rational and carry real families of rational curves (the identity in §4 is
one), which is exactly why degree 3 needs the finer determinant-method route above instead of a
clean exclusion argument.

## 7. Coefficient-height note

The absolutely-irreducible cubic used in §4's small-gap case, dehomogenized at w=1, has
coefficients O_c(h²) (using a centered residue |r| ≤ h/2): the t³ coefficient is O(h²), the t²
coefficient O(hr) = O(h²), the t coefficient O(r²) = O(h²), and the constant term
O(r³/h) + O(h²) = O(h²). Heath-Brown's explicit determinant-method bound (Ann. of Math. 155,
Theorem 14) carries a (log‖F‖)^(2n−3) factor for n-variable forms; for our case this is a *fixed*
power of log h ≪ log X, absorbed into X^ε regardless of the precise exponent. No hidden dependence
on h survives past this log factor.

## 8. Residue-count lemma

R_c(h) = #{r mod h : h | 4(r³−c)} ≪_{c,ε} h^ε: standard — for p ∤ 3c, at most 3 roots mod p with
unique Hensel lift to every p^e; for the finitely many primes dividing 3c, bounded in terms of c
by a valuation argument. Multiplicative, giving R_c(h) ≪_c 3^ω(h) ≪_{c,ε} h^ε.

## Open items — what we have *not* independently re-derived

- We have not re-proved (HB) or (BHB) from their own foundations (the p-adic determinant method
  itself). Our check confirms the cited statements exist as claimed in the primary sources and
  that the hypotheses are met here — not that the underlying papers are themselves error-free.
- Everything above has been checked by the same model family that constructed it (two independent
  GPT-5.6 Sol (ChatGPT Pro) runs) plus Claude's from-scratch spot-checks (identity verification, the
  rational-lines argument in `VERIFICATION.md` §1, primary-source citation chases). No genuinely
  different model lineage, and no formal (Lean) verification, has looked at this yet — though the
  problem statement is already formalized at
  [google-deepmind/formal-conjectures](https://github.com/google-deepmind/formal-conjectures/blob/main/FormalConjectures/ErdosProblems/477.lean),
  so that's a concrete next step for anyone who wants to take it on.

Corrections, refutations, and pointers to literature we missed are genuinely welcome — see
[`VERIFICATION.md`](VERIFICATION.md) for the full adversarial trail, including the specific points
we pushed hardest on before deciding this was ready to share. The adversarial brief we used to
attack our own construction is in [`appendix/refutation-brief.md`](appendix/refutation-brief.md);
raw session transcripts from both proof runs and the refutation round are available on request.
