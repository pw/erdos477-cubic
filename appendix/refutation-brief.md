# Dyad brief — Erdős #477, ADVERSARIAL REFUTATION of the claimed cubic density-1 proof

**Seat:** ChatGPT Pro, max reasoning effort. Fresh chat — treat everything below as a claim to
be attacked, not ground truth to build on. A different Pro instance (same subscription, separate
session) produced the proof below in response to `erdos477_FA_multiC.md` (which asked only for
"finite-avoidance for |C|≥2," i.e. simultaneous good k for finitely many targets — the response
came back with a much stronger unconditional density-1 claim, via completely different machinery
than what that brief suggested). Your job is to try to break it, specifically at two points a
careful independent check (done on our end, by Claude, against the actual primary-source PDFs —
not just abstracts) could not fully close. Full honesty > a clean verdict. An honest "I found the
gap" or "I couldn't break it either" are both valuable — a false "confirmed" is the only bad
outcome.

## The problem (erdosproblems.com #477, OPEN for degree ≥3)

Exact statement, from the site's LaTeX source (verified primary, not paraphrase): *Is there a
polynomial f:ℤ→ℤ of degree at least 2 and a set A⊂ℤ such that for any n∈ℤ there is exactly one
a∈A and b∈{f(k):k∈ℤ} such that n=a+b?* Erdős and Graham conjectured NO. Degree 2 is fully killed
(Jan 2026, AlphaProof+Adenwalla, published on the site). Degree ≥3 is open.

**Important adversarial context you should weigh, not just verify the algebra:** the DeepMind
`formal-conjectures` Lean repository's formalization of this exact sub-case
(`FormalConjectures/ErdosProblems/477.lean`, `erdos_477.variants.X_pow_three`) states it as
*"Probably there is no such A for the polynomial X³,"* citing Sekanina (1959), "Remarks on the
factorization of an infinite cyclic group," Czechoslovak Math. J. 9. That is the standing expert
guess, and it's the OPPOSITE of what the proof below claims (existence, at density 1). This
doesn't make the proof wrong, but it raises the bar — if you can find or recall anything about
why a Sekanina-style factorization-of-ℤ obstruction would apply to cubes specifically, surface it.

## What's already independently established (this thread, tonight, verified — for context only)

- Cubic difference sets are sparse: |{f(x)−f(y)}∩[−N,N]| = O(N^{2/3}) for cubic f.
- FA (finite-avoidance) reduction: if for every finite C⊂ℤ\B there's a k with (C−k³)∩D=∅ (D=B−B,
  B={k³:k∈ℤ}), a greedy argument builds a full exact complement A. This is the same reduction the
  proof below reproves independently (their Lemma 1.7 ≈ our FA reduction) — good cross-check,
  worth confirming they match.
- THEOREM A (proved, |C|=1 case, unconditional, elementary mod-p argument — NOT the machinery
  used below): for every single c∉B, infinitely many k have c−k³∉D.
- **A known genuine exceptional family, found independently by two different methods tonight:**
  c=−2 has the infinite family (6t³−1)³+(6t²)³−(6t³+1)³=−2 for all t (found via direct algebraic
  identity search). The proof below independently rediscovers essentially the same family as a
  "singular fiber" at c=−2 (their §4, condition d³+4σc=0) via completely different (determinant-
  method) machinery, and this also matches Heath-Brown's own published example (his 2009 J.
  Number Theory paper opens with the identity (6t³+1)³+(−6t³+1)³−(6t²)³=2, the c=+2 sibling).
  **This three-way agreement is a real point in the proof's favor — flag it, don't just look for
  holes; calibrate accordingly.** But also check: does the proof's mechanism (indexed by a single
  auxiliary parameter d=v−u, one exceptional fiber per (d,σ) with d³+4σc=0) provably catch EVERY
  such degree-1-or-higher exceptional family on the original surface k³+x³−y³=c, or only the ones
  visible through that specific factorization? (This is refutation target 3 below.)

## THE CLAIM UNDER TEST — reproduce and attack this

