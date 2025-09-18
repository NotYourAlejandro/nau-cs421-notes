# Lecture Notes for Sep 16, 2025 - Substitution Method

_These notes are incomplete. Please watch the Sep 16 lecture and finish them._

This topic is **very difficult** to understand since it's an **abstract concept**. Take your time to read and **understand** it. Talk to _Dr. Otte_ if you still don't get it. Otherwise refer to the Sep 16 lecture on Canvas.

This is the **second** of the 3 methods to getting the runtime of an algorithm:
- Induction Method
- **Substitution Method**
- Master Method

## Overview

The **substitution method** is based on **induction**. It **verifies** a perceived solution, not **solve a recurrence**.

The substitution method **shows** the lower **or** upper bound. If you want both, do the upper and lower bounds individually.

## Comparing the Induction and Substitution Methods

For these examples, we'll be proving:

**something** (fill in later)

### Induction Method

Proof: $$ \sum_{i = 1}^{u} = \frac{u}{2}(u + 1) $$

**Base Case:**

$$\text{holds for } i = 1$$
$$\sum_{i = 1}^{1} i = \frac{1}{2}(1 + 1) = 1$$
$$\text{This is correct!}$$

**Inductive Hypothesis:**

$$\text{assume holds for } k \leq n$$
$$=> \sum_{i = 1}^{k} i = \frac{k}{2}(k + 1)$$

**Inductive Step:**

$$\text{...holds for successor}$$
$$=> \sum_{i = 1}^{k + 1} i = \sum_{i = 1}^{k} i + (k + 1)$$
$$\text{also } \sum_{i = 1}^{k + 1} i = \frac{k + 1}{2}(k + 2)$$
$$\text{These need to be equal!}$$

**Substitution:**

Now, we **substitute** the inductive step with the hypothesis.

$$\text{also } \sum_{i = 1}^{k + 1} i = \frac{k + 1}{2}(k + 2)$$

**Completion:**

$$\text{show equality}$$
$$\frac{k}{2}(k+1) + (k+1) = \frac{k+1}{2}(k+2)$$

### Substitution Method

**Proof:**

$$T(n) = 2T(\frac{n}{2}) + n$$

Where:

$$T(n) = O(n\lg{n})$$
$$T(n) \leq cn\lg{n}$$

**Base Case:**

see book _(grumble grumble)_

**Inductive Hypothesis:**

This holds for $k < n$, specifically for $k = \frac{n}{2}$

$$=> T(\frac{n}{2}) \leq c\frac{n}{2} \lg{\frac{n}{2}}$$

**Inductive Step:**

$$T(n) = 2T(\frac{n}{2})+n$$

We have an implicit **predecessor-successor** relationship via recurrence.

- Predecessor: $T(\frac{n}{2})$
- Successor: $T(n)$

**Substitution:**

Per **inductive hypothesis**, substitute $T(\frac{n}{2})$.

_(there's more here I missed)_

**Completion:**

This shows that the inequality holds.

$$T(n) \leq cn\lg{\frac{n}{2}} + n \leq cn\lg{n}$$

_(there's more here I missed)_


### Template Solution

**Example**:

Prove that $T(n) = 2T(\frac{n}{2}) + n => T(n) = O(n\lg{n})$

**Proof**:

1. Obtain the $\frac{n}{2}$ from the recurrence.
2. Rewrite $T(n) = O(n\lg{n})$ as $T(n) \leq cn\lg{n}$

_Make sure you do step 2! It's important!_

**Inductive Hypothesis**:

1. Set $k = \frac{n}{2}$ _(chosen from proof)_
2. Substitute $k$ into the simplified solution.

$$=> T(\frac{n}{2}) \leq c(\frac{n}{2})\lg{n}$$

This is used for the **upper bound** proof.

**Substitution**:

Replace the **recurive term** with the **non-recursive term**. **Substitute** the $c(\frac{n}{2})\lg{n}$ into the original equation, then **simplify**.

$$T(n) = 2T(\frac{n}{2}) + n$$
$$T(n) = 2c(\frac{n}{2})\lg{n} + n$$

**Completion**:

$$T(n) \leq cn\lg{\frac{n}{2}} + n \leq cn\lg{n}$$
$$\lg{\frac{n}{2}} + \frac{1}{c} \leq \lg{n}$$
$$-1 + \frac{1}{c} \leq 0$$
$$\frac{1}{c} \leq 1$$
$$c \geq 1$$

