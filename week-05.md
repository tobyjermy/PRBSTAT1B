---
layout: default
title: "Week 5 — Normal Distribution, Inverse CDF & Modes"
---

# Week 5 — Normal Distribution, Inverse CDF & Modes

[← Back to Home](./)

---

## Worked Exercises

### Exercise 1 — Normal Distribution (Heights)

$H$ = height (cm), with $H \sim N(175, 7^2)$.

**(a)** What % are over 185cm tall?

$$\mathbb{P}(X > 185) = \mathbb{P}\left(\frac{X - 175}{7} > \frac{185 - 175}{7}\right)$$

$$= \mathbb{P}\left(Z > \frac{10}{7}\right) = 1 - \mathbb{P}\left(Z \leq \frac{10}{7}\right) = 1 - \Phi\left(\frac{10}{7}\right)$$

$$= 0.0766$$

where $Z \sim N(0, 1)$. Use a calculator, table, or R.

**(b)** Among those who are at least 185cm tall, what proportion are more than 195cm tall?

$$\mathbb{P}(X > 195 \mid X > 185) = \frac{\mathbb{P}(X > 195 \cap X > 185)}{\mathbb{P}(X > 185)}$$

$$= \frac{\mathbb{P}(X > 195)}{\mathbb{P}(X > 185)} = \frac{0.0021}{0.0766} = 0.027$$

**(c)** Probability a man is shorter than 161cm?

$$\mathbb{P}(X < 161) = \mathbb{P}\left(\frac{X - 175}{7} < \frac{161 - 175}{7}\right) = \mathbb{P}(Z < -2) = \Phi(-2) \approx 0.025$$

By symmetry of the standard normal, $\Phi(-2) = 1 - \Phi(2) \approx 0.025$. This corresponds to the lower 2.5% tail.

---

### Exercise 2 — CDF and Inverse CDF Method

$$f_Y(y) = \begin{cases} \frac{1}{9}y^2 & 0 < y < 3 \\ 0 & \text{otherwise} \end{cases}$$

**(a)** Find the CDF.

For $0 < y < 3$:

$$\mathbb{P}(Y \leq y) = \int_0^y \frac{1}{9}w^2\,dw = \left[\frac{w^3}{27}\right]_0^y = \frac{y^3}{27}$$

Thus:

$$F_Y(y) = \begin{cases} 0 & y \leq 0 \\ \frac{y^3}{27} & 0 < y < 3 \\ 1 & y \geq 3 \end{cases}$$

**(b)** Inverse CDF method to generate samples from $Y$.

$F_Y: [0, 3] \to [0, 1]$, so $F_Y^{-1}: [0, 1] \to [0, 3]$.

We can input anything between 0 and 1 to $F^{-1}$ and we will get something from our distribution. Do this enough times and we get a clear picture of the distribution.

We choose to input $\text{Unif}(0, 1)$ observations!

Set $u = \frac{y^3}{27}$, then solving for $y$:

$$y = (27u)^{1/3}$$

Thus $F_Y^{-1}(u) = (27u)^{1/3}$ for $0 < u < 1$.

**Method:** Generate $U \sim \text{Unif}(0, 1)$ and set $Y = (27U)^{1/3}$.

---

### Exercise 3 — Median, Mean & Mode

**(a)** Suppose $X \sim \text{Binomial}(4, \frac{1}{2})$. Find the median of the distribution of $X$. Is this also the mode?

$$\mathbb{P}(X = 0) = \frac{1}{16}, \quad \mathbb{P}(X = 1) = \frac{4}{16}, \quad \mathbb{P}(X = 2) = \frac{6}{16}$$

$$\mathbb{P}(X = 3) = \frac{4}{16}, \quad \mathbb{P}(X = 4) = \frac{1}{16}$$

Since $\mathbb{P}(X \leq 2) = \frac{11}{16}$ and $\mathbb{P}(X \geq 2) = \frac{11}{16}$, the median is $m = 2$, also the mode!

**(b)** Mean, median and mode of $\text{Unif}(0, 20)$.

The mean and median of the $\text{Unif}(0, 20)$ distribution are both 10. Since the PDF is constant in $(0, 20)$, any value in this range could qualify as the mode.

**(c)** Mean, median, mode of $\text{Exp}(0.1)$.

$$f_T(t) = \begin{cases} 0 & t \leq 0 \\ 0.1\,e^{-0.1t} & t > 0 \end{cases} \qquad F_T(t) = \begin{cases} 0 & t \leq 0 \\ 1 - e^{-0.1t} & t > 0 \end{cases}$$

The mean is $\frac{1}{\lambda} = 10$.

The mode is $0$.

For the median, solve $1 - e^{-0.1t} = 0.5$ to obtain $t = 10\log 2$.

**(d)** Find the mode of $\text{Gamma}(\lambda, K)$ when $K > 1$. Is the mode equal to the mean?

The mode is the value of $x$ maximising:

$$f_X(x) = \frac{1}{\Gamma(K)}\lambda^K x^{K-1} e^{-\lambda x} \quad \text{for } x \geq 0$$

Or, we could maximise the log:

$$\log\{f_X(x)\} = \text{constant} + (K-1)\log x - \lambda x$$

$$\frac{d}{dx}\log\{f_X(x)\} = \frac{K-1}{x} - \lambda = 0 \quad \Longrightarrow \quad x = \frac{K-1}{\lambda}$$

Since $K > 1$:

$$\frac{d^2}{dx^2}\log\{f_X(x)\} = \frac{-(K-1)}{x^2} < 0$$

Thus this solution is indeed a maximum, and the mode is at:

$$\frac{K-1}{\lambda} \neq \frac{K}{\lambda} \quad \text{(the mean)}$$

---

## Hints for Problems to Hand In

**Q4(i)(b):** Split the probability into two cases.

**Q4(i)(c):** Find $c$ such that ($Z \sim N(0,1)$) $\mathbb{P}[Z > c] = 0.05$, and recover $X$.

**Q4(ii)(b):** Here $a = 1$, $b = -2$.

**Q6(a):** Use the law of the unconscious statistician to write $\mathbb{E}[e^{aX}]$ as an integral, and bring terms outside the integral.

**Q6(b):** You will need that $\Gamma(t + 1) = t\,\Gamma(t)$ for $t > 0$.

---

[← Back to Home](./)
