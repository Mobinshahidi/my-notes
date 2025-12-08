---
title: LP cheatsheet
description: cheatsheet
---

1. LP has linear objective,linear constraints, continuous var
2. General form:
   objective: $\min\ or\ max⁡\ c_1x_1+⋯+c_nx_n$
   constraints: $a_1​x_1​+⋯+a_n​x_n​ (≤,≥,=) b$
   non-negativity: $x_i​≥0$
3. Recognizing LP :
	   - objective is linear
	   - constraints are linear
	   - no powers: (✘ x^2)
	   - no products: (✘ xy)
	   - no abs: (✘ ∣x∣)
	   - no max/min inside constraints
	   - no logical conditions
4. Converting to standard form
	   - convert <= to >= : multiply constraint by -1
	   - equality becomes two inequalities
	   - ensure variables >= 0
5. Feasible region
	   - intersection of linear half spaces
	   - always convex
	   - LP optimum (if exists) occurs at a corner point
6. Corner point method (graphical LP)
	   - (used only when two variables)
	   - steps:
	   1. Turn constraints into lines
	   2. Shade feasible region
	   3. Compute all intersections
	   4. Keep only feasible corners
	   5. Evaluate objective at each corner
	   6. Pick best value	   
7. Types of LP outcomes
	   - bounded optimum: feasible region limited -> unique best corner
	   - unbounded: objective can improve infinitely. Minimize x with x >= 0 -> unbounded below
	   - infeasible: constraints contradict -> x>=5,x<=2
	   - infinite optimal solutions: objective parallel to a boundary -> x+y=10 and minimize x+y
8. How to write an LP
	   1. Define var(always first)
	   2. Objective: min/max (linear)
	   3. Constraints(linear only)
	   4. non-negativity
9. Typical LP patterns
	   - production scheduling
	   - transportation/shipping
	   - diet/cost minimization
	   - resource allocation
	   - flow/assignment relaxation
10. LP must know facts
	  - lp solutions always at corners
	  - feasible region convex
	  - lp cannot express:
		  - integer requirements
		  - or/and logic
		  - quadratic costs
		  - nonlinear constraints