# DSA Notes - Day 2

## Lecture 6: Big O - Drop Constants

### Rule: Drop Constants

When calculating Big O, **constant values are ignored**.

### Example

```java
for (int i = 0; i < n; i++) {
    // Operation
}

for (int i = 0; i < n; i++) {
    // Operation
}
```

Operations:

- First loop → n
- Second loop → n
- Total = 2n

Big O:

```
O(2n) → O(n)
```

Even if it is:

- O(2n)
- O(10n)
- O(1000n)

It is always simplified to:

```
O(n)
```

### Key Takeaway
> **Ignore constant numbers in Big O.**

---

# Lecture 7: O(n²) - Quadratic Time

## What is O(n²)?

When one loop runs **inside another loop**, the time complexity becomes **O(n²)**.

### Example

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.println(i + " " + j);
    }
}
```

If:

- n = 10 → 100 operations
- n = 100 → 10,000 operations

Formula:

```
n × n = n²
```

### Graph

- Grows much faster than O(n).
- Less efficient for large inputs.

### Interview Tip

If you can change an **O(n²)** solution into an **O(n)** solution, it is a **major performance improvement**.

### Key Takeaway
> **Nested loops usually result in O(n²).**

---

# Lecture 8: Drop Non-Dominant Terms

### Rule: Keep Only the Largest Term

Example:

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // Operation
    }
}

for (int i = 0; i < n; i++) {
    // Operation
}
```

Operations:

- Nested loops → n²
- Single loop → n

Total:

```
O(n² + n)
```

Simplified:

```
O(n²)
```

### Why?

As **n becomes larger**, **n² grows much faster than n**.

Example:

If n = 100

- n² = 10,000
- n = 100

The **n²** part dominates, so the **n** becomes insignificant.

### Key Takeaway
> **Keep only the dominant (largest growing) term.**

---

# Lecture 9: O(1) - Constant Time

## What is O(1)?

The number of operations **does not change**, no matter how large the input is.

### Example 1

```java
return n + n;
```

Only **one addition** is performed.

```
O(1)
```

### Example 2

```java
return n + n + n;
```

Two additions are performed.

```
O(2) → O(1)
```

### Why?

Even though there are two operations, the number of operations stays **constant** as the input size grows.

### Graph

- A flat horizontal line.
- Input size increases, but operations stay the same.

### Key Takeaway
> **O(1) is called Constant Time and is the most efficient Big O.**

---

# Quick Revision

### Simplification Rules

- **O(2n)** → **O(n)** (Drop Constants)
- **O(100n)** → **O(n)** (Drop Constants)
- **O(n² + n)** → **O(n²)** (Drop Non-Dominant Terms)

### Common Big O So Far

| Big O | Name | Performance |
|-------|------|-------------|
| O(1) | Constant Time | ⭐⭐⭐⭐⭐ Best |
| O(n) | Linear Time | ⭐⭐⭐⭐ |
| O(n²) | Quadratic Time | ⭐⭐ Slower |

---

# Interview One-Liners

- Ignore constant values when calculating Big O.
- Nested loops usually result in **O(n²)**.
- Keep only the dominant term in the final Big O.
- O(1) means the running time stays constant regardless of input size.
- O(1) is the most efficient time complexity.
