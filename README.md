# Erdős Problem #477: every integer power ≥ 3 has a tiling complement

**Claim:** for every integer K ≥ 3, the set B_K = {mᴷ : m ∈ ℤ} has a *tiling complement* in ℤ — a
set A ⊂ ℤ such that every integer n has a **unique** representation n = a + b, a ∈ A, b ∈ B_K.

This is [Erdős Problem #477](https://www.erdosproblems.com/477), which asks: does *any*
polynomial f : ℤ → ℤ of degree ≥ 2 have this property? Erdős and Graham conjectured no. Combined
with the already-published negative result for degree 2 (AlphaProof + Sarosh Adenwalla — every
even-symmetric or linear-shifted quadratic fails via a congruence argument), this would resolve
the question in full: **no for degree 2, yes for every degree ≥ 3.**

**Scope note — this claim grew in two stages, both documented here.** We first closed the cubic
case (K=3) alone; that construction and its independent verification trail are preserved at
[`appendix/cubic-case-detail.md`](appendix/cubic-case-detail.md). We then asked whether the same
method generalizes to degrees 4–12 (the only gap left by a separate, differently-constructed
degree-13 result — [Peng et al., June 2026](https://github.com/Pengbinghui/pipeline-math/blob/main/papers/tiling-complement.pdf)).
It came back not just covering 4–12, but proving the fully general statement for every K ≥ 3 by
the same uniform argument, K=3 included. What follows is that general proof. The cubic-specific
appendix remains as the first, independently-verified instance and its own worked example.

**Provenance:** construction via GPT-5.6 Sol (ChatGPT Pro, OpenAI). Adversarially attacked twice —
once for the cubic case alone, once for the general/K=4–12 extension — in fresh sessions
explicitly instructed to refute rather than confirm, and separately checked by Claude (Anthropic)
against primary sources rather than taken on faith. The second adversarial round found one real
(cosmetic, non-load-bearing) error, corrected below — see [`VERIFICATION.md`](VERIFICATION.md).
**We have not yet sought review from a human mathematician or a different model lineage, and this
has not been posted to erdosproblems.com's own forum** — their posting rules explicitly require a
human to have independently verified the mathematics (or a sorry-free Lean proof) before posting
there, and we don't yet clear that bar ourselves. This repository is offered for outside scrutiny,
not as a claim of community acceptance.

— Patrick White & Claude (MathDyad)

---

## Semantic note (checked against the primary source)

The problem asks for uniqueness of the **value** b ∈ B_K, not uniqueness of the integer m with
mᴷ=b. This matters for even K, where m ↦ mᴷ is not injective. We checked this against the actual
erdosproblems.com LaTeX statement ("...there is exactly one a∈A and b∈{f(k):k∈ℤ}...") and against
Sekanina's original 1959 exact-factorization definition, which is unambiguous: m=a+b with a,b
themselves unique, not any parameter used to enumerate B. It also has to be this reading for the
degree-2 negative result to be a real theorem at all — under literal (a,k)-pair uniqueness, every
even polynomial would fail trivially (f(k)=f(-k) always), and the actual published degree-2 proof
is a genuine congruence argument, not that triviality. For K=3 the distinction is moot (k↦k³ is
injective), which is why the cubic write-up phrases things in terms of a unique k without loss.

## 1. Setup

For B_K = {mᴷ : m ∈ ℤ}, D_K = B_K − B_K, and c ∈ ℤ \ B_K, define

E_{K,c}(X) = #{1 ≤ n ≤ X : c − nᴷ ∈ D_K}.

**Finite-avoidance reduction (elementary).** If for every finite C ⊂ ℤ \ B_K there's an n with
(C − nᴷ) ∩ D_K = ∅, a greedy enumeration of ℤ builds a full exact complement (§7 below — no
uniformity in |C| needed, since the threshold is chosen fresh at each finite stage).

## 2. Main theorem

For fixed K ≥ 3, let q_K = min(9/10, 10/K), α_K = (q_K·K−1)/(K−2+q_K), β_K = q_K(K−1)/(K−2+q_K).
Then for every ε > 0:

**E_{K,c}(X) ≪_{K,c,ε} X^(β_K+ε).**

Since q_K < 1 and K > 2, β_K < 1 always — so this is o(X), which is what finite avoidance needs.
For 3 ≤ K ≤ 11, q_K = 9/10. For K ≥ 12, q_K = 10/K. (A formal check: substituting K=2 into the
same formula gives exponent exactly 1, not o(X) — the mechanism structurally turns on exactly at
degree 3, matching where the negative quadratic result sits.)

## 3. The two external inputs

**(HB1/HB2) Heath-Brown** ("Sums and Differences of Three k-th Powers," J. Number Theory 129
(2009); [arXiv:0806.4330](https://arxiv.org/abs/0806.4330)). For a nonsingular diagonal ternary
form X₁ᴷ±X₂ᴷ±X₃ᴷ, apart from "special" solutions (one signed term individually equal to the
target), the solution count in a box of size B is O_{K,ε}(B^(9/10+ε)) (Theorem 1) or O_K(B^(10/K))
(Theorem 2) — both explicit theorem statements, not abstract-level paraphrase. The paper's proof
shows linear diagonal parameterizations reduce to special solutions via Fermat's Last Theorem, so
no per-degree line-classification is needed.

**(BHB) Browning–Heath-Brown** ("Plane curves in boxes and equal sums of two powers," Math. Z. 251
(2005); [arXiv:math/0506497](https://arxiv.org/abs/math/0506497)). For absolutely irreducible
ternary F of degree d and box sides 1 ≤ P₂ ≤ P₃ with 𝒯 the largest monomial box-weight:

N(F;1,P₂,P₃) ≪_{d,ε} P₃^ε · exp(log P₂ · log P₃ / log 𝒯)

— implied constant depending only on d and ε, not on F's coefficients.

## 4. Reduction to a gap parameter

A bad n has c = nᴷ + xᴷ − yᴷ, i.e. nᴷ − c = yᴷ − xᴷ (1). Discard O_c(1) small n so R := nᴷ−c > 0.

**Even K:** set a=|x|, b=|y|; then R = bᴷ−aᴷ, b>a.

**Odd K:** if x,y have opposite sign, R = |x|ᴷ+|y|ᴷ, giving |x|,|y| ≪_c X directly — counted by
(HB) in O_{K,c,ε}(X^(q_K+ε)) (2). Otherwise (same weak half-line, including zero), set nonnegative
a<b so again R = bᴷ−aᴷ.

Either way, b=a+h, h≥1, and from bᴷ−aᴷ = h(bᴷ⁻¹+bᴷ⁻²a+...+aᴷ⁻¹): h ≪_c X (4), and
a ≤ b ≪_c X^(K/(K−1)) h^(−1/(K−1)) (5).

## 5. Small gaps

Fix cutoff H<X, 1≤h≤H.

**Residue classes.** R_{K,c}(h) = #{r mod h : rᴷ≡c mod h} ≪_{K,c,ε} h^ε — standard: ≤K roots mod
p (p∤Kc) with unique Hensel lift; finitely many p|Kc handled by a bounded valuation argument.

**The curve.** Write n=r+hℓ. Homogenizing gives an integral degree-K form Φ_{h,r}(W,L,A), with
box sides P₂ ≍_c X/h, P₃ ≍_c X^(K/(K−1)) h^(−1/(K−1)).

**Absolute irreducibility — unconditional, every h and c.** After the substitution Z=r+hL, the
curve is Zᴷ = P(A), P(A) = c+(A+h)ᴷ−Aᴷ, degree exactly K−1, leading coefficient Kh. Over
L=ℂ(A) (which contains every K-th root of unity), suppose Zᴷ−P(A) reducible with a root θ of
degree d<K over L. Then L(θ)/L is automatically Galois (it already contains all K roots ζθ),
cyclic of order d|K, so θᵈ ∈ L, and P = θᴷ = (θᵈ)^(K/d) — a p-th power in ℂ(A) for some prime
p|K. But the valuation of P at infinity is −(K−1), and gcd(K,K−1)=1, so no prime dividing K can
divide that valuation. Contradiction — the curve is absolutely irreducible for every h,c, singular
or not (the classical Vahlen–Capelli exceptional case for 4|K vanishes here specifically because
ℂ(A) contains i, making −4b⁴=(2ib²)² already a square).

**Applying BHB.** The monomial −K·Aᴷ⁻¹W gives 𝒯 ≥ P₃ᴷ⁻¹, so

N(Φ_{h,r};1,P₂,P₃) ≪_{K,ε} P₃^ε P₂^(1/(K−1)) = X^(1/(K−1)+ε) h^(−1/(K−1)+ε).

Summing over h≤H and the ≪h^ε residues per h:

S_K(X,H) ≪_{K,c,ε} X^(1/(K−1)+ε) H^((K−2)/(K−1)+ε).

## 6. Large gaps

For h>H: a,b ≪_c M := X^(K/(K−1)) H^(−1/(K−1)) ≥ X. Every counted solution here is non-special —
a case check by sign of c and parity of K (§6 detail in `VERIFICATION.md`) shows any special
solution would force c ∈ B_K, contradiction, or (even K, c<0) force n=0, contradicting n≥1. Dyadic
Heath-Brown gives

L_K(X,H) ≪_{K,c,ε} X^(q_K·K/(K−1)+ε) H^(−q_K/(K−1)).

## 7. Balancing and the greedy construction

Setting H=X^α and balancing the two exponents gives α_K = (q_K·K−1)/(K−2+q_K), common exponent
β_K = q_K(K−1)/(K−2+q_K) < 1, proving E_{K,c}(X) = O(X^(β_K+ε)) = o(X). The odd-K opposite-sign
contribution X^(q_K+ε) is smaller and absorbed.

The greedy construction is standard: enumerate ℤ, maintain disjoint translates a+B_K covering an
initial segment; at each uncovered mⱼ, the finite target set Cⱼ = {mⱼ−a : a already chosen} is
automatically ⊂ ℤ\B_K; finite avoidance gives an n with (Cⱼ−nᴷ)∩D_K=∅; adjoin a*=mⱼ−nᴷ. No
collision by construction, no uniformity needed in the growing Cⱼ (the threshold at each stage is
chosen fresh, after that stage's C is already fixed).

## 8. Exceptional-fiber audit (not needed for the proof, but explains the cubic identity)

Not load-bearing — §§4–7 only use absolute irreducibility, proved unconditionally above, never
smoothness or genus. This section explains *why* the cubic case (K=3) needed a separate
exceptional-family treatment and higher K don't.

**Singular condition.** Z^K=c+(A+h)^K-A^K is singular at a finite point exactly when
c = −hᴷ/(q−1)^(K−1) for some (K−1)-th root of unity q≠1; every such repeated root is exactly
double.

**Even K:** K−1 is odd, and (q−1)^(K−1) is always nonzero and *purely imaginary* for q a nontrivial
(K−1)-th root of unity (derivation: q−1 = 2i·sin(θ/2)·e^(iθ/2), so (q−1)^(K−1) picks up a factor
i^(K−1) = ±i since K−1 is odd). Since c/hᴷ must be rational, this can never hold for real
integer c,h — **every even-K fiber is smooth**, unconditionally, for every arithmetically relevant
value. (No genus argument is even needed for even K.)

**Odd K ∈ {5,7,9,11}:** finitely many explicit rational singular c per h (tabulated in
`VERIFICATION.md`), each pinning at most one h for fixed c — singular gaps stay O_K(1), don't
proliferate with X.

**Genus, corrected.** For the cyclic cover Zᴷ=P(A), a point where P has order m contributes
K−gcd(K,m) to the ramification divisor. The generic curve has genus g₀=(K−1)(K−2)/2. Each double
root (order-2 zero, s of them) drops the genus by **s·(K−2+gcd(K,2))/2** — not s(K−1)/2 as an
earlier draft of this section claimed. That formula happens to coincide with the correct one for
odd K (gcd(K,2)=1) but is wrong for even K (an easy tell: for K=4 it produces a non-integer
genus, 1.5, which is impossible). The corrected version gives integer genus 1 for a complex K=4
singular fiber — but since even-K fibers are never singular for real/integer c (previous
paragraph), this correction has zero arithmetic consequence; it only fixes a mislabeled complex-
geometry aside. For the odd-K singular fibers that *do* occur arithmetically (K=5,7,9,11), the
original (unaffected-by-the-bug) genus values hold — all ≥2 — meaning by Riemann–Hurwitz no
nonconstant map from ℙ¹ (hence no polynomial parametrization, no cubic-style identity) can exist
on any of them. This is why the cubic case is genuinely special: its own singular fiber has genus
0 (a cuspidal cubic), which is exactly what admits the explicit identity in the cubic appendix;
every K=4–12 exceptional fiber sits at genus ≥1 (even K, vacuously — no such fiber exists at all)
or ≥2 (odd K), closing off the cubic-style mechanism entirely.

## 9. Degree-by-degree table

| K | H=X^α_K | β_K | HB input |
|---|---|---|---|
| 3 | X^17/19 | 18/19 | HB1 *(cubic case; see appendix for the fully independent original write-up)* |
| 4 | X^26/29 | 27/29 | HB1 |
| 5 | X^35/39 | 12/13 | HB1 |
| 6 | X^44/49 | 45/49 | HB1 |
| 7 | X^53/59 | 54/59 | HB1 |
| 8 | X^62/69 | 21/23 | HB1 |
| 9 | X^71/79 | 72/79 | HB1 |
| 10 | X^80/89 | 81/89 | HB1 |
| 11 | X^89/99 | 10/11 | HB1 |
| 12 | X^54/65 | 11/13 | HB2 |

...and the general closed form covers every K≥13 too (subsuming, via a completely different
route, what Peng et al.'s degree-13 S-unit construction already established for that one case).

## Open items — what we have *not* independently re-derived

- We have not re-proved (HB1/HB2) or (BHB) from their own foundations (the p-adic determinant
  method itself). We've confirmed the cited statements exist as claimed in the primary sources and
  that their hypotheses are met in this application — not that the underlying papers are
  themselves error-free.
- Everything above has been checked by the same model family that constructed it (GPT-5.6 Sol,
  multiple independent runs across the cubic and general rounds) plus Claude's from-scratch spot
  checks — see `VERIFICATION.md` for the specific list, which now includes independently
  re-deriving the corrected genus formula and confirming the K=4 non-integer tell by direct
  computation. No genuinely different model lineage, and no formal (Lean) verification, has looked
  at this yet — though the problem statement is already formalized at
  [google-deepmind/formal-conjectures](https://github.com/google-deepmind/formal-conjectures/blob/main/FormalConjectures/ErdosProblems/477.lean).
- We have not sought review from a working number theorist. Given the scale of what's being
  claimed here (potentially the full resolution of a 46-year-old question), that's the natural
  next step before treating this as settled, not an optional nicety.

Corrections, refutations, and pointers to literature we missed are genuinely welcome — see
[`VERIFICATION.md`](VERIFICATION.md) for the full adversarial trail across both rounds.
