## Worked Exercises

### Exercise 1 — Fair Coin Tossed 3 Times

A fair coin is tossed 3 times. Outcomes are noted in order.

**(a)** The sample space is:

$$\Omega = \{HHH,\; HHT,\; HTH,\; HTT,\; THH,\; THT,\; TTH,\; TTT\}$$

Since the coin is fair, each outcome is equally likely. So for any event $A \subseteq \Omega$:

$$\mathbb{P}(A) = \frac{|A|}{|\Omega|}$$

**(b)** Let $A_i = \{\text{the } i\text{th toss is H}\}$ for $i = 1, 2, 3$.

$$A_1 = \{HHH,\; HHT,\; HTH,\; HTT\}$$

$$A_2 = \{HHH,\; HHT,\; THH,\; THT\}$$

$$A_3 = \{HHH,\; HTH,\; THH,\; TTH\}$$

**(c)** $A_i$ and $A_j$ for $i \neq j$ appear to share elements, so they should **not** be disjoint. For example:

$$A_1 \cap A_2 = \{HHH,\; HHT\} \neq \emptyset$$

**(d)** For each event: $\mathbb{P}(A_i) = \frac{1}{2}$ and $\mathbb{P}(A_i \cap A_j) = \frac{1}{4}$.

Thus for any $i, j$:

$$\mathbb{P}(A_i \cap A_j) = \frac{1}{4} = \frac{1}{2} \times \frac{1}{2} = \mathbb{P}(A_i)\,\mathbb{P}(A_j)$$

**Yes, they are independent.**

**(e)** Let $S$ = total number of H's in three tosses. This is a random variable $S: \Omega \to \mathbb{R}$.

$$S(HHH) = 3, \quad S(HHT) = 2, \quad S(HTH) = 2$$

$$S(HTT) = 1, \quad S(THH) = 2, \quad S(THT) = 1$$

$$S(TTH) = 1, \quad S(TTT) = 0$$

**(f)** For each $\omega \in \Omega$, $i \in \{1, 2, 3\}$:

$$\mathbb{1}_{A_i}(\omega) = \begin{cases} 1 & \text{if } \omega \in A_i \\ 0 & \text{if } \omega \notin A_i \end{cases}$$

These are functions on $\Omega \to \mathbb{R}$ — **indicator variables!** Indeed:

$$S = \mathbb{1}_{A_1} + \mathbb{1}_{A_2} + \mathbb{1}_{A_3}$$

---

### Exercise 2 — Sum of Independent Poissons

$X_1, X_2$ are non-negative integers, so is $X_1 + X_2$ — so it will likely be Poisson...

$$\mathbb{P}(X_1 + X_2 = n) = \sum_{k=-\infty}^{\infty} \mathbb{P}(X_1 = k)\,\mathbb{P}(X_2 = n - k)$$

For $k < 0$: $\mathbb{P}(X_1 = k) = 0$ (non-negative).
For $k > n$: $\mathbb{P}(X_2 = n - k) = 0$ (non-negative).

So:

$$= \sum_{k=0}^{n} \mathbb{P}(X_1 = k)\,\mathbb{P}(X_2 = n - k)$$

$$= \sum_{k=0}^{n} e^{-\lambda}\frac{\lambda^k}{k!} \cdot e^{-\mu}\frac{\mu^{n-k}}{(n-k)!}$$

$$= e^{-(\lambda + \mu)} \frac{1}{n!} \sum_{k=0}^{n} \frac{n!}{k!(n-k)!}\,\lambda^k\,\mu^{n-k}$$

$$= e^{-(\lambda + \mu)} \frac{1}{n!}(\lambda + \mu)^n \sim \text{Pois}(\lambda + \mu)$$

---

### Exercise 3 — Uniform Distribution

$X \sim \text{Unif}(5, 10)$.

$$\mathbb{P}(X \in (7, 8)) = \int_7^8 \frac{1}{5}\,dx = \frac{1}{5}$$

and

$$\mathbb{P}(X > 6) = \int_6^{10} \frac{1}{5}\,dx = \frac{4}{5}$$

Finally,

$$\mathbb{P}(X \in (7, 8) \mid X > 6) = \frac{\mathbb{P}(X \in (7, 8) \text{ and } X > 6)}{\mathbb{P}(X > 6)} = \frac{\mathbb{P}(X \in (7, 8))}{\mathbb{P}(X > 6)} = \frac{1/5}{4/5} = \frac{1}{4}$$

---

## Problems to Hand In

**Please hand in Q4, Q5, Q6.**

**Hint for Q6:** Draw a joint probability table like this:

|       | $X = -1$ | $X = 0$ | $X = 1$ | Marginals |
|-------|----------|---------|---------|-----------|
| $Y = -1$ |          |         |         |           |
| $Y = 0$  |          |         |         |           |
| $Y = 1$  |          |         |         |           |
| **Marginals** |    |         |         | **Sums to 1** |

> **Reminder:** Lab next week.
