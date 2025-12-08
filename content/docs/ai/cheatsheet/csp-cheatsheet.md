---
title: csp cheatsheet
description: cheatsheet
---
1. CSP defined by:
	   - variables → $( X_1, X_2, \dots, X_n )$
	   - domains → possible values for each variable
	   - constraints → rules limiting value combinations
	   - goal: assign values to all variables satisfying all constraints
2. Types of constraints:
	   - unary → constraint on 1 variable
	   - binary → constraint on pairs of variables
	   - higher-order → constraint on 3+ variables
	   - global constraints → general structured constraints (e.g., all-different)
3. Constraint graph:
	   - nodes = variables
	   - edges = binary constraints
	   - structure often determines difficulty of CSP
4. Backtracking search
	   - depth-first search over assignments
	   - assign variable → check constraints → continue
	   - fails early when inconsistency detected
5. Minimum Remaining Values (MRV):
	   - choose variable with fewest legal values left
	   - helps reduce branching factor
6. Degree heuristic:
	   - choose variable involved in most constraints
	   - breaks ties in MRV
7. Least Constraining Value (LCV):
	   - choose value that rules out fewest values for neighbors
	   - improves chance of success
8. Forward checking:
	   - when assigning variable (X), eliminate inconsistent values from neighbors
	   - detects failure early
9. Arc consistency (AC-3):
	   - revise constraints to ensure:$$\text{for every value of } X,\ \exists\ \text{compatible value of } Y$$
	   - removes impossible values before search
10. Arc consistency behavior:
	    - AC-3 repeatedly enforces binary arc consistency
	    - reduces domains
	    - may detect inconsistency (empty domain → no solution)
11. Backtracking + inference:
	    - combine: MRV + LCV + forward checking + AC-3
	    - dramatically reduces search time
12. Local search for CSPs (e.g., min-conflicts):
	    - start with full assignment
	    - repeatedly repair constraint violations
13. Min-Conflicts heuristic:
	    - select conflicted variable
	    - assign value minimizing number of violated constraints
	    - extremely effective for large problems (e.g., ( n)-Queens)
14. Completeness & optimality:
	    - backtracking search: complete (will find solution or prove none)
	    - min-conflicts local search: not complete, not optimal, but works well for large CSPs
15. Domain pruning:
	    - if domain becomes empty → failure
	    - smaller domains → easier search
16. CSP examples:
	    - map coloring
	    - N-queens
	    - Sudoku
	    - scheduling
17. Why CSP is different from standard search:
	    - no path cost (g(n))
	    - no A- / BFS / UCS
	    - states defined by partial assignments
18. Backtracking ordering summary:
	    - MRV → choose variable
	    - Degree heuristic → tie-break
	    - LCV → choose value
	    - Forward checking / AC-3 → inference
19. Constraint propagation:
	    - inference techniques that reduce domains before search
	    - AC-3 is the most common
20. When AC-3 is useful:
	    - before search: reduce domains
	    - during search: maintain consistency
	    - avoids exploring impossible assignments
