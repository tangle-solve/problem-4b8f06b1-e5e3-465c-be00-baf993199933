<!-- solve-problem:4b8f06b1-e5e3-465c-be00-baf993199933 -->
# BPP equals P

A [Tangle Solve problem](https://solve.tangle.tools/problems/4b8f06b1-e5e3-465c-be00-baf993199933).

## What is the problem?

Determine whether BPP = P: can every randomized algorithm that runs in polynomial time and errs with probability ≤ 1/3 be replaced by a deterministic polynomial-time algorithm computing the same function?

Formal setting: BPP is the class of languages L ⊆ {0,1}* decided by a probabilistic Turing machine M(x; r) running in poly(|x|) time, with Pr_r[M(x;r) accepts] ≥ 2/3 for x ∈ L and ≤ 1/3 for x ∉ L, over uniformly random coins r ∈ {0,1}^{m(|x|)}, m polynomial. The question: does there exist, for every such L, a deterministic machine running in poly(|x|) time deciding L?

The standard approach via derandomization: construct a pseudorandom generator G: {0,1}^s → {0,1}^m with s = O(log n) and seed length so small that enumerating all 2^s = poly(n) seeds and simulating M deterministically costs poly(n). Such a generator must fool every polynomial-time algorithm — equivalently (by standard characterizations) every polynomial-size circuit family. The problem is unconditional: no assumptions about hardness are permitted in the final answer.

Note: the answer is widely conjectured to be yes, so the real task is proving BPP ⊆ P (the reverse inclusion P ⊆ BPP is trivial). A proof of separation (BPP ≠ P) would be a major (unexpected) breakthrough.

## Why does it matter?

This is the central question of derandomization: it determines whether randomness gives any inherent polynomial-time speedup, and resolves the fate of hundreds of randomized algorithms (primality was already derandomized by AKS; most others were not). A proof requires either an unconditional PRG construction (advancing pseudorandomness far beyond current techniques) or lower bounds against circuits — which would also yield major complexity separations (e.g., progress toward P ≠ NP-type results, since NEXP ⊄ P/poly would follow from optimal derandomization of nondeterministic classes). Conversely, even circuit lower bounds are known to follow from derandomization, so this problem is a two-way bridge between algorithms and lower bounds.

## What's already known?

- **Hardness vs randomness (Nisan–Wigderson 1994):** If a function in E = DTIME(2^{O(n)}) requires 2^{Ω(n)}-size circuits, then BPP = P. More generally, hardness H (against circuits of size S) yields PRGs with seed length roughly m/poly for functions with hardness S.
- **Impagliazzo–Wigderson 1997:** The assumption weakens to E requiring 2^{Ω(n)} circuits for infinitely many input lengths; moreover, worst-case hardness can be amplified to average-case hardness via the Impagliazzo hardcore-set lemma, so worst-case circuit lower bounds for E suffice.
- **Known unconditional PRGs:** Nisan's generator fools space-bounded computation with seed O(log^2 n), giving RL vs SC-type results, but no unconditional PRG with O(log n) seed fooling all of polynomial time exists.
- **Black-box barriers:** Work on the limits of black-box derandomization (e.g., the "easy witness lemma" of Impagliazzo–Kabanets–Wigderson, showing general derandomization implies circuit lower bounds: BPP = P essentially requires NEXP ⊄ P/poly-type results) shows the problem cannot be solved without proving circuit lower bounds that currently elude us.
- **Partial results:** BPP ⊆ Σ_2^P ∩ Π_2^P (Sipser–Gács–Lautemann); BPP ⊆ P/poly (Adleman); derandomization of specific algorithms (AKS for primality); nondeterministic PRG-based barriers (KLW10-type "easy witness" methods).

Why approaches fall short: constructing the needed PRG requires average-case hardness in E, and the best known circuit lower bounds (e.g., ~5n for explicit functions against general circuits) are exponentially far from 2^{Ω(n)}.

## What would count as solving it?

- **Positive resolution:** A proof that BPP ⊆ P — e.g., an explicit PRG family with seed length c·log n fooling all polynomial-size circuits, or a direct deterministic simulation argument, with no unproved assumptions.
- **Negative resolution:** A proof that P ≠ BPP, i.e., a language with a polynomial-time randomized algorithm but no deterministic one (would be shocking; requires techniques far beyond current lower bounds).
- **Intermediate publishable targets** (not full solutions but referee-acceptable progress): weaker derandomization such as BPP ⊆ io-SubEXP, derandomizing specific subclasses (RP, BP·subclasses), improving seed length under weaker hardness assumptions, or proving new circuit lower bounds for E (e.g., 2^{εn} for some explicit function — the census-record line of IW97 shows even this suffices).

## How to start

1. Read the Impagliazzo–Wigderson 1997 paper first (STOC '97), especially the statement "P = BPP if E requires exponential circuits," and the hardcore-set lemma; this gives the exact reduction you'd need to power.
2. Read Nisan–Wigderson 1994 (JCSS) to understand the PRG design paradigm (design matrices + hard function) and where its analysis is tight.
3. Internalize the easy-witness barrier (Impagliazzo–Kabanets–Wigderson 2002) to understand why "pure algorithmic" derandomization cannot avoid circuit lower bounds — this tells you any attack must either prove lower bounds or evade black-box reasoning.
4. Natural approach: try to weaken the required hardness (e.g., derandomization from worst-case lower bounds against weaker circuit classes, or via ``#SAT/satisfiability algorithms'' à la Kabanets–Impagliazzo connections between Circuit-SAT algorithms and derandomization). Main obstacle: no known technique proves 2^{Ω(n)} lower bounds for explicit functions against general circuits; the natural proofs barrier (Rudich– Razborov) blocks many candidates.

## Key references

- Nisan, N., Wigderson, A. (1994). "Hardness vs Randomness." JCSS 49(2):149–167. Establishes the hardness-vs-randomness framework: constructs PRGs from hard functions, showing circuit hardness in E implies BPP = P.
- Impagliazzo, R., Wigderson, A. (1997). "P = BPP if E Requires Exponential Circuits: Derandomizing the XOR Function." STOC '97. Shows worst-case exponential circuit lower bounds for E suffice (via the hardcore lemma), strengthening NW94 to 2^{Ω(n)} worst-case hardness.
- Impagliazzo, R. (2003). "Hardness as Randomness: A Survey of Universal Derandomization." arXiv:cs/0304040. Survey of the hardness-vs-randomness program and open problems around BPP vs P. (link: https://arxiv.org/abs/cs/0304040)
- Impagliazzo, R., Kabanets, V., Wigderson, A. (2002). "In Search of an Easy Witness: Exponential Time vs. Probabilistic Polynomial Time." JCSS 65(4). Shows derandomization of MA (and related classes) implies circuit lower bounds — the key barrier to unconditional BPP = P. (verify exact statement/venue details)

## Warnings

- P ⊆ BPP trivially; only BPP ⊆ P needs proof — don't spend effort on the wrong direction.
- Do not "prove" BPP = P from an unproved hardness assumption; the problem demands an unconditional result. Many papers conditionally derandomize — that is known territory.
- The easy-witness lemma means full derandomization entails circuit lower bounds (roughly, NEXP ⊄ P/poly or similar); any proposal avoiding lower bounds must explain how it evades black-box barriers.
- Natural proofs (Razborov–Rudich): any lower-bound-based route must confront this barrier; "natural" hardness measures against general circuits are ruled out under standard one-way-function assumptions.
- Constant 1/3 error is immaterial (amplification); the distinction that matters is polynomial vs. superpolynomial deterministic simulation time — "derandomization to SubEXP" is weaker and itself open in general.

---
*`ALGO-000050` · unverified*

## Acceptance guidance

- **Positive resolution:** A proof that BPP ⊆ P — e.g., an explicit PRG family with seed length c·log n fooling all polynomial-size circuits, or a direct deterministic simulation argument, with no unproved assumptions.
- **Negative resolution:** A proof that P ≠ BPP, i.e., a language with a polynomial-time randomized algorithm but no deterministic one (would be shocking; requires techniques far beyond current lower bounds).
- **Intermediate publishable targets** (not full solutions but referee-acceptable progress): weaker derandomization such as BPP ⊆ io-SubEXP, derandomizing specific subclasses (RP, BP·subclasses), improving seed length under weaker hardness assumptions, or proving new circuit lower bounds for E (e.g., 2^{εn} for some explicit function — the census-record line of IW97 shows even this suffices).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/4b8f06b1-e5e3-465c-be00-baf993199933?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000050.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000050)
