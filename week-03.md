---
layout: default
title: "Week 3 — CDFs, Transformations & Waiting Times"
---

# Week 3 — CDFs, Transformations & Waiting Times

[← Back to Home](./)

---

## Worked Exercises

### Exercise 1 — Finding a CDF and Moments

$$f_X(x) = \begin{cases} cx^2 & \text{if } 0 < x < 1 \\ 0 & \text{otherwise} \end{cases}$$

**(a)** Find the CDF of $X$, and deduce $c$.

For $0 < x < 1$:

$$F_X(x) = \int_{-\infty}^{x} f_X(u)\,du = \int_0^x cu^2\,du = \frac{cx^3}{3}$$

Thus:

$$F(x) = \begin{cases} 0 & x < 0 \\ \frac{cx^3}{3} & 0 \leq x \leq 1 \\ \frac{c}{3} & x > 1 \end{cases}$$

For $F_X(x) = 1$ for all $x > 1$, we need that $c = 3$. So:

$$F(x) = \begin{cases} 0 & x < 0 \\ x^3 & 0 \leq x \leq 1 \\ 1 & x > 1 \end{cases}$$

**(b)** Find $\mathbb{P}(0.5 < X < 0.75)$.

$$= \mathbb{P}(X < 0.75) - \mathbb{P}(X \leq 0.5)$$

$$= F_X(0.75) - F_X(0.5)$$

$$= 0.75^3 - 0.5^3 = 0.297$$

**(c)** Calculate $\mathbb{E}[X]$ and $\text{Var}(X)$.

$$\mathbb{E}[X] = \int_{-\infty}^{\infty} x\,f_X(x)\,dx = \int_0^1 3x^3\,dx = \frac{3}{4}$$

$$\mathbb{E}[X^2] = \int_{-\infty}^{\infty} x^2\,f_X(x)\,dx = \int_0^1 3x^4\,dx = \frac{3}{5}$$

Thus:

$$\text{Var}(X) = \mathbb{E}[X^2] - \mathbb{E}[X]^2 = \frac{3}{5} - \left(\frac{3}{4}\right)^2 = \frac{3}{80}$$

---

### Exercise 2 — Transformation Formula (Uniform)

Suppose $Y \sim \text{Unif}(\theta, \phi)$ and $Z = a + bY$ where $b > 0$. Use the transformation formula to find the distribution of $Z$.

$$f_Y(y) = \begin{cases} \frac{1}{\phi - \theta} & \theta < y < \phi \\ 0 & \text{otherwise} \end{cases}$$

We have $Z = g(Y)$ where $g(y) = a + by$. The inverse of $g$ is:

$$g^{-1}(z) = \frac{z - a}{b}$$

We know $\mathbb{P}(0 < Y < \phi) = 1$, so $\mathbb{P}(a + b\theta < Z < a + b\phi) = 1$.

Apply the transformation formula for $Z$ in this range:

$$\boxed{f_Z(z) = f_Y(g^{-1}(z)) \cdot \frac{d}{dz}g^{-1}(z) = \frac{1}{\phi - \theta} \cdot \frac{1}{b}}$$

for $a + b\theta < z < a + b\phi$.

Thus, $Z \sim \text{Unif}(a + b\theta,\; a + b\phi)$.

**Reproducing the result from Lecture 5:**

Take $\theta = 0$, $\phi = 1$. Then if $Y \sim \text{Unif}(0, 1)$ and $Z = a + (b - a)Y$:

$$Z \sim \text{Unif}(a + (b-a) \cdot 0,\; a + (b-a) \cdot 1) = \text{Unif}(a, b)$$

---

### Exercise 3 — Bus Waiting Time

Time measured in minutes after 5pm. Buses arrive at 5:05, 5:25, 5:45, and 6:00.

- $T$ = time when next bus arrives
- $W$ = waiting time until next bus arrives

**(a)** The only possible values for $T$ are 5, 25, 45, 60, so it must be discrete.

Let $X$ = Glinda's arrival time after 5pm, with $X \sim \text{Unif}(0, 60)$.

$$\mathbb{P}(T = 5) = \frac{5}{60} = \frac{1}{12}, \quad \mathbb{P}(T = 25) = \frac{20}{60} = \frac{1}{3}$$

