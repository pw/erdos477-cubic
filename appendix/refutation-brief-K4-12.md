# Dyad brief — ADVERSARIAL REFUTATION of the claimed K=4..12 (+ general K) proof

**Seat:** ChatGPT Pro (GPT-5.6 Sol), max reasoning effort. Fresh chat — treat everything below as a
claim to attack, not ground truth. A different Pro instance, in response to our brief asking it to
try extending the cubic (K=3) construction of Erdős #477 to degrees 4–12, came back claiming FULL
PROOF for K=4 through 12 simultaneously, plus a general theorem for every K≥3. This is a much
bigger claim than the cubic case (github.com/pw/erdos477-cubic) — it would essentially finish the
whole Erdős–Graham question outright when combined with the already-negative K=2 case and the
already-positive K=3 (ours) and K=13 (Peng et al., github.com/Pengbinghui/pipeline-math) cases.
Bigger claim, higher bar. Try to break it. An honest "I found a real gap" or "I couldn't break it"
are both valuable; a false "confirmed" is the only bad outcome.

## The claim under test

*(Full text below, lightly cleaned of rendering artifacts. cite tags in the original: [HB1]=
Heath-Brown Theorem 1 (arXiv:0806.4330), [HB2]=Heath-Brown Theorem 2 (same paper), [BHB]=
Browning–Heath-Brown box theorem (arXiv:math/0506497), [AG]=standard algebraic geometry.)*

## Verdict

FULL PROOF for every degree K=4,...,12. In fact, the same argument proves the stronger statement:

For every integer K≥3, the image set B_K={m^K : m∈ℤ} has an exact additive complement in ℤ.

For 4≤K≤11, Heath-Brown's 9/10-exponent theorem is enough. For K=12, his 10/K=5/6 theorem gives a
substantially better exponent. The Browning–Heath-Brown small-box estimate becomes stronger, not
weaker, as K grows.

There is one semantic pin worth fixing first. Erdős #477 is naturally the image-set tiling
problem: uniqueness of a∈A and b∈f(ℤ), not uniqueness of the preimage k. That is also the
formulation visible in the problem's discussion and the one used by the cubic repo. Under literal
uniqueness of the pair (a,k), f(k)=k^K would be unusable for even K, since f(k)=f(-k). Everything
below concerns the actual image-set formulation A⊕B_K=ℤ.

Rigor tags: [Elementary] proved directly below. [HB1] Heath-Brown, Theorem 1. [HB2] Heath-Brown,
Theorem 2. [BHB] Browning–Heath-Brown's plane-curve box estimate. [AG] standard algebraic
geometry, used only for the exceptional-family audit, not the main proof. No heuristic step enters
the proof.

### 1. Quantitative theorem

For fixed K≥3, put D_K=B_K−B_K and, for c∉B_K, E_{K,c}(X)=#{1≤n≤X : c−n^K∈D_K}.

Define q_K=min(9/10, 10/K), and α_K=(q_K·K−1)/(K−2+q_K), β_K=q_K(K−1)/(K−2+q_K).

Then: E_{K,c}(X) ≪_{K,c,ε} X^{β_K+ε} for every ε>0.

Since q_K<1 and K>2, β_K<1. Thus E_{K,c}(X)=o(X), which is exactly what finite avoidance needs.

For 4≤K≤11, q_K=9/10, so α_K=(9K−10)/(10K−11), β_K=9(K−1)/(10K−11).
For K=12, q_12=5/6, α_12=54/65, β_12=11/13.

### 2. The two published inputs

[HB1/HB2] Heath-Brown proves for the nonsingular diagonal ternary form X_1^K±X_2^K±X_3^K that,
apart from special solutions, the number of solutions of a fixed equation in a box of size B is
O_{K,c,ε}(B^{9/10+ε}) from Theorem 1, and O_K(B^{10/K}) from Theorem 2, subject to conditions on
the fixed right-hand side that are automatic once B is sufficiently large. The diagonal "apart
from special solutions" conclusion is part of the theorem itself, not an inference from an
abstract. The proof explicitly says linear parameterizations for diagonal forms reduce to special
solutions using Fermat's Last Theorem. So no degree-by-degree classification of lines on Fermat
surfaces is needed here. The homogenized equation remains a surface in P^3 for every K; its degree
changes, not its dimension.

