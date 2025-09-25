# Lecture Notes for Sep 16, 2025

## Overview

Determining whether you need to **prove** or **disprove** is a grey area.

## Overshooting (loose bound)

We do a guess that totally fits in.

### Basis

$$T(n) = 2T(\frac{n}{2}) + 2$$
$$T(n) = O(n^2)$$
$$T(n) \leq cn^2$$

### Inductive Hypothesis

It holds for $k<n$, specifically $k=\frac{n}{2}$.

$$=> T(\frac{n}{2}) \leq c(\frac{n}{2})^2$$

### Substitution

Replace $T(\frac{n}{2})$ with $c(\frac{n}{2})^2$.

$$T(n) = 2T(\frac{n}{2})$$
$$T(n) \leq 2c(\frac{n}{2})^2 + n$$

### Completion

$$T(n) \leq \frac{n}{2}n^2 + n \leq cn^2$$
$$\frac{n}{2} + \frac{1}{c} \leq n$$
$$\frac{2}{c} \leq n$$


$\frac{2}{c} \leq n$ holds for $c=2$ and $n_0 \get 1$. **Proved!!!**

_Note: not a tight bound, so you can't flip the_ $\leq$.

## Undershooting



## Run extended form of guess



