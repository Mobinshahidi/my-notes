---
title: search & local search cheatsheet
description: cheatsheet
---


1. Search problem defines by:
	   - state  -> config of agent
	   - initial state
	   - goal test
	   - successor func
	   - path cost g(n)
2. Bfs ->
	   - fifo (first in first out)
	   - expands nodes in order of increasing depth
	   - complete if branching finite
	   - optimal if all step costs 1
	   - Time & space:O(b^d)
	   - good for -> 
		   - uniform cost actions
		   - finding shortest path in terms of number of steps
		- **Completeness ≠ optimality**
		- BFS is **only optimal when all step costs are equal**.
3. Dfs -> 
	   - lifo(last in first out)(stack) or recursion (that use call stack)
	   - expands deepest node first
	   - not complete
	   - not optimal
	   - time: `O(b^m)` (m=max depth)
	   - space: `O(b*m)` (very memory efficient)
	   - good for
		   - low memory 
		   - deep solutions
		   - when completeness doesn't matter
4. Ucs -> 
	   - priority queue ordered by g(n)
	   - expands node with lowest path cost so far
	   - its complete
	   - its optimal
	   - time: worst among uninformed
	   - space: huge(keeps many frontier nodes)
	   - good for
		   - non uniform costs
		   - finding cheapest path
		- bfs = ucs, when all costs = 1
5. Iddfs -> 
	   - hybrid -> bfs completeness & dfs memory efficiency
	   - process -> run dfs with increasing depth limits: 0 → 1 → 2 → … → d
	   - its complete
	   - its optimal
	   - time: `O(b^d)`
	   - space: `O(b*d)` 
	   - good for 
		   - low memory 
		   - large search space
6. A* -> 
	   - priority queue ordered by: f(n)=g(n)+h(n)
		   - g(n): costs so far
		   - h(n): heuristic estimate to goal
	   - A* expands lowest f-value
	   - heuristic is and estimate of remaining cost and used to guide search
	   - admissible heuristic: h(n)<=h*(n) -> never overestimate & guarantees A* ***is optimal***
	   - consistent heuristic: h(n)<=c(n,n')+h(n'): triangle inequality & guarantees:
		   - A* never reopens nodes
		   - frontier values never decrease
		   - search is efficient
		- consistency => admissibility (but not opposite)
		- if `h1` and `h2` are admissible: `h(n)=max(h1,(n),h2(n))` -> is admissible and more informed and if `h1` and `h2` are consistent, h(n) is also consistent
		- consistent heuristic; estimated cost from n is never more than going through n' -> makes A* efficient
		- max of consistent heuristics → consistent
		- sum of admissible heuristics → may be inconsistent
7. Local search algo does not store full paths, only current state
8. Hill climbing
	   - start at current state -> move to best neighbor -> repeat
	   - problems: gets stuck in local maxima, plateaus, ridges
	   - not complete
	   - not optimal
	   - o(1) memory
9. SA (simulated annealing)
	   - it sometimes allow bad moves to escape local maxima
	   - probability of accepting a worse state: $P=e^{−ΔE/T}$  -> t decreases over time ("cooling")
	   - pros:can escape local optima, better than hill climbing
	   - cons: requires tuning cooling schedule (temperature)
10. Beam search
	    - keep k best states at each layer, expand all children and keep best k
	    - k = beam width
	    - pros: faster than bfs, uses less memory
	    - cons: not complete, not optimal, can lose good branches early
11. GA(genetic algo)
	    - state=chromosome
	    - process: 
	      1. Start with population
	      2. Evaluate fitness
	      3. Select parents
	      4. Apply crossover and mutation
	      5. Produce next generation
	    - ranking trick -> instead of raw scores, rank individuals and computer probability based on rank -> avoid domination
12. In bfs all step costs must be equal(unit cost) to that bfs be optimal (because it expands by number of steps, not by path cost)
13. Dfs is complete if (state space is infinite, there are cycle, deep path leads nowhere)
14. Ucs is complete if all step costs are positive
15. In A*, heuristic overestimates, its not admissible because it should be <=of our value not overestimate
16. Ucs prioritize the node with smallest path cost g(n) (because it always choose cheapest path so far)
17. Manhattan distance ->  for grid world: $h(n)=∣x−x_g​∣+∣y−y_g​∣$  -> 
    - number of horizontal steps
    - plus number of vertical step
    - required to reach goal (no diagonals allowed)
18. Manhattan distance is the shortest possible path cost when moves cost 1.
19. Search tree vs graph? Tree = paths explored; graph = real states
20. Why visited? Prevent cycles & repeated states

| Situation                          | Best Algorithm      |
| ---------------------------------- | ------------------- |
| Uniform cost, small depth          | BFS                 |
| Deep tree, little memory           | DFS                 |
| Variable costs                     | UCS                 |
| Need optimal & heuristic           | A*                  |
| Huge depth but low memory          | IDDFS               |
| Only care about improving state    | Hill Climbing       |
| Need exploration past local maxima | Simulated Annealing |
| Large, noisy search                | Genetic Algorithm   |

|Algorithm|Node order|Frontier type|
|---|---|---|
|**DFS**|deepest first|stack|
|**BFS**|shallowest first|queue|
|**UCS**|least g(n)|priority queue|
|**A***|least g(n)+h(n)|priority queue|
|**Greedy Best First**|least h(n)|priority queue|

| Algorithm | Complete? | Optimal?            | Time       | Space      | Notes                          |
| --------- | --------- | ------------------- | ---------- | ---------- | ------------------------------ |
| **BFS**   | ✔         | ✔ (unit cost)       | (O(b^d))   | (O(b^d))   | Expands by depth               |
| **DFS**   | ❌         | ❌                   | (O(b^m))   | (O(bm))    | Memory cheap, bad completeness |
| **UCS**   | ✔         | ✔                   | VERY large | VERY large | Expands cheapest (g(n))        |
| **IDDFS** | ✔         | ✔ (unit cost)       | (O(b^d))   | (O(bd))    | BFS+DFS hybrid                 |
| **A***    | ✔         | ✔ (if h admissible) | Depends    | Depends    | Expands lowest (f=g+h)         |
