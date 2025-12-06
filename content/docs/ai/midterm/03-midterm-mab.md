---
title: MAB, midterm
description:  MAB, midterm
---


# 🚀 WEEK 3 — Multi-Armed Bandits (MAB)

Multi-Armed Bandits (MAB) model the problem of making decisions under uncertainty where:

- You repeatedly choose between several actions (“arms”).
- Each arm gives a stochastic (random) reward.
- You want to **maximize total reward over time** while learning which arm is best.

This creates the fundamental trade-off:

---

## 🔄 Exploration vs Exploitation

- **Exploration** → try different arms to gather information.
- **Exploitation** → choose the arm you currently believe is the best.

A good bandit algorithm must balance both.

---

# ⭐ PART 1 — Problem Setup and Expected Reward

Consider \(K\) arms. At each time step \(t = 1, 2, \dots, T\):

- You choose an arm \(a_t \in \{1, 2, \dots, K\}\).
- You receive a reward \(r_t\), drawn from an unknown distribution of that arm.

For each arm \(i\), the (unknown) **true expected reward** is:

$$
\mu_i = \mathbb{E}[R_i]
$$

But we do **not** know \(\mu_i\), so we estimate it using sample averages:

Let \(n_i(t)\) be the number of times we have played arm \(i\) up to time \(t\), and let \(r_{i,1}, r_{i,2}, \dots, r_{i,n_i}\) be the rewards observed from that arm.

The **empirical mean** (estimate) of arm \(i\) is:

$$
\hat{\mu}_i = \frac{1}{n_i} \sum_{k=1}^{n_i} r_{i,k}
$$

This \(\hat{\mu}_i\) is used in essentially all algorithms.

---

# ⭐ PART 2 — Regret (Very Important for Exams)

Regret measures how much reward we *lost* by not always playing the best arm.

Define:

- \(i^*\) = index of the best arm.
- \(\mu^* = \mu_{i^*}\) = expected reward of the best arm.
- At step \(t\), we choose arm \(a_t\) and receive reward \(r_t\).

**Cumulative regret after \(T\) rounds**:

$$
R_T = T \mu^* - \sum_{t=1}^T r_t
$$

Equivalently (in terms of expectations):

$$
R_T = \sum_{t=1}^T \bigl( \mu^* - \mu_{a_t} \bigr)
$$

Every bandit algorithm aims to make \(R_T\) as small as possible.

---

# ⭐ PART 3 — ε-Greedy Algorithm (Deep Explanation)

## 3.1 What is ε (epsilon)?

\(\epsilon\) is a **probability** that controls how often we explore:

- With probability \(\epsilon\): explore (pick a random arm).
- With probability \(1 - \epsilon\): exploit (pick the current best arm).

Typical exam values:

- \(\epsilon = 0.1\) → 10% exploration, 90% exploitation.
- \(\epsilon = 0.01\) → 1% exploration.

---

## 3.2 Why do we need ε?

Without exploration:

- The algorithm might try an arm a few times.
- Get lucky rewards for that arm.
- Think it’s the best arm.
- Never try other arms again.
- → It can get stuck in a suboptimal choice.

\(\epsilon\)-greedy forces the agent to sometimes try other arms.

---

## 3.3 Formal Definition of ε-Greedy

At time step \(t\), with current estimates \(\hat{\mu}_1, \dots, \hat{\mu}_K\):

- With probability \(\epsilon\): choose a random arm.
- With probability \(1 - \epsilon\): choose the arm with the highest estimated mean.

Mathematically:

$$
a_t =
\begin{cases}
\text{random arm in } \{1, \dots, K\}, & \text{with probability } \epsilon, \\
\displaystyle \arg\max_{i} \hat{\mu}_i, & \text{with probability } 1 - \epsilon.
\end{cases}
$$

---

## 3.4 Updating the Estimates

Each time we play arm \(i\), we observe a reward \(r\) and update $(\hat{\mu}_i)$.

The simple **sample mean** update:

$$
\hat{\mu}_i \leftarrow \frac{1}{n_i} \sum_{k=1}^{n_i} r_{i,k}
$$

Or using an incremental formula (often seen in code):

$$
\hat{\mu}_i \leftarrow \hat{\mu}_i + \frac{1}{n_i} \bigl( r - \hat{\mu}_i \bigr)
$$

Where:

- \(n_i\) is the count *after* observing this new reward.
- \(r\) is the newly observed reward.

---

