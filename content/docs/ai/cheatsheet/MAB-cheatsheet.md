---
title: MAB cheatsheet
description: cheatsheet
---
1. MAB setting: k arms, each arm has unknown reward mean $( \mu_i )$; goal: maximize cumulative reward (minimize regret).
2. Reward estimate (sample mean):
   $\hat{\mu}-i = \frac{1}{n_i} \sum-{t=1}^{n_i} r_{i,t}$
   incremental update:
   $\hat{\mu} \leftarrow \hat{\mu} + \frac{1}{n}(r - \hat{\mu})$
3. Regret:
   $R_T = T\mu^- - \sum_{t=1}^T r_t$
   or
   $R_T = \sum_{t=1}^T (\mu^- - \mu_{a_t})$
4. Ε-greedy:
	   - with prob $( \epsilon )$: random arm
	   - with prob $( 1-\epsilon )$: arm with highest $( \hat{\mu}_i )$
	   - simple, constant exploration even late
5. Adaptive ε-greedy:
	   - ( $\epsilon_t = \frac{1}{t}$ )
	   - high exploration early, low exploration later
	   - lower regret than constant ε
6. Optimistic initial values (OIV):
	   - initialize $( \hat{\mu}_i(0) = Q_0 ) (large)$
	   - forces exploration (all arms look good at start)
	   - no random exploration needed
7. UCB (Upper Confidence Bound):
   $( \text{UCB}_i = \hat{\mu}_i + \sqrt{\frac{2 \ln t}{n_i}} )$
   choose arm: $( a_t = \arg\max_i \text{UCB}_i )$
	   - first term: exploitation
	   - second term: exploration bonus
	   - exploration decreases as $( n_i )$ increases
8. Algorithm comparison:
	   - ε-greedy: simple, random exploration
	   - adaptive ε: improves regret
	   - OIV: forced exploration via optimistic values
	   - UCB: principled exploration, near-optimal regret
9. What MAB algorithms require tracking:
	   - $( n_i ):$ how many times each arm chosen
	   - $( \hat{\mu}_i ):$ estimated mean reward
	   - t: round number
	   - regret or cumulative reward if asked
10. Typical exam tasks:
	    - compute sample mean after each pull
	    - simulate ε-greedy decisions
	    - simulate UCB values and pick arm
	    - compute regret for a sequence
	    - identify exploration vs exploitation behavior
11. When to use each:
	    - ε-greedy: simple tasks
	    - adaptive ε: improving over time
	    - OIV: structured exploration
	    - UCB: best theoretical performance
12. Key ideas:
	    - exploration prevents premature commitment
	    - exploitation uses learned estimates
	    - regret measures cost of not knowing the best arm