[BHB] For an absolutely irreducible ternary form F of degree d, and 1≤P_1≤P_2≤P_3, let T be the
largest box-weight of a monomial occurring in F. When P_1=1,
N(F;1,P_2,P_3) ≪_{d,ε} P_3^ε exp(log P_2 · log P_3 / log T).
The paper's convention makes the implied constant depend only on d and ε, not on the coefficients
of F. Thus the changing coefficients indexed by h,r are not a uniformity problem.

### 3. Elementary reduction to gaps

A bad n has c=n^K+x^K−y^K, i.e. n^K−c=y^K−x^K (1). Discard O_c(1) small n so R:=n^K−c>0.

**Even K.** Set a=|x|,b=|y|. Then R=b^K−a^K, b>a. Sign choices give constant multiplicity.

**Odd K.** If x,y have strictly opposite signs, R=|x|^K+|y|^K, so |x|,|y|≪_c X — counted directly
by Heath-Brown in O_{K,c,ε}(X^{q_K+ε}) (2). If x,y lie on the same weak half-line (including zero),
define nonnegative a<b so again R=b^K−a^K.

Either way, every remaining solution has b=a+h, h=b−a≥1, and n^K−c=(a+h)^K−a^K (3). From
b^K−a^K=h(b^{K−1}+b^{K−2}a+...+a^{K−1}): h^K≤R≪_c X^K and h·b^{K−1}≤R≪_c X^K. Hence h≪_c X (4) and
a≤b≪_c X^{K/(K−1)} h^{−1/(K−1)} (5). This is the uniform higher-degree replacement for the cubic
identity involving h and u=x+y — no special quadratic-form identity needed.

### 4. Small gaps

Fix cutoff H<X, 1≤h≤H.

**4.1 Residue classes.** n^K≡c (mod h). R_{K,c}(h)=#{r mod h : r^K≡c mod h} ≪_{K,c,ε} h^ε (6).
Proof: for p∤Kc, roots mod p are simple (≤K of them), unique Hensel lift. For the finitely many
p|Kc, put t=v_p(c); for e>t a solution needs K|t, v_p(r)=t/K; after removing this fixed power of p
one gets a unit equation, whose solution count is bounded in terms of K,p uniformly in the
exponent. CRT gives R_{K,c}(h)≪_{K,c} K^{ω(h)} ≪_{K,c,ε} h^ε.

**4.2 The plane curves.** Choose r mod h with r^K≡c mod h, write n=r+hℓ. Homogenizing:
Φ_{h,r}(W,L,A) = [(rW+hL)^K − cW^K − (A+hW)^K + A^K] / h (7) — an integral form of degree K (r^K−c
divisible by h; every other term in the first binomial contains h; every term in (A+hW)^K−A^K
contains h). Relevant solutions have W=1, |L|≪_c X/h, 0≤A≪_c X^{K/(K−1)} h^{−1/(K−1)}. Set
P_2≍_c X/h, P_3≍_c X^{K/(K−1)} h^{−1/(K−1)} (8); since h≤X, P_2≤P_3.

**4.3 Absolute irreducibility: no exceptional fibers at all.** After the invertible affine
substitution Z=r+hL, the dehomogenized curve is Z^K=P_{h,c}(A), P_{h,c}(A)=c+(A+h)^K−A^K (9),
degree exactly K−1, leading coefficient Kh.

Claim: Z^K−P_{h,c}(A) is absolutely irreducible for every h≠0 and every c. Let L=ℂ(A); suppose
reducible, θ a root with d=[L(θ):L]<K. Since L contains all K-th roots of unity, all roots ζθ lie
in L(θ), so L(θ)/L is Galois with group ⊆ μ_K cyclic of order d, hence θ^d∈L. So
P_{h,c}(A)=θ^K=(θ^d)^{K/d} — a p-th power in ℂ(A) for some prime p|K/d, hence p|K. But the
valuation at infinity of P_{h,c} is v_∞=−(K−1), not divisible by any prime dividing K (since
gcd(K,K−1)=1). Contradiction. So Φ_{h,r} is absolutely irreducible, always.

*Correction to the cubic write-up:* the cubic exceptional fiber h³+4c=0 is singular but still
absolutely irreducible (a cuspidal cubic k³=λu²). The README's partial-derivative calculation
correctly detects singularity, but singularity does not imply reducibility — the separate O(X^1/2)
treatment there is valid but was actually unnecessary; BHB already applies to that fiber directly.

