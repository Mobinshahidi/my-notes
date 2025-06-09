---
title: theory of language and machine notes
description: theory of language and machine notes
---

# 0.1
## automata, computability and complexity
### 3 core idea
### 1. Automata theory (finite models of computation)
- Auatomata are abstract machines that read strings and decide yes/no(accept/reject)
- Ex: a simple machine that checks if a string ends in '01'
- **Goal: understand which languages (sets of strings) can be accepted by simple machines.**
Think of its like: 
> you give an input -> machine reads it -> machine decides if its 'valid' or not.

Types of machines:
- Finite automata (fa): memoryless machines, good for simple patterns.
- Pushdown automata (pda): like fa + a memory stack, used for languages with nesting (like parentheses).
- Turin machines (tm): full power of real computers
### 2. Computability (what is computable?)
- Not every problem can be solved by and algorithm.
- Some problems are undecidable: no computer or algorithm can ever solve them for all inputs
- Ex: can we write a program that detects whether any other program halts or loops forever? -> no. This is the halting problem
- **goal:**
	- **define the limits of what problems are solvable**
	- **prove some problems are unsolvable even in theory**
### 3. Complexity theory (how hard is a problem?)
- Some problems are solvable but not efficiently
- We classify problems based on how much time or memory they need
Key concept:
- P: problems solvable quickly (polynomial time)
- Np: problems whose solutions can be verified quickly, but not necessarily found quickly
- Np-complete: the hardest problem in np.
- **Goal : to understand the resources required for solving problems and distinguish between easy vs hard problems** 
## **Big Picture**

| Topic         | Question it answers                          | Example                                     |
| ------------- | -------------------------------------------- | ------------------------------------------- |
| Automata      | What languages can simple machines accept?   | DFA accepting binary strings ending in "01" |
| Computability | What problems can be solved at all?          | Halting problem → not solvable              |
| Complexity    | How much effort does solving a problem need? | Sorting numbers → easy (P), Sudoku → NP     |


# 0.2
## mathematical notions and terminology
### key concepts
1. Sets
   a set is a collection of distinct elements
	   - {a,b,c} -> a set of symbols
	   - ∅ -> the empty set, has no elements
	   - {∅} -> a set with one element, and that element is the empty set!
2. Set notations
	   - `a ∈ A` → "a is an element of A"
	- `A ⊆ B` → "A is a subset of B" (all elements in A are also in B)
	- `A ∪ B` → union
	- `A ∩ B` → intersection
	- `A - B` → difference
	- `A′` → complement (everything not in A)
> 	**important**: sets are unordered and don't contain duplicates:
> 		- Sets **cannot have repeated elements**.
> 		  `{a, a, b}` is **equivalent to** `{a, b}`
> 		- The **order of elements doesn't matter**.
> 		  `{a, b, c}` is **the same** as `{b, a, c}` or `{c, b, a}`
3. Cartesian product(A x B)
   the set of ordered pairs:
   ```
   A = {1, 2}, B = {x, y}  
   A × B = {(1, x), (1, y), (2, x), (2, y)}
   ```
   used to define **relations** and **functions**
4. Functions 
   A **function** `f: A → B` assigns to each `a ∈ A` one and only one `b ∈ B`.
	- **One-to-one (injective):** Different `a` gives different `b`
	- **Onto (surjective):** Every `b ∈ B` is matched
	- **Bijective:** Both injective and surjective
	- **Inverse:** If `f(a) = b`, then `f⁻¹(b) = a`
5. Operations
	- **Unary operation:** takes one input (`¬p`)
	- **Binary operation:** takes two inputs (`p ∧ q`)
	- Examples: union, intersection, string concatenation
6. Languages
   A **language** is a set of strings over an alphabet.
	- Alphabet: finite set of symbols (`Σ = {0,1}`)
	- String: sequence of symbols (`0101`)
	- `Σ*`: all possible finite strings (including empty string `ε`)
	- Language `L ⊆ Σ*`: a subset of all strings over Σ
	Examples:
	- `L1 = {w | w has even number of 0s}`
	- `L2 = {ε, 1, 11, 111, ...}` → strings of only 1s
## Big Picture: Why this matters

|Concept|Use in Theory|
|---|---|
|Sets|Define languages, transitions, alphabets|
|Functions|Define automata behavior (δ function)|
|Operations|Language union, concatenation, closure|
|Cartesian|Used in defining states and transitions|
|Languages|Main object we study & manipulate|