*(Source text below has some OCR/PDF-extraction glyph corruption from how it reached us — ↑=∈,
↔=− (minus) or ⊂/→ depending on context, ≃=≥, →=maps-to or "gives", ⇓↓=↦. Reconstruct standard
math notation from context; a garbled glyph is not grounds to dodge a step — if a specific
substitution is genuinely ambiguous, say so explicitly rather than guessing silently.)*

---

# Cubic FA has density one

I think this closes the cubic case—and therefore the original problem—with (f(k)=k^3).

## Two corrections to the setup

**[Fully elementary] The literal FA statement must exclude cubes.**
If (c=t^3∈B:={k^3:k∈ℤ}), then for every (k),
[
c−k^3=t^3−k^3∈D:=B−B.
]
So FA cannot hold for every finite (C⊂ℤ). The correct version is:

[
C⊆ℤ∖B.
]

That is exactly enough for the greedy construction: if (n) is not yet covered and (a∈A), then (n−a∉B), or else (n=a+(n−a)) was already covered.

**[Fully elementary] The stated congruence classification is false as written.**
Modulo both (7) and (9), the differences of cubes are
[
{0,±1,±2},
]
not merely ({0,±1}). Indeed,
[
1^3−(−1)^3=2.
]
This correction is orthogonal to the argument below.

---

## Main quantitative theorem

**[Relies on two named determinant-method theorems; all reductions around them are elementary]**

For a fixed noncube (c∈ℤ∖B), define
[
E_c(X):=
#{k∈ℤ:|k|≤X,\ c−k^3∈D}.
]

Then, for every (ε>0),
[
E_c(X)≪_{c,ε}X^{18/19+ε}.
\tag{T}
]

Consequently,
[
#{1≤k≤X:c−k^3∉D}=X+O_{c,ε}(X^{18/19+ε}),
]
so (G_c) has natural density (1), not merely positive density.

Even better, for every finite (C⊂ℤ∖B),
[
#{1≤k≤X: c−k^3∉D\ \text{for every }c∈C}=X+O_{C,ε}(X^{18/19+ε}).
\tag{FA_dens}
]
Thus the simultaneous good set has density (1).

---

# Proof of (T)

A bad (k) has some (x,y∈ℤ) satisfying
[
c−k^3=x^3−y^3,
]
or equivalently
[
c=k^3+x^3−y^3.
\tag{1}
]

Put (L=max(|x|,|y|)). Fix a parameter (η>0), split representations by (L≤X^{1+η}) or (L>X^{1+η}).

## 1. Moderate representations

**[Named theorem: Heath-Brown, 2008]**

D. R. Heath-Brown proves that for a nonsingular diagonal ternary form of degree (3), the number of
nonspecial integer solutions with variables of size at most (B) and with fixed bounded form value is
O_ε(B^{9/10+ε}). More precisely, his theorem gives O(B^{9/10+ε}N^{1/10}) for (|F|≤N); here (N=|c|)
is fixed. He defines the exceptional "special" solutions as those in which one signed cube
individually equals the target value.

Apply this to F(k,x,y)=sgn(c)(k^3+x^3−y^3), F(k,x,y)=|c|. There are no special solutions: if one of
the signed terms equals (|c|), then (c) itself is an integer cube, contrary to the hypothesis.

After a dyadic decomposition, the number of triples with (|k|≤X, L≤X^{1+η}) is
[
≪_{c,ε}(X^{1+η})^{9/10+ε}=X^{\frac9{10}(1+η)+ε}.
\tag{2}
]

## 2. Large representations: a small difference parameter

Suppose (L>X^{1+η}). Let (m=k^3−c, σ=sgn(m)) (nonzero since c is not a cube). Write
(|m|=v^3−u^3, d=v−u>0, s=v+u) (after interchanging x,y if needed). The identity
(4(v^3−u^3)=(v−u)((v−u)^2+3(v+u)^2)) gives
[
4σ(k^3−c)=d(d^2+3s^2).
\tag{3}
]
Since (u^2+uv+v^2≥\frac34 max(|u|,|v|)^2=\frac34 L^2) and (|k^3−c|=d(u^2+uv+v^2)),
[
d≤\frac{4|k^3−c|}{3L^2}≪_c\frac{X^3}{X^{2+2η}}=X^{1−2η}.
\tag{4}
]

