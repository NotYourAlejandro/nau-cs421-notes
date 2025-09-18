# Reading 4 - Recursion Tree Method

## 4.1 - The maximum-subarray problem

### Tasks

- _Know the runtime of the brute-force solution and why it is what it is_
- _Understand the rephrased problem after the "transformation" described in the book_
- _Understand the solution using D&C, specifically the crucial fine_max_crossing_subarray() function_
- _Have an idea how equation 4.7 came to be_

### Brute Force

- **A Brute Force Solution**: try every input possible one by one in the hopes you get lucky.
    - **Runtime**: $\theta(n^2)$

### A Transformation

**maximum subarray**: a range of an array that produces the highest sum
    - _Example_: 
        In the array `[-3, -16, -23, 18, 20, -7, 12, -5, -22]`,
        `[-23, 18, 20, -7, 12]` adds up to 43, so this range is the **max subarray**
    - Flaws:
        - If all array numbers are positive, then the whole array is _ALWAYS_ the **max subarray**.

Getting the **maximum subarray** of your array is considered to be a **transformation**.

### A solution using divide-and-conquer

Our goal is to split the array into two subarrays. To do that, we need to define:

- `low`
- `medium`
- `high`

For example, we can do:

```python
master_array = [-3, -16, -23, 18, 20, -7, 12, -5, -22]
subarr_1 = master_array[0:len(master_array/2)]
subarr_2 = master_array[(len(master_array/2) + 1):len(master_array)]
```

### Understanding how equation 4.7 came to be

**Find-Max-Subarray**:

```
Find-Maximum-Subarray(A, low, high)

if high == low
    return (low, high, A[low])

else
    mid = floor((low + high) / 2)
    (left-low, left-high, left-sum) = Find-Maximum-Subarray(A, low, mid)
    (right-low, right-high, right-sum) = Find-Maximum-Subarray(A, mid + 1, high)
    (cross-low, cross-high, cross-sum) = Find-Maximum-Subarray(A, low, mid, high)       // why 4 args here?
    
    if left-sum >= right-sum && right-sum >= cross-sum
        return (left-low, left-high, left-sum)
    else if right-sum >= left-sum && right-sum >= cross-sum
        return (right-low, right-high, right-sum)
    else
        return (cross-low, cross-high, cross-sum)
```

Let's look at the base case first:

```
if high == low
    return (low, high, A[low])
```

This is our best-case scenario when $n = 1$, which runs in constant time: $T(1) = \theta(1)$

We can sum up the runtimes of rest of the algorithm:
- `mid = floor((low + high) / 2)`: $\theta(1)$
- `(left-low, left-high, left-sum) = Find-Maximum-Subarray(A, low, mid)`: $2\theta(\frac{n}{2})$
- `(right-low, right-high, right-sum) = Find-Maximum-Subarray(A, mid + 1, high)`: $2\theta(\frac{n}{2})$
- `(cross-low, cross-high, cross-sum) = Find-Maximum-Subarray(A, low, mid, high)`: $\theta(n)$

And the final if-paths are all $\theta(1)$:

```
if left-sum >= right-sum && right-sum >= cross-sum
    return (left-low, left-high, left-sum)
else if right-sum >= left-sum && right-sum >= cross-sum
    return (right-low, right-high, right-sum)
else
    return (cross-low, cross-high, cross-sum)
```

Then we add everything together:

$$
\theta(1) + 2\theta(\frac{n}{2}) + \theta(n) + \theta(1)
2\theta(\frac{n}{2}) + \theta(n)
$$

**Equation 4.7**:

$$
T(n) = \begin{cases}
\theta(1)           & \text{if } n = 1,\\
2T(n/2)+\theta(n)   & \text{if } n > 1.
\end{cases}
$$

## 4.4 - The recursion-tree method for solving recurrences

### Tasks

- _Know how to expand the recurrence_
- _Know how to figure the costs per level ("breadth")_
- _Know how many levels there are ("depth")_

### Expanding Recurrence

**recursion trees**: A tree that visualizes the runtime of a recursion, where nodes at each tree level describe the runtime at that level

At each level of a **recursion tree**, we can sum up all the runtimes at a level, which can then all be summed up to get the **total runtime** of the recurrence.

Within these trees, the lowest level is always $T(n)$, while the rest is the highest-degree polynomial.

### Determining costs per level ("breadth")

Take the node $cn^2$ at level 2, assuming $n % 4 = 0$. When the tree expands, $n$ will expand: $c(\frac{n}{4})^2$.

If the tree has 3 branches per level, we can multiply the node by 3 and simplify:

$$
3c(\frac{n}{4})^2
3c(\frac{n^2}{4^4})
\frac{3}{16}cn^2
$$

By the same method, the sum at tier 3 is $(\frac{3}{16})^2)cn^2$.

### Determining number of levels ("depth")

We've determined the following sums of levels 1-3:
- Level 1: $cn^2$
- Level 2: $\frac{3}{16}cn^2$
- Level 3: $(\frac{3}{16})^2)cn^2$

We can identify a pattern here: $(\frac{3}{16})^k)cn^2$

We can then solve for $i$

