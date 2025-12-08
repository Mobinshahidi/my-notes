---
title: states cheatsheet
description: cheatsheet
---

1. Reaching goal detect by goal test  -> goal test is a function that check if we are get to our goal or not
2. Most smallest valid state for pacman is {x,y} (pacman location it self)
3. Initial state in search => starting point
4. Successor states -> every possible move for our current state like `(x+1, y) (x-1, y) (x, y+1) (x, y-1)` -> The successor function returns **all the next possible states** from the current state.
5. Branching factor -> the **maximum number of successors** any state can have.
	   - Successor states = actual children for _this_ state
	   - Branching factor = maximum number of children ANY state can have
6. Markov property -> future depends only on current state, not on history -> state must contain all info necessary to determine future actions
7. Add extra var to a state just makes search slower and its not minimal anymore
8. Dfs on a binary tree has branching factor of 3
9. A state is valid only if it contains _all information needed to make decisions_.
10. Smallest valid state(must include only information that affects future decision) depends on the problem’s goal
    - If Pacman must eat all food, smallest valid state is:
    - `(x, y, food_status)`
    - If Pacman must reach a location, smallest valid is:  
    - `(x, y)` 
11. Successor function must update ALL parts of the state  -> If state = `(x, y, has_key)`, then successor must update **has_key** when needed.
12. Goal test only depends on state, not path and check -> (position,food eaten, progress boolean, but never check history of actions)
13. You must include Boolean “progress” variables for multi-stage goals
    - Catch ghost twice → `caught_once`
    - Pick up key → `has_key`
    - Visit all corners → `visited_TL, visited_TR, visited_BL, visited_BR`
14. State must not include -> search algo info, path history, whole map
15. 