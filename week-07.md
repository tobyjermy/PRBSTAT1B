---
layout: default
title: "Week 7 — Maximum Likelihood & Method of Moments"
---

# Week 7 — Maximum Likelihood & Method of Moments

[← Back to Home](./)

---

## Worked Exercises

### Exercise 1 — MLE for a Discrete Distribution

$X_1, \ldots, X_n$ are i.i.d. discrete RVs with PMF:

$$p_{X_i}(x_i) = \mathbb{P}(X_i = x_i) = \binom{x_i + 2}{x_i}(1 - \psi)^3 \psi^{x_i}$$

for $x_i \in \{0, 1, 2, \ldots\}$ and $0 \leq \psi < 1$.

**(a)** Likelihood function for observed $\mathbf{x}$:

"Explain what likelihood actually means."

$$\mathcal{L}(\psi, \mathbf{x}) = \prod_{i=1}^{n} \binom{x_i + 2}{x_i} (1 - \psi)^{3n} \psi^{\sum_{i=1}^{n} x_i}$$

Log-likelihood:

$$\ell(\psi, \mathbf{x}) = \sum_{i=1}^{n} \log\binom{x_i + 2}{x_i} + 3n\log(1 - \psi) + \left(\sum_{i=1}^{n} x_i\right)\log\psi$$

Find the maximum by setting the derivative to zero:

$$\frac{d}{d\psi}\ell(\psi, \mathbf{x}) = \frac{-3n}{1 - \psi} + \frac{\sum_{i=1}^{n} x_i}{\psi} = 0$$

Solving:

$$\hat{\psi} = \frac{\sum_{i=1}^{n} x_i}{3n + \sum_{i=1}^{n} x_i} \qquad \text{(Maximum likelihood estimate)}$$

Checking that this is indeed a maximum:

$$\frac{d^2}{d\psi^2}\ell(\psi, \mathbf{x}) = \frac{-3n}{(1 - \psi)^2} - \frac{\sum_{i=1}^{n} x_i}{\psi^2} < 0 \quad \forall\, \psi \in (0, 1)$$

since we know $\sum_{i=1}^{n} x_i > 0$. Thus this is indeed a maximum.

**(b)** What if $\sum_{i=1}^{n} x_i = 0$? Then $X_i = 0$ for all $i = 1, \ldots, n$.

$$\mathcal{L}(\psi, \mathbf{x}) = \prod_{i=1}^{n} \binom{2}{0}(1 - \psi)^3 = (1 - \psi)^{3n}$$

This is a decreasing function of $\psi$, so the maximum over $\psi \in [0, 1]$ occurs at $\psi = 0$.

$$\Longrightarrow \hat{\psi} = 0$$

**(c)** In both cases, the ML estimate is:

$$\hat{\psi} = \frac{\sum_{i=1}^{n} x_i}{3n + \sum_{i=1}^{n} x_i}$$

Hence the ML **estimator** is the random variable:

$$\hat{\Psi} = \frac{\sum_{i=1}^{n} X_i}{3n + \sum_{i=1}^{n} X_i}$$

---

### Exercise 2 — MLE for a Continuous Distribution

Now $X_1, \ldots, X_n$ are i.i.d. continuous with PDF:

$$f_{X_i}(x_i) = \frac{1}{\mu^2}x_i\,e^{-x_i/\mu} \quad \text{for } x > 0, \quad \text{and } f_{X_i}(x_i) = 0 \text{ otherwise.}$$

**(a)** Likelihood:

$$\mathcal{L}(\mu, \mathbf{x}) = \prod_{i=1}^{n} \frac{1}{\mu^2}x_i\,e^{-x_i/\mu} = \mu^{-2n}\left(\prod_{i=1}^{n} x_i\right)\exp\left\{-\frac{1}{\mu}\sum_{i=1}^{n} x_i\right\}$$

for $\mu > 0$.

Thus, as a function of $\mu$:

$$\ell(\mu, \mathbf{x}) = \text{constant} - 2n\log\mu - \frac{\sum_{i=1}^{n} x_i}{\mu} \quad \text{for } \mu > 0$$

$$\frac{d}{d\mu}\ell(\mu, \mathbf{x}) = -\frac{2n}{\mu} + \frac{\sum_{i=1}^{n} x_i}{\mu^2} = 0 \quad \text{for the maximum}$$

which yields:

$$\hat{\mu} = \frac{1}{2n}\sum_{i=1}^{n} x_i$$

Second derivative:

$$\frac{d^2}{d\mu^2}\ell(\mu, \mathbf{x}) = \frac{2n}{\mu^2} - \frac{2\sum_{i=1}^{n} x_i}{\mu^3}$$

We cannot argue that the 2nd derivative is always negative — it's positive for large $\mu$. But:

- $\frac{d}{d\mu}\ell > 0$ for $0 < \mu < \frac{\sum x_i}{2n}$
- $\frac{d}{d\mu}\ell < 0$ for $\mu > \frac{\sum x_i}{2n}$

So this must be the ML estimate.

**(b)** The maximum likelihood **estimator** of $\mu$ is:

$$\hat{\mu} = \frac{\sum_{i=1}^{n} X_i}{2n} \qquad \text{(which is a random variable)}$$

---

### Exercise 3 — Method of Moments

**(a)** Good guesses for the distributions: $X \sim \text{Gamma}$, $Y \sim \text{Normal}$, $Z \sim \text{Exponential}$.

**(b)(i)** If $X \sim \text{Gamma}(\lambda, K)$: $\mathbb{E}[X] = \frac{K}{\lambda}$, $\text{Var}(X) = \frac{K}{\lambda^2}$.

So $\mathbb{E}[X^2] = \frac{K(K+1)}{\lambda^2}$.

Using the method of moments:

$$\frac{K}{\lambda} = \frac{1}{200}\sum_{i=1}^{n} x_i = \frac{155.6}{200} = 0.778$$

$$\frac{K}{\lambda^2} + \left(\frac{K}{\lambda}\right)^2 = \frac{1}{200}\sum_{i=1}^{n} x_i^2 = \frac{156.2}{200} = 0.781$$

$$\Longrightarrow \frac{K}{\lambda^2} = 0.781 - 0.778^2 = 0.1757$$

And thus the estimates are:

$$\hat{\lambda} = \frac{0.778}{0.1757} = 4.428, \qquad \hat{K} = 0.778\hat{\lambda} = 3.45$$

**(b)(ii)** If $Y \sim N(\mu, \sigma^2)$ then $\mathbb{E}[Y] = \mu$, $\mathbb{E}[Y^2] = \sigma^2 + \mu^2$.

Using the method of moments:

$$\hat{\mu} = \frac{1}{200}\sum_{i=1}^{200} y_i = \frac{1}{200} \cdot 4051.5 = 20.26$$

$$\hat{\sigma}^2 + \hat{\mu}^2 = \frac{1}{200} \cdot 83644.6 = 418.223$$

$$\hat{\sigma}^2 = 418.223 - \hat{\mu}^2 = 7.86$$

---

## Hints for Problems to Hand In

**Q4:** The case where $\sum_{i=1}^{n} y_i + \sum_{j=1}^{m} w_j = 0$ needs to be treated separately since one of the factors in the likelihood disappears.

**Q6(b):** Experiment with data sets where all but two observations are close to 0, whilst the other two take values $-d$ and $d$ for a fairly large value $d$.

---

[← Back to Home](./)
