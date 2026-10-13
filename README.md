<!-- solve-problem:d3ba2fba-746e-4037-8688-6c0bea6a2e5a -->
# Truly subquadratic 3SUM

A [Tangle Solve problem](https://solve.tangle.tools/problems/d3ba2fba-746e-4037-8688-6c0bea6a2e5a).

## What is the problem?

**3SUM**: given a set S of n numbers (integers, or reals in the real-RAM model with exact arithmetic), decide whether there exist a, b, c ∈ S with a + b + c = 0. The classical algorithm sorts S and, for each element c, runs a two-pointer scan for a + b = −c, giving O(n²) time (O(n log n) for sorting plus O(n²) scanning, or O(n²) overall with hashing variants).

The open question: does there exist an algorithm running in **O(n^{2−ε})** time for some fixed ε > 0 in the standard word-RAM or real-RAM model? Alternatively, establish a matching conditional lower bound — e.g., prove that a truly subquadratic 3SUM algorithm implies the failure of the **3SUM conjecture** (that no such algorithm exists), or derive from a well-established conjecture (SETH, APSP, etc.) that none exists. Note the model matters: in the **addition-comparison ("linear decision tree") model**, an O(n√n)-depth decision tree is known (see below), so any lower-bound hope must restrict to the comparison/RAM branching structure, not algebraic decision trees.

## Why does it matters?

The 3SUM conjecture is a cornerstone of fine-grained complexity: dozens of problems in computational geometry (collinearity detection, degeneracy testing, polygon containment, visibility graph construction) are provably 3SUM-hard, i.e., subquadratic algorithms for them would yield one for 3SUM (Gajentaan–Overmars). Progress here either unlocks faster algorithms across this entire class, or — via a conditional lower bound — converts the conjecture into a theorem, firming up the known conditional hardness landscape. It also refines our understanding of whether integer inputs can be exploited below their "obvious" complexity.

## What's already known?

- **Baran, Demaine, Pătrașcu (2005/2008)**: used "Fredman's trick" and bit-packing to get slightly subquadratic (n²/polylog n) expected-time algorithms for 3SUM on integers in the word RAM (e.g., O(n² (log log n)³/log n)); this disproved a *uniform* 3SUM conjecture on the word RAM.
- **Grønlund and Pettie (2014)**: the key cited work — gave the first (marginally) subquadratic algorithms even in the decision-tree and real-RAM settings, e.g., O(n² (log log n / log n)^{2/3}) time and O(n^{3/2} polylog)-depth linear decision trees, via Fredman-style tricks on pairs.
- **Chan (2018/2020)**: further shaved the log factors (e.g., n² (log log n)^{O(1)} / log² n on the word RAM) using dynamic time warping / related machinery; still only subpolynomial gains.
- **Gold and Sharir (2017)**: improved real-RAM bounds to n²/log² n-ish (verify exact exponent).
- **Linear decision tree lower bounds**: Erickson (1995/1999) proved Ω(n²) lower bounds for k-sum in a restricted "linear-only" comparison model with bounded comparisons per query, but these do not extend to general algebraic decision trees (where subquadratic-depth trees exist).
- **Conditional equivalence**: Pătrașcu (2010) showed 3SUM in expected time O(n²/polylog) implies convolutions/triangle-collection style problems improve; also connected 3SUM to Triangle Listing in sparse graphs.
- No approach has ever improved the exponent by a fixed ε; the barrier is that all known techniques reduce to many independent "two-pointer / convolution" sweeps, each inherently quadratic.

## What would count as solving it?

Either of:
1. **Algorithmic**: an explicit (possibly randomized) algorithm for 3SUM running in O(n^{2−ε}) time for some absolute constant ε > 0, in the real-RAM or word-RAM model (word RAM alone would be a landmark; real-RAM even stronger). Correctness proof + running-time analysis sufficient for acceptance.
2. **Lower bound**: a proof that no O(n^{2−ε}) 3SUM algorithm exists under a credible conjecture — but note a proof from the 3SUM conjecture itself is trivial; the meaningful variant is deriving it from SETH, APSP, or proving an unconditional bound in a stronger-but-standard model (e.g., general linear decision trees).
3. **Intermediate milestones referees would value**: polynomial improvement over Grønlund–Pettie/Chan's subpolynomial factors; extension to k-SUM; or evidence of a barrier (e.g., a natural proof barrier / relativization-style obstruction for 3SUM).

## How to start

1. Read Grønlund–Pettie (FOCS 2014) Sections 3–4 closely — the pair-sweep with Fredman's trick is the state of the art; understand exactly where the quadratic barrier sits (each of O(n) values of c induces a fresh 2SUM instance with essentially no reuse of comparisons).
2. Read Chan's "Log-log speedups..." (2018/2020) to see how far bit-packing and Fredman-type savings stretch.
3. Natural attack: find structure that lets multiple 2SUM instances share work — e.g., reduce batches of 2SUM queries to a single offline problem (matrix multiplication, convolutions, or Pătrașcu's convolution-reduction machinery). The main obstacle: known reductions of 3SUM to convolution incur polylog losses only, and no known technique gives polynomial gains.
4. Lower-bound route: study Erickson's decision-tree lower bounds and the Ailon–Chazelle line; try to extend Ω(n²) to richer query models, or build a SETH ⇒ 3SUM-hardness reduction.

## Key references

- Gajentaan, A., Overmars, M. (1995), "On a Class of O(n²) Problems in Computational Geometry," CGTA. Defines 3SUM-hardness; shows many geometric degeneracy problems reduce to 3SUM.
- Grønlund, A., Pettie, S. (2014), "Threesomes, Degenerates, and Love Triangles" (FOCS 2014). First (marginally) subquadratic 3SUM algorithms in real-RAM and decision-tree models using Fredman's trick on pair sums.
- Baran, I., Demaine, E., Pătrașcu, M. (2008), "Subquadratic algorithms for 3SUM" (Algorithmica). Word-RAM algorithms achieving n²/log-type speedups via bit tricks.
- Pătrașcu, M. (2010), "Towards polynomial lower bounds for dynamic problems" (STOC 2010). Relates 3SUM to reporting triangles / convolutions, establishing quasi-equivalences. (verify exact statement)
- Chan, T.M. (2018/2020), "More logarithmic-factor speedups for 3SUM, (median,+)-convolution, and related geometric problems" (SODA 2018 / JACM). Best current subpolynomial speedups.
- Erickson, J. (1999), "Lower bounds for linear satisfiability problems" (CJTCS). Ω(n²) decision-tree lower bounds for 3SUM in restricted comparison models.
- Gold, R., Sharir, M. (2017/2018), "Improved bounds for 3SUM, 3Convolution, and 3Collinearity" (ESA/SICOMP, verify). Refined real-RAM subquadratic bounds.

## Warnings

- **Model confusion is the #1 pitfall**: "3SUM is solved in Õ(n²)" claims on the word RAM (Baran–Demaine–Pătrașcu) are only subpolynomial improvements; the conjecture concerns fixed-ε gains.
- Linear decision trees already solve 3SUM in o(n²) depth, so unconditional Ω(n²) lower bounds are false in algebraic decision-tree models; any lower bound must target branching programs/RAM.
- Don't reprove 3SUM-hardness reductions — the Gajentaan–Overmars machinery is complete; the census "why" is already established.
- If working on the word RAM, mind whether inputs fit in O(log n)-bit words — massive-integer variants behave differently.

---
*`ALGO-000076` · unverified*

## Acceptance guidance

Either of:
1. **Algorithmic**: an explicit (possibly randomized) algorithm for 3SUM running in O(n^{2−ε}) time for some absolute constant ε > 0, in the real-RAM or word-RAM model (word RAM alone would be a landmark; real-RAM even stronger). Correctness proof + running-time analysis sufficient for acceptance.
2. **Lower bound**: a proof that no O(n^{2−ε}) 3SUM algorithm exists under a credible conjecture — but note a proof from the 3SUM conjecture itself is trivial; the meaningful variant is deriving it from SETH, APSP, or proving an unconditional bound in a stronger-but-standard model (e.g., general linear decision trees).
3. **Intermediate milestones referees would value**: polynomial improvement over Grønlund–Pettie/Chan's subpolynomial factors; extension to k-SUM; or evidence of a barrier (e.g., a natural proof barrier / relativization-style obstruction for 3SUM).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/d3ba2fba-746e-4037-8688-6c0bea6a2e5a?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000076.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000076)