## 3. Fix d, split k into residue classes

(3) implies (d∣4(k^3−c)). For each residue (r\bmod d) with (d∣4(r^3−c)), write (k=r+dt). Dividing
(3) by (d) and homogenizing with (w) gives the ternary cubic
[
F_{d,r,σ}(w,t,s)=4σd^2t^3+12σdrt^2w+12σr^2tw^2+\left(\frac{4σ(r^3−c)}d−d^2\right)w^3−3s^2w.
\tag{7}
]
(the coefficient in parentheses is integral by construction). Every relevant solution gives a
primitive integral point (w,t,s)=(1,t,s) on (F_{d,r,σ}=0).

## 4. Nonsingularity and the exceptional fibers

Set (K=rw+dt). Multiplying (7) by (d), the curve becomes
[
4σK^3−3ds^2w−(d^3+4σc)w^3=0.
\tag{8}
]
A direct check (computing partials of (8) and finding common zeros) shows this projective cubic is
nonsingular precisely when (d^3+4σc≠0). A nonsingular plane cubic is absolutely irreducible.

**Singular fiber:** if (d^3+4σc=0), then (3) simplifies to (4σk^3=3ds^2), forcing (|k|=κu^2) for a
fixed squarefree (κ=κ(c,d)) — square-root density only, i.e. O_c(X^{1/2}) possible k. This
identifies the c=−2 example: (σ=1,d=2), (2^3+4(−2)=0), giving k=6u^2.

## 5. Count the nonsingular fibers via a plane-curve box theorem

Choose r centered mod d: (|t|≪X/d=:T_d). From (3): (3ds^2≤4|k^3−c|≪_c X^3), so
(|s|≪_c X^{3/2}d^{-1/2}=:Y_d).