**4.4 Applying BHB.** Φ_{h,r} contains the monomial −KA^{K−1}W, so T≥P_3^{K−1}. BHB gives
N(Φ_{h,r};1,P_2,P_3) ≪_{K,ε} P_3^ε exp(log P_2 log P_3/log T) ≪_{K,ε} P_3^ε P_2^{1/(K−1)} (since
log T≥(K−1)log P_3) = X^{1/(K−1)+ε} h^{−1/(K−1)+ε} (10) using (8). Multiplying by (6) and summing
h≤H: S_K(X,H) ≪_{K,c,ε} X^{1/(K−1)+ε} H^{(K−2)/(K−1)+ε} (11). Small-gap exponent improves as K
grows.

### 5. Large gaps

h>H. By (5), a,b≪_c M:=X^{K/(K−1)} H^{−1/(K−1)} (12). Since H≤X, M≥X, so n,a,b lie in a common box
of size O_c(M). Relevant equation: n^K+a^K−b^K=c (13).

**5.1 Special solutions.** If c>0: special would need n^K=c, a^K=c, or −b^K=c — first two
contradict c∉B_K; third impossible for even K, and for odd K would say c=(−b)^K∈B_K. If c<0:
apply Heath-Brown to b^K−n^K−a^K=−c. Odd K: every special again implies c∈B_K. Even K: only extra
possibility b^K=−c, but then n^K+a^K=0 forces n=a=0, contradicting n≥1. So every counted solution
is non-special.

**5.2 Heath-Brown count.** After dyadic decomposition, L_K(X,H) ≪_{K,c,ε} M^{q_K+ε}, i.e. using
(12): L_K(X,H) ≪_{K,c,ε} X^{q_K K/(K−1)+ε} H^{−q_K/(K−1)} (14). For odd K, the opposite-sign branch
from (2) is O(X^{q_K+ε}), smaller than the optimized exponent below.

### 6. Exponent optimization

H=X^α. Small-gap exponent (11): (1+(K−2)α)/(K−1). Large-gap exponent (14): q_K(K−α)/(K−1).
Balancing: 1+(K−2)α=q_K(K−α), so α=α_K=(q_K K−1)/(K−2+q_K). Common exponent β_K=q_K(K−1)/(K−2+q_K).

β_K−q_K = q_K(1−q_K)/(K−2+q_K) > 0, so the odd-K opposite-sign contribution is absorbed.

β_K<1 ⟺ q_K(K−1)<K−2+q_K ⟺ q_K<1. This proves E_{K,c}(X) ≪_{K,c,ε} X^{β_K+ε} = o(X).

Sanity check: formally substituting K=2 gives exponent exactly 1, not o(X) — the mechanism starts
exactly at degree 3, consistent with the known negative quadratic case.

### 7. From o(X) avoidance to a tiling complement

[Elementary] For every finite C⊂ℤ\B_K, the number of 1≤n≤X bad for at least one c∈C is at most
Σ_{c∈C} E_{K,c}(X) = o(X). So some n simultaneously has (C−n^K)∩D_K=∅. Standard greedy: enumerate
ℤ, maintain disjoint translates a+B_K covering m_1,...,m_{j−1}; if m_j uncovered, C_j={m_j−a}⊂ℤ\B_K
(every element outside B_K since m_j uncovered); choose n avoiding all of C_j; add a*=m_j−n^K. No
collision by construction. Union over all stages gives A⊕B_K=ℤ. No uniformity in growing C_j
required.

### 8. Singular-fiber and identity audit

Not needed for the main proof, but classified because this is exactly where the cubic identity
came from.

**8.1 Singular condition.** [Elementary] C_{h,c}: Z^K=c+(A+h)^K−A^K. Point at infinity is smooth.
Affine singularity needs Z=0 and (A+h)^{K−1}=A^{K−1}. Write q=(A+h)/A, q^{K−1}=1, q≠1, A=h/(q−1).
Then c=−h^K/(q−1)^{K−1} (15), q∈μ_{K−1}\{1}. Every such repeated root is exactly double (a
simultaneous second-derivative vanishing would force q=1).