## 3.5 How to Execute ε-Greedy — Step-by-Step

Assume:

- 2 arms: A and B.
- \(\epsilon = 0.1\).

**Step 0 — Initialization**

Set estimates (e.g.):

$$
\hat{\mu}_A = 0, \quad \hat{\mu}_B = 0
$$

Set counts:

$$
n_A = 0, \quad n_B = 0
$$

**Each round \(t\):**

1. Flip a biased coin:
   - With probability \(\epsilon\): choose a random arm.
   - With probability \(1 - \epsilon\): choose $(\arg\max(\hat{\mu}_A, \hat{\mu}_B))$.

2. Play chosen arm \(a_t\) and observe reward \(r_t\).

3. Update:
   - Increase $(n_{a_t} \leftarrow n_{a_t} + 1)$.
   - Update its estimate:
     $$
     \hat{\mu}_{a_t} \leftarrow \hat{\mu}_{a_t} + \frac{1}{n_{a_t}} \bigl( r_t - \hat{\mu}_{a_t} \bigr)
     $$

4. Repeat.

---

## 3.6 Intuition

ε-greedy means:

> “Most of the time, trust what you know (exploit),  
> but sometimes deliberately try something else (explore).”

It is simple and widely used, but explores randomly (no notion of confidence).

---

# ⭐ PART 4 — Adaptive ε-Greedy

## 4.1 Motivation

Fixed \(\epsilon\)-greedy will **keep** exploring at a constant rate forever, even after it has become clear which arm is best.

We’d like:

- High exploration early.
- Low exploration later.

---

## 4.2 Decaying ε Schedule

A common schedule is:

$$
\epsilon_t = \frac{1}{t}
$$

So:

- At \(t = 1\), \(\epsilon_1 = 1\) → pure exploration.
- At \(t = 10\), \(\epsilon_{10} = 0.1\).
- At \(t = 100\), \(\epsilon_{100} = 0.01\).

At time \(t\), the arm selection is:

$$
a_t =
\begin{cases}
\text{random arm}, & \text{with probability } \epsilon_t, \\
\displaystyle \arg\max_i \hat{\mu}_i, & \text{with probability } 1 - \epsilon_t.
\end{cases}
$$

The update of \(\hat{\mu}_i\) is the same as in standard ε-greedy.

---

## 4.3 Intuition

Early in learning:

- \(\epsilon_t\) is large → frequent exploration → we learn about all arms.

Later:

- \(\epsilon_t\) becomes very small → we mostly exploit the best arm.

This usually leads to **lower regret** than fixed \(\epsilon\)-greedy.

---

# ⭐ PART 5 — Optimistic Initial Values (OIV)

## 5.1 Problem It Solves

If we initialize all estimates at 0, the algorithm might:

- Try an arm a few times.
- Get a slightly better-than-average streak.
- Decide it’s the best.
- Never try some arms at all (if no forced exploration).

Optimistic initial values fix this by **encouraging exploration without randomness**.

---

## 5.2 Idea

Instead of starting with:

$$
\hat{\mu}_i(0) = 0,
$$

we start with a **large initial value**:

$$
\hat{\mu}_i(0) = Q_0
$$

for all arms \(i\), where \(Q_0\) is optimistic (e.g., 5, 10, 100, depending on reward scale).

---

## 5.3 Algorithm

1. Initialize:
   $$
   \hat{\mu}_i = Q_0, \quad n_i = 0, \quad \forall i.
   $$

2. At each time step \(t\):

   - Choose:
     $$
     a_t = \arg\max_i \hat{\mu}_i
     $$
     (no ε, no randomness needed — just greedily pick the highest estimated value).

   - Observe reward \(r_t\).

   - Update:
     $$
     n_{a_t} \leftarrow n_{a_t} + 1
     $$
     $$
     \hat{\mu}_{a_t} \leftarrow \hat{\mu}_{a_t} + \frac{1}{n_{a_t}} \bigl( r_t - \hat{\mu}_{a_t} \bigr)
     $$

---

## 5.4 Intuition

- At the beginning, **all arms look very good** because of \(Q_0\).
- When an arm is played a few times and gets realistic rewards, its estimate drops.
- Unplayed arms still have high estimates → the agent is “pulled” to try them.
- Eventually, estimates converge to realistic values, and the algorithm becomes purely greedy (always exploiting the best estimate).

This gives **forced exploration early**, then exploitation later.

---

# ⭐ PART 6 — UCB (Upper Confidence Bound)

