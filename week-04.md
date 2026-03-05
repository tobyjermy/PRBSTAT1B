---
layout: default
title: "Lab 2 — Histograms, Normal Approximation & Random Number Generation"
published: false
---

# Lab 2 — Histograms, Normal Approximation & Random Number Generation

[← Back to Home](./)

---

## Exercise 1

**(a)** Use R to create a vector `x` containing 1000 independent realisations from the $N(3, 4^2)$ distribution.

```r
x = rnorm(1000, 3, 4)
```

**(b)** Plot a histogram of `x`. Use the option `prob=TRUE` in `hist` to show probability density on the y-axis: with this option, the scale implies that the area of each block in the histogram is equal to a probability. Plot the histogram again but this time give a title by including `main="Observed X values"` in the `hist` command, and write `xlab="X values"` and `ylab="Density of the distribution"` to label the axes.

```r
hist(x, prob=TRUE, main="Observed X values",
     xlab="X values", ylab="Density of the distribution")
```

**(c)** Add the PDF of the $N(3, 4^2)$ distribution to the plot in red. The PDF should match the histogram.

```r
hist(x, prob=TRUE, main="Observed X values",
     xlab="X values", ylab="Density of the distribution")
curve(dnorm(x, 3, 4), add=TRUE, col="red")
```

---

## Exercise 2

A fair die is rolled 1000 times. Find the probability that 4 appears between 150 and 180 times inclusively.

**(1)** Use `pbinom` to obtain the binomial probability exactly. The command `pbinom(x, n, p)` returns $\mathbb{P}(X \leq x)$ for $X \sim \text{Binomial}(n, p)$.

```r
pb2 = pbinom(180, 1000, 1/6)
pb1 = pbinom(149, 1000, 1/6)
pb  = pb2 - pb1
pb1
pb2
pb
```

Run the following code and investigate the output. The answer is `pb`.

**(2)** We can approximate the distribution of a binomial random variable $X \sim \text{Binomial}(n, p)$ by that of a normal RV $Y \sim N(np,\; np(1-p))$, which implies $\mathbb{P}\{X \leq x\} \approx \mathbb{P}\{Y \leq x\}$. One may try to improve this approximation by applying a **continuity correction**:

$$\mathbb{P}\{X < x\} \approx \mathbb{P}\{Y \leq x - 0.5\}$$

$$\mathbb{P}\{X \leq x\} \approx \mathbb{P}\{Y \leq x + 0.5\}$$

Use `pnorm` to evaluate the normal approximation to $\mathbb{P}\{150 \leq X \leq 180\}$, where $X$ denotes the number of times a 4 appears in 1000 rolls of a fair die. Do this with and without the continuity correction.

**With continuity correction:**

```r
mu = 1000 * (1/6)
sd = sqrt(1000 * (1/6) * (5/6))

pnc1 = pnorm(149.5, mu, sd)
pnc2 = pnorm(180.5, mu, sd)
pnc  = pnc2 - pnc1
pnc1
pnc2
pnc
```

The answer is `pnc`.

**Without continuity correction:**

```r
pn1 = pnorm(149, mu, sd)
pn2 = pnorm(180, mu, sd)
pn  = pn2 - pn1
pn1
pn2
pn
```

The answer is `pn`.

> **Question to think about:** Which method (continuity or non-continuity correction) gives the more accurate answer?

---

## Exercise 3

In Lecture 9, you will discuss how R produces random numbers. Here is a practical introduction to a key method, the **linear congruential generator**.

**(i)** Write a function to generate pseudo-random values from a $\text{Uniform}(0, 1)$ distribution using a linear congruential generator, as follows.

Set $m$, $a$ and $c$ to be:

$$m = 2^{32}, \quad a = 1664525, \quad c = 1013904223$$

Initiate the sequence $\{X_i\}$ by assigning a value to $X_1$, then calculate $X_2, X_3, \ldots$ according to the rule:

$$X_{n+1} = (aX_n + c) \bmod m$$

Finally, divide by $m$ to produce pseudo-random $\text{Uniform}(0, 1)$ RVs:

$$U_n = X_n / m, \quad n = 1, 2, \ldots$$

Theory tells us that this process will produce a sequence $\{X_1, \ldots, X_m\}$ containing a permutation of the integers $\{0, 1, \ldots, m-1\}$ in what appears to be a random order, and then the sequence will be repeated. Consequently, $\{U_1, \ldots, U_m\}$ should behave like a sequence of independent $\text{Uniform}(0, 1)$ random variables.

```r
set.seed(12345)

rgen = function(nreps, seed)
{
  m = 2^32
  a = 1664525
  c = 1013904223
  random.numbers = rep(0, nreps)
  for (i in c(1:nreps))
  {
    seed = (a * seed + c) %% m
    random.numbers[i] = seed / m
  }
  return(random.numbers)
}

seed  = 1234
nreps = 10^4
xx    = rgen(nreps, seed)
hist(xx)
```

**(ii)** Each of 100 squirrels buries an acorn in a 10m × 10m square of ground. For each squirrel, the coordinates $X$ and $Y$ of the location of its acorn (measured in metres) are independent $\text{Uniform}(0, 10)$ RVs.

**(a)** Using the random number generator from (i), simulate this process by generating vectors `X_coord` and `Y_coord`, each of length 100. Remember that if $X \sim \text{Uniform}(0, 1)$, then $10X \sim \text{Uniform}(0, 10)$.

```r
Xcoord = rgen(100, 12345) * 10
Ycoord = rgen(100, 54321) * 10
```

**(b)** Plot `Ycoord` against `Xcoord` to produce a map of the 100 acorn locations.

```r
plot(Xcoord, Ycoord)
```

**(c)** See if you can spot any patterns in the above plot! Although our brains are good at finding patterns, the plot we have produced is truly random.

**(d)** Repeat the set of commands used in (c) four times, with different random number sequences, to produce 4 independent plots of 100 acorns each.

```r
par(mfrow = c(2, 2))  # To give 4 plots in the graphics window
for (irep in c(1:4))
{
  Xcoord = rgen(100, 10 * irep) * 10
  Ycoord = rgen(100, 10 * irep + 1) * 10
  plot(Xcoord, Ycoord)
}
```

Set the plot space back to normal:

```r
par(mfrow = c(1, 1))
```

---

[← Back to Home](./)
