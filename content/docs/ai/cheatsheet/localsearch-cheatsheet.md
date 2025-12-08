---
title: loaclsearch cheatsheet
description: cheatsheet
---
1. Local search evaluates **states**, not paths; works with a single current state.
2. Goal: improve current state by moving to a neighboring state.
3. Uses very little memory → typically (O(1)).

---

4. Hill climbing:

   * move to neighbor with **highest value** (or lowest cost)
   * greedy improvement
   * gets stuck in:

     * local maxima
     * plateaus
     * ridges
   * not complete
   * not optimal
   * memory efficient

---

5. Variants of hill climbing:

   * stochastic hill climbing → choose random improving move
   * first-choice → first improving move rather than best
   * random-restart hill climbing → restart when stuck

---

6. Simulated annealing (SA):

   * sometimes accepts worse moves to escape local maxima
   * acceptance probability:
     $$P = e^{-\Delta E / T}$$
   * (T) (temperature) decreases over time (cooling schedule)
   * better at escaping local optima than hill climbing
   * not complete, not optimal, but very effective in practice

---

7. Beam search:

   * keep top (k) best states at each level
   * expand all children → keep best (k)
   * (k =) beam width
   * faster and uses less memory, but **not complete**, **not optimal**

---

8. Local search characteristics:

   * no backtracking
   * no frontier
   * only current state + evaluation
   * used when path doesn’t matter, only solution quality matters

---

9. Fitness function:

   * evaluates how good a state is
   * search tries to maximize or minimize it

---

10. Genetic Algorithms (GA):

    * population-based search
    * inspired by natural selection
    * each state = chromosome
    * fitness determines survival

---

11. GA process:

    1. initialize population
    2. evaluate fitness
    3. select parents
    4. crossover (recombine chromosomes)
    5. mutation (small random change)
    6. produce next generation

---

12. Selection strategies:

    * fitness proportional (roulette-wheel)
    * tournament selection
    * rank selection (used for stability)

---

13. Ranking trick (MIT):

    * instead of raw scores, rank individuals
    * compute probability based on rank
    * prevents one high-score individual from dominating selection
    * improves genetic diversity

---

14. Mutation:

    * prevents premature convergence
    * ensures exploration
    * usually applied with low probability

---

15. Crossover:

    * main source of generating new structures
    * mixes parts of parent chromosomes
    * types: single-point, two-point, uniform

---

16. When to use GA:

    * large search spaces
    * noisy evaluation functions
    * hard combinatorial problems
    * when local search gets stuck easily
    * when heuristic structure is weak or unknown

---

17. Min-conflicts (for CSP local search):

    * choose a conflicted variable
    * choose value minimizing conflicts
    * extremely effective for N-Queens
    * often solves large CSPs quickly

---

18. Completeness summary:

    * hill climbing: ✘
    * SA: ✘
    * beam search: ✘
    * GA: ✘
    * min-conflicts: ✘
      (Local search is almost never complete)

---

19. Memory usage summary:

    * hill climbing: (O(1))
    * SA: (O(1))
    * beam search: (O(k))
    * GA: (O(\text{population size}))

---

20. Local search is ideal when:

    * state space is huge
    * path to solution is irrelevant
    * approximate or “good enough” solutions are acceptable
    * randomization helps escape local traps