# 0.3
## definitions, theorems and proofs
### key concepts
1. Definition
	   - a definition introduces a new concept using existing ideas.
	   - it names something and describes what it is, precisely.
	   - ex: a palindrome is a string that reads the same forward and backward. Formally: a string `w ∈ Σ*` is a palindrome if `w = reverse(w)`.
	   - **important: definitions are not provable. They are accepted as the rules of the game.**
2. Theorem
	   - a theorem is a mathematical truth that must be proven using logic
	   - once proven, it becomes a reliable tool
	   - ex: every dfa can be converted to an equivalent nfa.
3. Lemma (لم)
	   - a lemma is a helpful mini theorem, usually used to prove a bigger theorem
	   - its like a stepping stone
	   - **think: first prove lemma A -> then use it to prove theorem B**
4. Corollary (نتیجه یا استنتاج)
	   - a corollary is something that follows directly from a theorem.
	   - its often obvious once the theorem is proved.
	   - ex: if we prove that regular languages are closed under union -> a corollary might be : they are also closed under intersection (using DeMorgan's laws) 
5. Propositions and claims
	   - proposition: a minor theorem, usually easy to prove
	   - claim: a statement made within a proof , to help break the logic into steps
6. Proof
	   - a proof is a logical argument that shows why a theorem is true
	   - its built sing:
		   - definitions
		   - lemmas
		   - logic
		   - previously proven theorems
	   - its like a chain: `True facts → connected logically → to reach the statement` 
#### notes
تعریف = چیز جدید را _معرفی می‌کند_  
قضیه = چیز واقعی را _ثابت می‌کند_  
لم = ابزار اثبات قضیه  
نتیجه = خروجی سریع از قضیه  
اثبات = زنجیره‌ی منطقی
## Summary Table

|Concept|Description|Example|
|---|---|---|
|Definition|Precise naming of a concept|Palindrome = reverse(w) = w|
|Theorem|Major truth, must be proven|DFA ⊆ NFA|
|Lemma|Smaller theorem used in proofs|Pumping Lemma|
|Corollary|Immediate result from a theorem|If A ∪ B is regular, so is A*|
|Proposition|Small/easy theorem|All finite languages are regular|
|Claim|Temporary step in a proof|

# 0.4
## types of proof
### main types of proofs
1. Proof by exhaustion(enumeration/case analysis) (اثبات با بررسی تمام حالات)
	   - try all possible cases and show each one works
	   - good when the number of cases is finite and small
	   - ex: prove a number `n ∈ {1, 2, 3, 4}` is even → check all 4 values manually.
	> tip: very basic method. Easy but doesn't scale well
2. Direct proof (اثبات مستقیم)
	   - start with the assumption (if part) and logically deduce(استنباط کردن) the conclusion (then part)
	   - ex: If `n` is even, then `n²` is even:  
		`n = 2k ⇒ n² = 4k² = 2(2k²)` ⇒ even.
3. Proof by contrapositive (اثبات متقابل)
	   - instead of proving: if p then q, you prove: if not q, then not p.
	   - why? Sometime proving the contrapositive is easier.
	   - key logic: `P → Q` is logically **equivalent** to `¬Q → ¬P`.
	   - ex: If `n²` is odd, then `n` is odd. → Contrapositive: If `n` is even, then `n²` is even.
4. Proof by conditions (اثبات به تناقض)
	   - assume the statement is false and show this leads to a logical contradiction
	   - ex: To prove √2 is irrational:  Assume √2 **is rational**, say = a/b → Leads to contradiction.
5. Proof by induction (اثبات به روش استقرا)
	   - used for statements about natural numbers or recursive structures
		   - two steps:
		     1. Base case: prove for the starting value (e.g, n = 0)
		     2. Inductive step: assume true for n, then prove for n+1.
		- analogy: like dominoes -> if one falls and each pushes the next, they all fall.
## Summary Table

|Type|Description|When to Use|
|---|---|---|
|Exhaustion|Try all cases|Small, finite sets|
|Direct Proof|From assumptions to result|When logic flows directly|
|Contrapositive|Prove opposite statement|If direct proof is hard|
|Contradiction|Assume false, show contradiction|When proving false is easier|
|Induction|Use base case + inductive step|For sequences, recursion, etc.|
# 1.1
## finite automata
### key concepts
1. What is a finite automaton?
   a finite automaton (fa) is an abstract mach that:
	   - reads and input string symbol by symbol
	   - changes its state based on the input
	   - decides whether the string is accepted or rejected.
	   - used to model things like pattern checking and lexical analysis
2. Components of a finite automaton
   a fa is formally a 5-tuple: 
   `M = (Q, Σ, δ, q₀, F)`

|Symbol|Meaning|
|---|---|
| `Q` | Finite set of **states** |
|`Σ`|Finite **input alphabet**|
|`δ`|**Transition function**|
|`q₀`|**Start state** (initial state)|
| `F` | Set of **accepting (final)** states |
3. How it works
	   1. The machine starts at `q₀`.
	   2. It reads each symbol of the input string.
	   3. Uses the transition function `δ` to determine the next state.
	   4. After reading the entire string:
		- If it ends in a state in `F` → **Accept**
		- Otherwise → **Reject**
4. DFA (deterministic finite automaton)
   a dfa is a special kind of fa where:
	   - every state and input symbol has exactly one transition
	   - no ambiguity or guessing is allowed
	   - mathematically : `δ: Q × Σ → Q`
5. Language of a dfa
   let `M` be a dfa. The language of M is the set of all strings `W` such that `M` accepts `W` :
   `L(M) = { w ∈ Σ* | M accepts w }`
6. Example dfa - ends with '01'
	   - states : `Q = {q0, q1, q2}`
	   - Alphabet: `Σ = {0,1}`
	   - Start state: `q0`
	   - Final state: `F = {q2}`
	 transition: 
 ```
	 δ(q0, 0) = q1
	 δ(q1, 1) = q2 (other inputs loop or go to q0)
```

## Why Minimize a DFA?
- To reduce **complexity** and **memory usage**.
- Simplify design and implementation in compilers or software.
- It's useful when converting NFA → DFA (since that can create many states).
## Steps of DFA Minimization

### Step 1: **Remove Unreachable States**
- Start from the start state.
- Use BFS/DFS to mark all reachable states.
- Remove any state that is **not reachable**.
### Step 2: **Partition the States**
Use the **Myhill-Nerode equivalence method** (also called **partition refinement**):
#### Initial Partition:
Split states into two groups:
- Accepting states (F)
- Non-accepting states (Q - F)
#### Step-by-Step Refinement:
- Compare states based on transitions.
- If two states behave **differently** for some input (go to different groups), **split them into different groups**.
- Repeat until no more splits are needed.
### Step 3: **Build the New DFA**
- Each group of equivalent states becomes **one new state**.
- Create transitions between the new states based on the transitions in the original DFA.
### Final Result:
You get a **minimal DFA** — smallest number of states that still accepts the same language.
## Example:
Original DFA:

|State|0|1|Accepting?|
|---|---|---|---|
|A|B|C|❌|
|B|A|D|❌|
|C|E|F|✅|
|D|C|B|✅|
|E|E|F|✅|
|F|F|F|✅|
## Summary Table

|Term|Description|
|---|---|
|FA|Machine to recognize regular languages|
|Q|Set of states|
|Σ|Input alphabet|
|δ|Transition function|
|q₀|Initial state|
|F|Set of final states|
|DFA|FA with unique transition for each input|
|L(M)|Language accepted by machine `M`|
# 1.2
## nondeterminism
### key concepts
1. what is an nfa?
   an nfa is similar to a dfa but allows:
	   - multiple transitions for the same input
	   - no transition for some inputs
	   - ε transitions: moves without reading any symbol
	 **this means the machine can be in multiple states at once or choose between paths.**
2. nfa formal definition
	   - an nfa is a 5-tuple: `N = (Q, Σ, δ, q₀, F)`
	   - same structure as dfa, but transition function `δ` is different: `δ: Q × Σε → 𝒫(Q)` where :
		   - `Σε = Σ ∪ {ε}` (includes ε-transitions)
		   - `𝒫(Q)` means “set of subsets of Q” (can return multiple states) (2^Q)
3. how nfa works
   for a given input string:
	   - the machine may follow many paths at once.
	   - if at least one path leads to an accepting state, the string is accepted.
	 **so nfa accepts a string if it can reach an accepting state, not necessarily must.**
4. ε-Transitions
	   - allow the machine to move to another state without consuming any input
	   - useful in simplifying automata or combining machines.
	 **dfa does not allow ε-transitions -> only nfa can**
5. dfa vs nfa

|Feature|DFA|NFA|
|----|-----|----|
|Transitions|One per symbol per state|Multiple possible transitions|
|ε-Transitions|❌ Not allowed|✅ Allowed|
|Current State|One state at a time|Can be in multiple states|
|Determinism|Fully determined|May "guess" the right path|
|Power|Equal (both accept regular languages)|
**bot accept exactly the same languages (regular languages)**
6. converting nfa to dfa
	   - for every nfa, there exists a dfa that accepts the same languages
	   - this process is called subset construction or powerset construction
	   - idea: **simulate all possible nfa states as one dfa state**
7. why use nfas?
	   - easier to design and combine than dfas
	   - often lead to simpler solutions for complex patterns
	   - but ultimately, any nfa can be replaced by a dfa
## Summary Table

|Term|Description|
|---|---|
|NFA|Non-deterministic finite automaton|
|ε-transition|Transition without reading input|
|δ Function|Returns a set of possible next states|
|Acceptance|Accept if **any path** leads to final state|
|DFA vs NFA|Equivalent power, NFA is more flexible|
|Conversion|Every NFA can be converted to an equivalent DFA|
# 1.3
## regular expressions
### key concepts
1. what is a regular expression?
   a regular expressions is a symbolic way to describe a regular language.
   it builds pattern using characters and special operators
   example:
   ```
    (0 + 1)* → all binary strings  
	01 → only one string: "01"  
	1*0 → all strings ending with one 0 after 1
	```
2. alphabet and base cases
   regular expressions are built over an alphabet **Σ**, like `{0,1}`.
   these are the base expressions:

|Expression|Language it describes|
|---|----|
|`∅`|The empty language (accepts nothing)|
|`ε`|Accepts only the empty string|
|`a`|Accepts only the string `"a"`|

3. operators in regular expressions

|Operator|Meaning|Example|
|---|---|---|
|`+`|Union (`L1 ∪ L2`)|`0 + 1` = either 0 or 1|
|`.`|Concatenation (`L1 L2`)|`01` = string "01"|
|`*`|Kleene star (zero or more repetitions)|`0*` = "", "0", "00",...|
|`()`|Grouping (like math parentheses)|`(01 + 10)`|
4. example regular expressions and their languages

|Expression|Language|
|---|---|
|`0*1`|Any number of 0s followed by a single 1|
|`(0 + 1)*`|All binary strings (including ε)|
|`1(0 + 1)*`|Strings that start with 1|
|`1*0*`|Any number of 1s followed by any number of 0s|
|`1*01*`|Strings with exactly one 0 somewhere|
5. regular expressions vs automata
	   - every re can be converted into an nfa
	   - every dfa/nfa can be converted into an re 
	   - re <-> nfas <-> dfas
6. **operator precedence** (order)

|Priority|Operator|Description|
|---|---|---|
|Highest|`*`|Kleene star|
|Medium|`.` Concatenation|Combine strings|
|Lowest|`+`|Union|
	**always use `()` when needed**

## Summary Table

|Concept|Description|
|---|---|
|Regular Expression|A way to describe regular languages|
|Base cases|`∅`, `ε`, and characters from alphabet|
|Operators|`+`, `.`, `*`, `()`|
|Equivalence|RE = NFA = DFA|
|Precedence|`*` > Concatenation > `+`|

# 1.4
## nonregular languages
### key concepts
1. what is a nonregular language?
	   - a nonregular language is a language that cannot be accepted by any dfa or nfa.
	   - example : `L = { aⁿbⁿ | n ≥ 0 } → strings with equal number of a’s followed by equal number of b’s`
	   - or palindrome languages
	   - you can't make dfa for this because dfa has no memory to count n.
2. how to prove a language is not regular
	   - to prove a language is not regular we use:
	   - **pumping** **lemma** for regular languages 
	   - its a proof tool that :
		  - **if a language is regular, then all long strings in it must behave in a certain way.**
3. statement of the pumping lemma
	   - let `L` be a regular language
	   - then there exist a constant `p` (called the pumping length) such that :
	   - For **any string** `s ∈ L` with `|s| ≥ p`,  
	   - there exists a way to split `s` into **3 parts**: `s = xyz`
	   - with the following conditions:
		   1. `|y| > 0`
		   2. `|xy| ≤ p`
		   3. For **all i ≥ 0**, the string `xyⁱz ∈ L`
	>this means : **we can pump (repeat) the middle part `y` any number of times, and still stay in the language**
4. how to use it (proof strategy)
	   - to prove a language `L` is not regular:
		1. assume `L` is regular.
		2. let `p` be the pumping length.
		3. choose a specific string `s ∈ L` such that `|s| ≥ p`.
		4. show that for any possible way to split `s = xyz`,  **pumping** `y` breaks the condition `xyⁱz ∉ L` for some `i`.
	>	condition -> so `L` is not regular
5. example
   Prove `L = { aⁿbⁿ | n ≥ 0 }` is not regular.
	1. Assume `L` is regular → pumping lemma holds.
	2. Let `p` be the pumping length.
	3. Choose `s = aᵖbᵖ` → length ≥ p
	4. Any split `s = xyz`, where `|xy| ≤ p` ⇒ `y` contains only `a`s.
	5. Pump `y` twice → get more `a`s than `b`s → not in `L`
    Contradiction → `L` is **not regular**.

## Summary Table

|Term|Description|
|---|---|
|Nonregular|Languages **not** accepted by any DFA/NFA|
|Pumping Lemma|Tool to prove nonregularity|
|`s = xyz`|Decomposition of long strings in regular languages|
|Proof strategy|Assume regular → show contradiction when pumping|

# 2.1
## context free grammars
### key concepts
1. what is context free grammar (cfg)?
   a cfg is a 4-tuple `G = (V, Σ, R, S)`

|Symbol|Meaning|
|---|---|
|`V`|Finite set of **variables** (non-terminals)|
|`Σ`|Finite set of **terminals** (alphabet)|
|`R`|Set of **rules** or **productions**|
|`S`|**Start variable** (S ∈ V)|
2.  production rules
	   - each rule is written like: `A → α`
	   - where :
		   - `A` is a non-terminal (from `V`)
		   - `α` is a string of terminals and/or non-terminals (from `(V ∪ Σ)*`)
		 this means: we can replace `A` with `α`.
3. language of a cfg
	-  the generated by grammar `G` is:
	  `L(G) = { w ∈ Σ* | S ⇒* w }`
	- that means: all string w made by starting from `S` and applying rules to read terminal only strings.
4. example cfgs
	 Grammar for balanced parentheses:
	```
	S → SS  
	S → (S)  
	S → ε
	```
	 Grammar for strings of form `aⁿbⁿ`
	```
	S → aSb  
	S → ε
	```
	 Grammar for arithmetic expressions:
	```
	E → E + E  
	E → E * E  
	E → (E)  
	E → id
	```
5. derivations
	   - a derivation is a sequence of steps from `S` to a string of terminals
	   - example: `S ⇒ aSb ⇒ aaSbb ⇒ aabb`
	   - you apply rules step by step
6. leftmost and rightmost derivations
	   - leftmost derivation: always expand the leftmost non-terminal
	   - rightmost derivation: always expand the rightmost non-terminal
	  **this is useful when generating parse trees**
7. parse trees
	   - a parse tree is a tree representation of how a string is derived from `S`.
	   - leaves = terminal symbols.
	   - internal nodes = non-terminal.
	  parse trees help:
		   - visualize derivations
		   - detect ambiguity
8. ambiguity in cfgs
	   - a cfg is ambiguous if a string can have more than one parse tree
	   - example: 
		   - arithmetic grammar can have multiple interpretations:
		   - `E + E * E → could mean (E + E) * E or E + (E * E)`
		   - ambiguity can cause problems in compilers and parsers

## Summary Table

|Term|Description|
|---|---|
|CFG|Grammar with rules A → α|
|L(G)|Language generated by CFG|
|Derivation|Sequence of rule applications|
|Parse Tree|Tree form of derivation|
|Ambiguity|More than one parse tree for a string|
|Leftmost/Rightmost|Strategy for derivation order|

# 2.2
## pushdown automata
### key concepts
1. what is a pda?
	- a pushdown automaton is like a dfa plus a stack.
	- the stack provides unlimited memory (lifo)
	- it lets the machine match nested structures(e.g.,`aⁿbⁿ`, balanced parentheses)
	- pda accepts more languages than dfa
2. pda components
	- a pda is a 7-tuple `P = (Q, Σ, Γ, δ, q₀, Z₀, F)`

|Symbol|Meaning|
|---|---|
|`Q`|Finite set of states|
|`Σ`|Input alphabet|
|`Γ`|Stack alphabet (symbols pushed/popped)|
|`δ`|Transition function|
|`q₀`|Start state|
|`Z₀`|Initial stack symbol|
|`F`|Set of accepting states|

3. pda transition function
   `δ: Q × (Σ ∪ {ε}) × Γ → 𝒫(Q × Γ*)`
   it takes :
	   - current state
	   - current input symbol (or ε)
	   - top of the stack
   and returns:
	   - new state(s)
	   - what to push on the stack (or pop if ε)

4. how pda works
	- it reads an input symbol (or ε)
	- it checks the top of the stack
	- it changes state, and modifies the stack (push/pop)
	- if it reaches a final state **OR** empties the stack -> it accepts
5. pda example -> language ### `{ aⁿbⁿ | n ≥ 0 }`
	This language is **not regular**, but it is **context-free** and can be accepted by a PDA.
	**Idea:**
	- Push an `A` onto the stack for each `a`
	- Pop an `A` for each `b`
	- Accept if the stack ends empty (or enters accepting state)
6. acceptance modes
   two types of acceptance:
	   1. final state: pda reaches an accepting state after reading input
	   2. empty stack: pda empties its stack after reading input
	  **both methods define the same class of languages**

 7. PDA vs DFA

|Feature|DFA|PDA|
|---|---|---|
|Memory|None (finite states only)|Stack (LIFO memory)|
|Power|Regular languages only|Context-free languages|
|Uses|Simple patterns|Nested structure|
## Summary Table

|Term|Description|
|---|---|
|PDA|Machine with stack memory|
|Γ|Stack alphabet|
|δ|Transition using input + stack|
|Push/Pop|Modify the stack|
|Acceptance|By final state or empty stack|

# important notes
- for solving dfa that told us to not contain something, we can find the dfa for  contain, then flip it(final state became as non final state and non final state become final states)
- Regular language U Regular language = Regular language  
- Regular language CONCAT Regular language = Regular language  
- Regular language * = Regular language  
- not(Regular language) = Regular language  
- Context-free language ∩ Regular language = Context-free language  
- Context-free language U Context-free language = Context-free language  
- Context-free language CONCAT Context-free language = Context-free language  
- Context-free language * = Context-free language
- every dfa is an nfa but not vice versa, but there is an equivalent dfa for every nfa
- for conversion nfa to dfa or reverse, we should write a state transition diagram and the empty state place in nfa, means trap state in dfa
- in conversion when we face with multiple transition from one state, we cant handle that in dfa, so we should combine that multiple transition into one state: a -> {a,b} => dfa: a->{ab} and for that conceited state(transition diagram), we should look at the union of this two states: A -> {a} , B -> {empty} : ab -> {A} and so on we are moving forward in states, we should see that which one of the states still we doesn't talk about that, we go for that next and for final state, we should consider each state, that has previous final state on it, as final state     
  ![[IMG-20250609120720209.png]]
- to minimize a dfa we can use equivalent : ![[IMG-20250609123435414.png]]
- To minimize a DFA (Deterministic Finite Automaton), we follow these steps
		1. **Draw the State Transition Diagram** of the original DFA.
		2. **Construct the Initial Table for 0-Equivalence (P₀)**:
		    - Group the states into two sets:
		        - One set for **final (accepting)** states.
		        - Another set for **non-final** (non-accepting) states.
		3. **Refine the Partition to 1-Equivalence (P₁)**:
		    - For each group in P₀, compare all states **pairwise**.
		    - For each input symbol, check **which group the transition leads to**.
		    - If two states in the same group transition to **different groups** for any input, **split** the group.
		4. **Repeat Refinement for P₂, P₃, ..., until no more changes occur**:
		    - This process continues until the partition becomes stable (no more refinement).
		5. **Construct the Minimized DFA**:
		    - Each group from the final partition becomes a **single state** in the minimized DFA.
		    - The start state and final states are updated accordingly.
		- for unreachable states,(states that doesn't have any income) we remove that and proceed 
	- 