---
title: minimax cheatsheet
description: cheatsheet
---
1. Adversarial search is used when multiple agents act with **conflicting goals** (e.g., player vs opponent).
2. Game states alternate between **MAX** (your turn) and **MIN** (opponent’s turn).
3. Terminal states have **utility values** (payoff to MAX).
   Example: win = 1, lose = −1, draw = 0.

---

4. Minimax value of a state:
   $$\text{Minimax}(s) =
   \begin{cases}
   \text{Utility}(s), & s \text{ is terminal} \
   \max_{a \in A(s)} \text{Minimax}(\text{Succ}(s,a)), & s \text{ is MAX} \
   \min_{a \in A(s)} \text{Minimax}(\text{Succ}(s,a)), & s \text{ is MIN}
   \end{cases}
   $$

---

5. MAX chooses action with **highest** minimax value.
6. MIN chooses action with **lowest** minimax value (perfect opponent).
7. Minimax assumes opponent behaves **optimally** to minimize your utility.

---

8. Expectimax value (for stochastic/opponent is random):
   $$\text{Expectimax}(s) =
   \begin{cases}
   \text{Utility}(s), & s \text{ is terminal} \
   \max_{a \in A(s)} \text{Expectimax}(\text{Succ}(s,a)), & s \text{ is MAX} \
   \sum_{a \in A(s)} P(a),\text{Expectimax}(\text{Succ}(s,a)), & s \text{ is chance node}
   \end{cases}
   $$

---

9. Expectimax uses **expected value**, not min.
10. Minimax = opponent is **adversarial**; Expectimax = opponent is **random**.

---

11. Game tree nodes:

    * MAX node: choose largest child
    * MIN node: choose smallest child
    * Chance node: weighted average of children

---

12. Alpha-beta pruning reduces nodes explored without changing answer.
13. Alpha (α): best value MAX can guarantee so far (lower bound).
14. Beta (β): best value MIN can guarantee so far (upper bound).

---

15. Pruning occurs when:

    * For MAX node:
      if current value ≥ β → prune remaining children
    * For MIN node:
      if current value ≤ α → prune remaining children

---

16. Alpha-beta correctness:

    * never removes branches that could affect final decision
    * only removes *provably irrelevant* branches
    * does **not** change minimax result

---

17. Alpha-beta best-case performance (perfect ordering):
    $$O(b^{d/2})$$
    (square root of original tree size)

18. Minimax tree complexity (no pruning):

    * Time: $$O(b^d)$$
    * Space: $$O(bd)$$ (depth-first)

---

19. Evaluation function (for non-terminal states):

    * approximates utility when searching to limited depth
    * often weighted sum of features
    * must correlate with true winning chances

---

20. Differences summary:

    * Minimax: worst-case optimal, opponent minimizes your score
    * Expectimax: average-case optimal, opponent/randomness modeled probabilistically
    * Alpha-beta: optimizes minimax, same answer faster
    * Evaluation: needed for limited-depth search (practical play)
