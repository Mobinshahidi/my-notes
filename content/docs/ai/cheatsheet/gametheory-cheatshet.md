---
title: gametheory cheatsheet
description: cheatsheet
---
1. Game theory studies strategic interactions where players choose actions to maximize their own utility.

2. Normal-form game defined by:

   * set of players
   * action set for each player
   * payoff matrix (utilities for each action profile)

3. Strictly dominated strategy:

   * strategy ( s_i ) is strictly dominated by ( s_i' ) if:
     $$u_i(s_i', s_{-i}) > u_i(s_i, s_{-i}) \quad \text{for all } s_{-i}$$
   * meaning: **always worse**, never optimal.

4. Strict domination elimination:

   * remove any strictly dominated strategy
   * repeat until no more eliminations
   * order does **not** matter for strict domination.

5. Weakly dominated strategy:

   * dominated in all cases, strictly better in at least one case
   * elimination order **can** change result (not always safe).

6. Iterated elimination of strictly dominated strategies (IESDS):

   * repeatedly remove strictly dominated strategies
   * reduces game to a smaller, simpler matrix
   * remaining strategies are “rationally survivable”

7. Best response:

   * a strategy that maximizes a player’s utility given others’ actions
     $$BR_i(s_{-i}) = \arg\max_{s_i} u_i(s_i, s_{-i})$$

8. Nash equilibrium (NE):

   * no player can improve by deviating alone
     $$u_i(s_i^*, s_{-i}^*) \ge u_i(s_i, s_{-i}^*) \quad \forall s_i$$
   * each player is playing a **best response** to the others
   * mutual consistency of expectations

9. Pure strategy NE:

   * NE where each player chooses a single deterministic action
   * found by identifying cells where both players’ actions are best responses.

10. Mixed strategy NE:

    * players randomize between actions with certain probabilities
    * used when no pure NE exists
    * makes opponent indifferent between their own actions

11. 2×2 mixed NE computation:

    * Let Player 1 randomize: P(A) = p, P(B) = 1−p
    * Player 2 is indifferent when:
      $$\text{Payoff of action X} = \text{Payoff of action Y}$$
    * Solve linear equations for p and q.

12. Indifference principle:

    * In equilibrium, a player must be indifferent among all actions they randomize over
    * because if one action were strictly better, they would not mix.

13. Support of a mixed strategy:

    * set of actions assigned **positive probability**

14. Zero-sum games:

    * one player’s gain = other’s loss
    * utilities sum to zero
    * minimax theorem applies:
      $$\max \min u = \min \max u$$

15. Dominant strategy equilibrium:

    * strategy is dominant if it is best regardless of opponents
    * when all players have dominant strategies → simple, unique outcome

16. Relation to Minimax:

    * Minimax solves optimal play for zero-sum games
    * Game theory NE applies to **general** strategic games, not necessarily zero-sum.

17. Payoff matrix reading:

    * Rows: Player 1 actions
    * Columns: Player 2 actions
    * Cells: ((u_1, u_2))

18. How to find pure NE in a matrix:

    * Circle best responses for Player 1 in each column
    * Circle best responses for Player 2 in each row
    * A cell that has **both circles** is a Nash equilibrium.

19. Prisoner’s Dilemma (standard example):

    * mutual cooperation is better
    * but both defect due to dominant strategies
    * (D,D) is the unique NE

20. Matching pennies:

    * no pure NE
    * unique mixed NE
    * each player mixes 50/50
    * textbook case of opponent unpredictability