**8.2 Even degrees.** K even ⟹ K−1 odd. For q=e^{2πij/(K−1)}: (q−1)^{K−1} =
(2sin(πj/(K−1)))^{K−1} i^{K−1} (−1)^j — nonzero and purely imaginary (i^{K−1} for K−1 odd is always
±i). Since c/h^K is rational, (15) can never hold. So for K=4,6,8,10,12, every fixed-gap curve is
smooth.

**8.3 Odd degrees 5,7,9,11.** Rational singular values of c (computed via (15) over μ_{K−1}\{1}):
K=5: c=h^5/4 or c=−h^5/16. K=7: c=−h^7, c=h^7/27, c=−h^7/64. K=9: c=−h^9/16, c=−h^9/256. K=11:
c=−h^11/1024. For fixed c, each relation determines at most one positive h — singular gaps stay
O_K(1), don't proliferate with X. The K=7 fiber c=−h^7 is irrelevant to finite avoidance since
−h^7=(−h)^7∈B_7.

**8.4 Why the cubic identity does not recur.** [AG: Riemann–Hurwitz] Generic normalization of
Z^K=P(A), deg P=K−1, has genus g_0=(K−1)(K−2)/2. If a singular value produces s distinct double
roots, RH gives g=g_0−s(K−1)/2. Smallest normalization genus per K: K=4→3, K=5→2, K=6→10, K=7→9,
K=8→21, K=9→20, K=10→36, K=11→40, K=12→55. Contrast: cubic generic genus is 1, single double-root
degeneration drops it to 0 — exactly why the cubic exceptional fiber becomes the monomial cusp
k³=λu² with a polynomial parametrization. For K=4..12, every fixed-gap normalization has genus
≥2, so no nonconstant polynomial parametrization of a fixed-gap exceptional fiber can exist (would
induce a nonconstant map P^1→(positive-genus curve), forbidden by Riemann-Hurwitz). This doesn't
claim every imaginable higher-degree identity on the full diagonal surface has been classified —
it says the cubic-style fixed-gap mechanism disappears; other non-special families are already
inside Heath-Brown's quantitative count.

### 9. Degree-by-degree verdicts (all exponents mean +ε)

K=4: H=X^{26/29}, β=27/29, HB1, FULL PROOF.
K=5: H=X^{35/39}, β=12/13, HB1, FULL PROOF.
K=6: H=X^{44/49}, β=45/49, HB1, FULL PROOF.
K=7: H=X^{53/59}, β=54/59, HB1, FULL PROOF.
K=8: H=X^{62/69}, β=21/23, HB1, FULL PROOF.
K=9: H=X^{71/79}, β=72/79, HB1, FULL PROOF.
K=10: H=X^{80/89}, β=81/89, HB1, FULL PROOF.
K=11: H=X^{89/99}, β=10/11, HB1, FULL PROOF.
K=12: H=X^{54/65}, β=11/13, HB2, FULL PROOF.

### 10. Adversarial self-audit (from the source)

Weakest external link: BHB must be uniform over the changing family Φ_{h,r}. The primary source
declares implied constants depend only on degree and ε; points are automatically primitive; the
monomial A^{K−1}W gives the needed T lower bound.

Weakest internal link: absolute irreducibility. The degree-at-infinity argument is stronger than a
singularity check and covers every fiber; worth independent scrutiny but no gap currently seen.

Exceptional-solution link: relies on Heath-Brown's explicit diagonal "apart from special solutions"
conclusion (stated for every K≥3, proof invokes FLT to show linear diagonal parameterizations are
special) rather than independently rebuilding his parameterization analysis.

Semantic link: even-degree conclusions are for uniqueness of the image value b∈f(ℤ). Under
uniqueness of the integer parameter k, the even monomials fail immediately.

Not independently redone: the determinant methods in HB and BHB themselves. Everything surrounding
their application — parity split, gap bounds, residue counts, curve irreducibility, box weights,
special-solution elimination, exponent balance, greedy construction — derived directly here.

## Refutation targets

## Refutation targets

### Target 1 — the semantic pin

Independently verify: is "exactly one a∈A and b∈{f(k):k∈ℤ}" (the actual erdosproblems.com LaTeX,
already checked by us) really about uniqueness of the VALUE b, not the pair (a,k)? If pair-
uniqueness were intended, does that make the ALREADY-PUBLISHED degree-2 negative result trivial in
a way that seems inconsistent with it being a real (AlphaProof-assisted) proof? Try to find any
reading of the problem, or any comment/discussion on the erdosproblems.com page, that contradicts
the value-uniqueness reading. Does K=3 (our closed cubic case) implicitly rely on this same
semantic reading, or is it moot there because k↦k³ is injective? (Should be moot — confirm.)