Use the (P_1=1) plane-curve-in-a-box estimate, formula (3) of Browning–Heath-Brown ("Plane curves
in boxes and equal sums of two powers"): for absolutely irreducible F and (1≤P_2≤P_3),
[
N(F;1,P_2,P_3)≪_ε P_3^ε\exp\left(\frac{\log P_2\log P_3}{\log 𝒯}\right),
\tag{14}
]
where 𝒯 is the largest box-weight of a monomial occurring in F with nonzero coefficient, and the
implied constant depends only on the degree and ε — NOT on the coefficients of F.

For (7), the monomial (s^2w) occurs, so (𝒯≥Y_d^2), giving
[
\exp\left(\frac{\log T_d\log Y_d}{\log 𝒯}\right)≤\exp(\tfrac12\log T_d)=T_d^{1/2}.
]
So, per nonsingular (d,r,σ):
[
#{(t,s):F_{d,r,σ}(1,t,s)=0}≪_{c,ε}X^{1/2+ε}d^{-1/2}.
\tag{15}
]

## 6. Number of admissible residue classes

Let (R_c(d)=#{r\bmod d: d∣4(r^3−c)}). Via Hensel lifting (for p∤3c, ≤3 roots mod p, unique lift to
p^e; for the finitely many primes dividing 3c, bounded independent of e by a valuation argument),
(R_c(d)≪_{c,ε}d^ε).

## 7. Sum over d

Combining (4), (15), (16):
[
X^{1/2+ε}\sum_{d≪X^{1-2η}}d^{-1/2+ε}≪_{c,ε}X^{1/2+ε}(X^{1-2η})^{1/2+ε}≪_{c,ε}X^{1-η+ε}.
\tag{17}
]
Adding the singular contribution O(X^{1/2}):
[
E_c(X)≪_{c,ε}X^{\frac9{10}(1+η)+ε}+X^{1-η+ε}+X^{1/2}.
\tag{19}
]
Balancing the first two exponents: (η=1/19), giving (E_c(X)≪_{c,ε}X^{18/19+ε}). ∎(T)

# Finite avoidance and the greedy construction

[Fully elementary, standard union bound over C, then a greedy enumeration of ℤ building
A_0⊂A_1⊂⋯ with uniqueness maintained at each step by construction — details omitted here for
length; available on request if this part specifically is in doubt.]

## The claim's own self-audit (from the source)

*"The weakest and most audit-sensitive point is the coefficient-uniform application of the
Browning–Heath-Brown box estimate (14) to the family F_{d,r,σ}, whose coefficients grow with
d,r... The second place to inspect is Heath-Brown's 'apart from special solutions' clause."*

## VERDICT CLAIMED BY THE SOURCE: FULL PROOF

---

## What Claude's independent check (against the real arXiv PDFs, not abstracts) found

- The 9/10 exponent and the "apart from special solutions only" clause for diagonal forms ARE
  genuinely printed in Heath-Brown 2008 (arXiv:0806.4330, Theorem 1 — not the more commonly-cited
  Theorem 2, which has the k-dependent 10/k exponent instead). Correctly matched.
- Recomputed the η=1/19 balance and the dyadic-sum arithmetic in §7 independently — checks out
  exactly as stated.
- Traced through the coefficients of F_{d,r,σ}: they're O(d^3)=O(X^{3(1-2η)}), i.e. polynomial in
  X, and the Browning-HB Theorem 1 proof's internal 𝒫≫...log²‖F‖ step (their eq. 16) only needs a
  LOG of the coefficient size, which is swamped by any ε>0 power-loss for polynomially-bounded
  coefficients. Verified T≥(P_1P_2)^d holds (T=Y_d^2=X^3/d ≥ T_d^3=X^3/d^3 since d≥1).
- Independently recognized (8) as a disguised Weierstrass model (s^2 ∝ cubic-in-K after dividing
  by w and rescaling) and re-derived the singularity condition d^3+4σc=0 that way — matches.

**What was NOT independently re-derived — this is your job:**

## Refutation target 1 — Heath-Brown's diagonal-form clause, completeness of the exclusion

Heath-Brown's Theorem 1 states, for diagonal ± forms, O(B^{9/10+ε}N^{1/10}) solutions "apart from
any special solutions" (special = one signed term equals N). Attack: does this literally mean NO
OTHER exceptional linear (degree-≤1-in-a-parameter) families exist on x1^3±x2^3±x3^3=N, for ANY N
in this residue-unrestricted setting? A smooth cubic SURFACE in P^3 is rational and classically
carries lines — for a Fermat-type diagonal cubic surface, are ALL of its rational lines accounted
for by the trivial "special solution" lines, or could there be OTHER rational lines (not of the
"one term=N" shape) for special N, that Heath-Brown's stated bound is implicitly assuming away
without full proof, or that only apply for N outside our relevant range? If you can find or
construct a counterexample line — or confirm from the structure of his proof (not just the
abstract) that this really is watertight — say so explicitly either way.

## Refutation target 2 — Browning–Heath-Brown box theorem, is it really over the WHOLE family

Go find the actual proof of their Theorem 1 (arXiv:math/0506497, not just the statement) and check
whether the "≪_ε" implied constant is TRULY uniform as (d,r,σ) range over the values used here —
d up to X^{1-2η}, r mod d, σ=±1, i.e., an UNBOUNDED FAMILY of curves as X→∞, not one fixed curve.
Their own paper's standard use case is a single fixed F. Is there any place in their proof
(auxiliary primes, Bézout's-theorem step, height bounds) where the implied constant secretly
depends on something about F_{d,r,σ} beyond T,P_2,P_3 — e.g. on the discriminant, or on how close
F_{d,r,σ} is to DEGENERATING (recall it's exactly nonsingular/singular depending on d,c) — that
could blow up as d approaches the exceptional value where d^3+4σc=0, even for d slightly off that
exact value? A curve that's "nonsingular but close to singular" can have pathological point counts
even when technically meeting a nonsingularity hypothesis. Push on this specifically.

## Refutation target 3 — does the (d,r,σ) factorization actually cover everything

The reduction fixes d=v−u (difference of the two OTHER cube-root variables) and stratifies by it.
Is it possible for a genuine infinite/large-density family of bad k to exist that does NOT
correspond to a single small d in this stratification — e.g., where d itself grows with k in a
way not captured by the d≪X^{1-2η} bound in step 2? Re-derive step 2's bound (4) yourself from
scratch rather than trusting the algebra as printed, since everything downstream depends on d
being confined to that range.

## Refutation target 4 — reconcile with the Sekanina "probably negative" expectation

Is there a known elementary or classical obstruction (Sekanina 1959, or anything in the
factorization-of-cyclic-groups literature) that would make "an infinite union of density-o(1)
exceptional sets can still conspire to block every simultaneous k as C grows" — i.e., a reason
the |C|→∞ (not just fixed finite C) limit of this argument could fail even though every FIXED
finite C is fine? The proof's own (FA_dens) is stated for fixed finite C only, uniform O_{C,ε}; the
actual greedy construction needs this for a SEQUENCE of growing C_j (j→∞, with |C_j|→∞ too, since
A_{j-1} grows without bound). Check the proof's own final greedy-construction section (which the
source text abbreviates) rigorously handles this — does the O_{C,ε} constant blowing up with |C|
(unstated dependence) ever threaten the "for all sufficiently large T, some k avoids every bad
condition" step at stage j, once |C_j|=j is unbounded?

## Refutation target 5 — a second, independently-run proof exists, converges, but isn't decorrelated

A separate Pro run (same subscription, different fresh chat, asked essentially the same open
question) produced a SECOND full proof, with a different case-split: splits first on sign(x,y)
(opposite sign → x,y confined directly to O(X), giving the moderate bound O(X^{9/10+ε}) with no
extra η-parameter; same sign → gap variable h=y−x, u=x+y, split at H=X^{17/19}). It cites the
IDENTICAL two theorems (Heath-Brown 2008 Thm 1, Browning–Heath-Brown formula (3)), lands on the
IDENTICAL final exponent 18/19, and its own self-audit names the IDENTICAL weakest link
(coefficient-uniformity of the box theorem across the varying curve family) as the proof above.

Two things about this: (a) it generalizes the c=−2 singular family to an explicit closed-form
identity for infinitely many c, (6ds²)³+[d(6s³−1)]³−[d(6s³+1)]³=−2d³ for all d,s≥1 — Claude
verified this EXACTLY, both algebraically (factor out d³; with a=6s³, (a−1)³−(a+1)³=−6a²−2 cancels
the 216s⁶ term to leave exactly −2) and numerically (20 random (d,s) pairs, exact integer match).
That specific claim is solid — no need to re-check it. (b) the convergence of two structurally
different decompositions on the same final bound is worth something for the ELEMENTARY parts
(exponent arithmetic, gap-parameter transforms, singular-fiber handling) but is NOT independent
evidence for refutation targets 1–2 above, since both proofs' entire power-saving content reduces
to the same two imported theorems. Don't let "two proofs agree" read as "twice as confirmed" —
it's the same crux, asked twice.

**What to actually do with the second proof:** check whether its sign-based case-split and the
first proof's size-based (L vs X^{1+η}) case-split are truly covering the same territory with no
gap between them — e.g. does the first proof's "moderate representations" branch (Heath-Brown
Theorem 1 applied over the WHOLE box regardless of x,y sign) correctly subsume what the second
proof needed the opposite-sign case split for, or is there a corner (same-sign, but with L only
moderately larger than X — i.e., h small but not covered by proof 2's H-threshold in a way that
maps cleanly onto proof 1's η-threshold) that one of them handles only by accident of exponent
slack, not by genuine case coverage? If you can map proof 1's (η, L) split onto proof 2's (H, h)
split exactly (they should be the same case space, sliced differently) and confirm both really do
cover it with no gap, that's useful. If you find a mismatch, that's a real find.

## House rules

Rigor-label every claim. Adversarial self-audit naming your own weakest link — not the source's.
An honest "I found a real gap," "I couldn't break it," or "I found a fix for a real gap" are all
valuable. End with a labeled verdict (REFUTED / GAP FOUND-BUT-FIXABLE / SURVIVES SCRUTINY /
COULD NOT DETERMINE) and one line on the state of the obstruction.