UCB is a more **principled** method that balances exploration and exploitation using confidence intervals.

## 6.1 Idea

For each arm \(i\), UCB constructs an **upper confidence bound** on the mean reward:

- If we have:
  - High estimated mean \(\hat{\mu}_i\), or
  - High uncertainty (few samples),
  
  then that arm’s UCB value will be high.

We always choose the arm with the highest **UCB score**.

---

## 6.2 UCB Formula

For arm \(i\) at time \(t\):

$$
\text{UCB}_i(t) = \hat{\mu}_i + \sqrt{\frac{2 \ln t}{n_i}}
$$

Where:

- \(\hat{\mu}_i\) is the current estimated mean reward.
- \(t\) is the current time step (1, 2, …).
- \(n_i\) is how many times arm \(i\) has been played so far.

At each time step \(t\), we choose:

$$
a_t = \arg\max_i \text{UCB}_i(t)
$$

---

## 6.3 Interpretation

- The first term \(\hat{\mu}_i\) is the **exploitation** term (how good the arm seems).
- The second termd
  $$
  \sqrt{\frac{2 \ln t}{n_i}}
  $$
  is the **exploration bonus** (how uncertain we are about the arm).

Properties:

- If \(n_i\) is small → the bonus is large → we are uncertain → UCB tends to explore this arm.
- If \(n_i\) is large → the bonus shrinks → we are confident → UCB explores the arm less.

UCB thus **automatically explores arms that are uncertain** and exploits arms that are clearly good.

---

## 6.4 Step-by-Step Use of UCB

For each time step \(t\):

1. For each arm \(i\) that has been played at least once, compute:

   $$
   \text{UCB}_i(t) = \hat{\mu}_i + \sqrt{\frac{2 \ln t}{n_i}}
   $$

   If an arm has not been played yet, you can:
   - Force-play each arm once at the beginning, or
   - Treat its UCB as \(+\infty\) to ensure it gets tried.

2. Choose:
   $$
   a_t = \arg\max_i \text{UCB}_i(t)
   $$

3. Play arm \(a_t\), observe reward \(r_t\).

4. Update:
   $$
   n_{a_t} \leftarrow n_{a_t} + 1
   $$
   $$
   \hat{\mu}_{a_t} \leftarrow \hat{\mu}_{a_t} + \frac{1}{n_{a_t}} \bigl( r_t - \hat{\mu}_{a_t} \bigr)
   $$

5. Go to the next step \(t+1\).

---

# ⭐ PART 7 — Algorithm Comparison Cheat Sheet

| Algorithm               | Exploration Mechanism                         | Exploitation Mechanism            | Notes                              |
|------------------------|-----------------------------------------------|-----------------------------------|------------------------------------|
| ε-Greedy               | Random with prob. \(\epsilon\)                | Greedy on \(\hat{\mu}_i\)         | Simple, easy to implement          |
| Adaptive ε-Greedy      | \(\epsilon_t = 1/t\) (shrinks over time)      | Greedy on \(\hat{\mu}_i\)         | Less random later, lower regret    |
| Optimistic Init Values | High initial \(\hat{\mu}_i(0) = Q_0\)         | Always pick max \(\hat{\mu}_i\)   | Forced early exploration           |
| UCB                    | Bonus term \(\sqrt{(2 \ln t)/n_i}\)           | Uses both mean + bonus            | Strong theoretical guarantees      |

---

# ⭐ PART 8 — Regret Example

Suppose the best arm has expected reward:

$$
\mu^* = 10
$$

You choose arms with these expected rewards in 3 rounds:

- Round 1: reward mean \(= 7\)
- Round 2: reward mean \(= 10\)
- Round 3: reward mean \(= 9\)

Then the regret after 3 rounds is:

$$
R_3 = (10 - 7) + (10 - 10) + (10 - 9) = 3 + 0 + 1 = 4
$$

Exam questions often give you such tables and ask you to compute regret.

---

# ⭐ WEEK 3 SUMMARY

### Concepts:
- MAB problem setup.
- Exploration vs exploitation.
- Estimating expected rewards with sample means.
- Regret definition and computation.

### Algorithms:
- ε-Greedy.
- Adaptive ε-Greedy.
- Optimistic Initial Values.
- UCB.

### Exam Skills:
- Track \(\hat{\mu}_i\) and \(n_i\) in a table.
- Apply each algorithm step-by-step.
- Compute regret.
- Explain differences between algorithms.