$$\mathbb{P}(T = 45) = \frac{20}{60} = \frac{1}{3}, \quad \mathbb{P}(T = 60) = \frac{15}{60} = \frac{1}{4}$$

**(b)** Find the CDF of $W$ by cases.

**Case 1:** $w < 0$. Can't have a negative waiting time, so $\mathbb{P}(W \leq w) = 0$.

**Case 2:** $w > 20$. All possible waiting times are less than 20, so $\mathbb{P}(W \leq w) = 1$.

**Case 3:** $0 \leq w < 5$. Glinda must arrive within $w$ minutes before each bus. There are 4 such windows of width $w$:

$$\mathbb{P}(W \leq w) = \frac{4w}{60} = \frac{w}{15}$$

**Case 4:** $5 \leq w < 15$. The first bus gap is only 5 mins, so that window is always captured. The other three windows have width $w$:

$$\mathbb{P}(W \leq w) = \frac{5 + 3w}{60}$$

**Case 5:** $15 \leq w < 20$. Two gaps are always captured ($\leq w$), plus two windows of width $w$:

$$\mathbb{P}(W \leq w) = \frac{20 + 2w}{60} = \frac{w + 10}{30}$$

Thus:

$$F_W(w) = \begin{cases} 0 & w < 0 \\ \frac{w}{15} & 0 \leq w < 5 \\ \frac{5 + 3w}{60} & 5 \leq w < 15 \\ \frac{10 + w}{30} & 15 \leq w < 20 \\ 1 & w \geq 20 \end{cases}$$

**(c)** Find the PDF by differentiating $F_W(w)$:

$$f_W(w) = \frac{d}{dw}F_W(w) = \begin{cases} \frac{1}{15} & 0 < w < 5 \\ \frac{1}{20} & 5 < w < 15 \\ \frac{1}{30} & 15 < w < 20 \\ 0 & \text{otherwise} \end{cases}$$

**(d)** To find $\mathbb{E}[W]$:

$$\mathbb{E}[W] = \int_{-\infty}^{\infty} w\,f_W(w)\,dw = \int_0^5 \frac{4w}{60}\,dw + \int_5^{15} \frac{3w}{60}\,dw + \int_{15}^{20} \frac{2w}{60}\,dw = 8.75$$

---

### Exercise 7 (Additional) — Tail Expectation Formula

Suppose $X$ is a continuous RV taking only positive values, and there is an upper limit $a$ on values it can take.

**Prove that:**

$$\mathbb{E}[X] = \int_0^{\infty} \mathbb{P}(X > x)\,dx$$

Recall $\mathbb{E}[X] = \int_0^a x\,f_X(x)\,dx$ (here $\mathbb{P}(X \geq 0) = 1$).

Apply integration by parts with $u = x$ and $v = -(1 - F_X(x))$ (by the hint), so $u' = 1$ and $v' = f_X(x)$.

This gives:

$$\int_{\mathbb{R}} x\,f_X(x)\,dx = \int_0^a x\,f_X(x)\,dx$$

$$= \Big[-x(1 - F_X(x))\Big]_0^a + \int_0^a 1 - F_X(x)\,dx$$

$$= 0 + \int_0^a 1 - F_X(x)\,dx = \int_0^{\infty} \mathbb{P}(X > x)\,dx \qquad \blacksquare$$

---

## Hints for Problems to Hand In

**Q5(a):** Calculate the area of each section of the target and use $\mathbb{P}(A)$.

**Q5(b):** Easier to find the CDF and differentiate to get the PDF. Use $\mathbb{P}[Y \leq y] = \mathbb{P}[\text{distance from centre} \leq yR]$ for $y \in [0, 3]$.

**Q6:** $(X_1, Y_1), \ldots, (X_K, Y_K)$ are i.i.d. For $\mathbb{P}[T = t \text{ and } (X^*, Y^*) \in B]$: use the independence property. In the second part of the question, you will need the formula for a geometric sum.

---

## Important Notes

- **PS1:** Well answered — remember to state i.i.d.
- **Lab Sheet 1:** Due on Moodle **Friday 20th, 5pm**. Solutions returned by next Friday.
- **Lab next week:** Start on assessed coursework.

---

[← Back to Home](./)