### Target 2 — absolute irreducibility, is it REALLY unconditional

Re-derive the Kummer-theory argument (Z^K=P(A) irreducible over ℂ(A) for every h,c) completely
from scratch. Specifically stress-test:
- The classical Vahlen–Capelli theorem for irreducibility of X^n−a has an extra exceptional case
  when 4|n (a ∈ −4F⁴). Does that caveat actually vanish here because ℂ(A) contains i, or is there
  a subtlety being missed? (We checked this ourselves and believe it vanishes — −4b⁴=(2ib²)² is
  itself a square when i∈F, so it's already covered by the "not a p-th power" criterion for p=2 —
  but re-derive this independently rather than trusting our check.)
- Does the argument secretly require h to be coprime to K, or K to be squarefree, or any other
  hidden condition not stated? Walk through K=4, K=8, K=9 specifically (K with repeated prime
  factors: 4=2², 8=2³, 9=3²) and check the argument's each step still goes through.
- Is P_{h,c}(A)=c+(A+h)^K−A^K really ALWAYS of degree exactly K−1 with leading coefficient Kh
  (nonzero since h≥1)? Any K or h where this degenerates?

### Target 3 — the genus / Riemann-Hurwitz argument

Independently recompute the normalization genus for the singular fibers at K=4 through 12 (the
table in §8.4: genus 3,2,10,9,21,20,36,40,55 for K=4..11 respectively, plus K=12). Does the
Riemann-Hurwitz computation (genus g = g_0 − s(K−1)/2 for s double roots, g_0=(K−1)(K−2)/2 generic
genus) actually apply correctly here — in particular, is the CLAIM "genus ≥2 blocks nonconstant
maps from P^1" being used correctly (this itself is standard — any nonconstant map FROM P^1 forces
the TARGET's genus to be 0, by Riemann-Hurwitz applied with the source having genus 0 — confirm
this direction is right, not misapplied)? Is it definitely true that EVERY singular fiber at every
K in 4-12 has only finitely many double roots contributing (never enough simultaneous degenerating
roots to push the genus down to 0 or 1)? Check at least K=4 and K=8 (both divisible by 4, where
multiple simultaneous singular conditions might coincide) explicitly by hand.

### Target 4 — the exponent table, remaining rows

We independently verified rows K=4, 7, 11, 12 by hand (all exact matches to the closed-form
α_K, β_K). Verify the remaining rows: K=5, 6, 8, 9, 10. Also re-derive the general balancing step
in §6 (setting small-gap exponent = large-gap exponent, solving for α_K) completely from scratch —
is the claimed closed form definitely the correct optimum, or could a different split of the gap
cutoff H do better (irrelevant to correctness, since ANY valid o(X) bound suffices for finite
avoidance, but worth confirming the claimed exponents are at least achievable, not overclaimed)?

### Target 5 — is the K=4..12 range genuinely exhaustive, or does something break silently in the middle

The proof presents K=4..12 as uniformly handled by one mechanism (HB1) except K=12 (HB2). Hunt
specifically for any K in this range where an assumption silently fails — e.g., h=0 edge cases,
the "opposite sign vs same weak half-line" split for odd K missing a configuration (x=0 or y=0),
or the residue-count lemma (§4.1) failing for K sharing a prime factor with h in some
uncovered way. If you find nothing, say so explicitly rather than passing over it quickly — this
target is specifically about NOT trusting the smoothness of the table just because the endpoints
check out.

### Target 6 — special solutions for even K, completeness

Re-verify §5.1's case analysis (special solutions requiring c∈B_K, for both c>0 and c<0, both odd
and even K) is exhaustive. In particular the even-K, c<0 sub-case ends with "n=a=0, whereas n≥1" —
confirm this really closes off every possibility and isn't quietly assuming something about which
variable is which.

## House rules

Rigor-label every claim. Adversarial self-audit naming your own weakest link — not the source's.
An honest "I found a real gap," "I couldn't break it," or "I found a fix for a real gap" are all
valuable. End with a labeled verdict (REFUTED / GAP FOUND-BUT-FIXABLE / SURVIVES SCRUTINY / COULD
NOT DETERMINE) per target, and an overall verdict.
