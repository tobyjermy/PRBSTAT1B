---
layout: default
title: "Lab 1 — Introduction to R"
---

# Lab 1 — Introduction to R

[← Back to Home](./)

---

## Exercise 1: Use R to do the following

Create a vector named "x" with elements -1, 2, 3, 0, 2, -1, 1, 4

```r
x = c(-1, 2, 3, 0, 2, -1, 1, 4)
```

Extract the 4th element of vector "x"

```r
x[4]
```

Extract as a single vector the 2nd, 3rd, 4th and 5th elements of "x".

```r
x[2:5]
```

What do `x[1 <= x & x <= 3]` and `x[x < 1 | x > 3]` yield?
Type these expressions in R and see what results you achieve!

Try setting `x[9] = 8` and `x[0] = -7`. Then look at the contents of x again typing `x` and `x[0]`. What do we notice?

Note that the first command adds a 9th element to x but the second command does not change x, since R starts at the first element rather than the 0th element. This is a key difference to what we see in Python and several other programming languages.

Create a vector named 'y' with elements 1/101, 2/101, …, 100/101

```r
y = c(1:100) / 101
```

Create a vector called 'z' that has 100 elements

```r
z = c(1:100)
```

The command `sum(v)` returns the sum of the elements of the vector 'v'. Find the sum of squares of the elements of 'y' above.

Type `sum(c(1,12)^3) - sum(c(9,10)^3)`. Why do we get a simple answer?

```r
sum(y^2)

sum(c(1, 12)^3) - sum(c(9, 10)^3)
12^3
1^3 + 12^3
9^3 + 10^3
```

Google: "Ramanujan taxi" to find out more.

Create vector 'a' with elements (1, 2, 3, 4, 5) and vector 'b' with elements (0, 6, 0, 4, 6). Try the commands:

- `a > 3`
- `a >= 3`
- `a > b`
- `max(a, b)`
- `pmax(a, b)`

Note that we apply `pmax` rather than `max` if we want to apply the maximum operation elementwise.

The natural exponential and logarithm functions are called `exp` and `log`. Use these to evaluate $e^{(\ln 2)^2}$

```r
exp(log(2)^2)
```

**Recycling.** When 'x' is a vector and 'h' is a number, the command `x + h` will add 'h' to each component of 'x'. If 'h' is a vector but the length of 'x' is a multiple of the length of 'h', R *recycles* the value of 'h' as many times as necessary to make a vector of the same length as 'x', and then adds this element-wise to 'x'.

Try the following commands:

```r
c(1, 1, 1, 1, 1, 1) + c(2, 3)
c(1, 1, 1, 1, 1) + c(2, 3)
```

The key observation is that the length of the longer vector must be a multiple of the length of the shorter vector.

---

## Exercise 2

> **Note:** The `?` function is very helpful in finding the right syntax in R. Try typing `?binom` or `?norm` in the console.

The R command `dbinom(x, n, prob)` calculates $\mathbb{P}[X = x]$ where $X \sim B(n, \text{prob})$.

The R command `pbinom(q, n, prob)` calculates $\mathbb{P}[X \leq q]$ for the same $X$.

Let's have a look at an example: finding $\mathbb{P}[X = 3]$ and $\mathbb{P}[X \leq 3]$ when $X \sim B(5, 0.3)$

```r
dbinom(3, 5, 0.3)
pbinom(3, 5, 0.3)
```

A balanced die is rolled 100 times. Let $X$ denote the number of times it shows a 6. Find two different ways of computing the probability that $X$ is at least 25, one based on `pbinom` and one based on `dbinom`.

```r
# Method 1
1 - pbinom(24, 100, 1/6)

# Method 2
sum = 0
for (x in (25:100))
{
  a = dbinom(x, 100, 1/6)
  sum = sum + a
}
sum
```

---

## Exercise 3

One hundred children rolled a die 10 times and counted the number of sixes. Simulate the outcome of this experiment.

```r
data = rbinom(100, 10, 1/6)
data
```

If 'x' and 'y' are vectors of length n, the R command `plot(x, y)` plots n points with the specified x and y coordinates. The command `plot(x, y, pch=20)` uses a prettier plotting character.

Plot your results for the 100 children, with the x coordinates being 1, …, 100, and the y coordinates the number of sixes obtained by each child.

```r
plot(c(1:100), data)
plot(c(1:100), data, pch = 20)
```

Plot the probability mass function of a $B(10, 1/6)$ RV

```r
pmass = dbinom(c(0:10), 10, 1/6)
pmass
plot(c(0:10), pmass)
```

Does the plot in (c) match with the result of the experiment?

```r
# We can compare values of pmass (or 100*pmass) with the plot in (b)
100 * pmass

# Find the observed numbers of 0,...,10 and compare these with expected numbers
count = rep(0, 11)
for (x in (0:10))
{
  count[x + 1] = sum(data == x)
}
count
100 * pmass    # Expected numbers of 0, ..., 10
```

---

[← Back to Home](./)
