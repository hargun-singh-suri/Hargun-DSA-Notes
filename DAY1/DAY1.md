# DSA Notes - Day 1

## Lecture 3: Introduction to Big O

### What is Big O?
- Big O is used to compare the **efficiency of two algorithms**.
- Two programs may produce the same result, but one may be faster or use less memory.

### Types of Complexity

#### 1. Time Complexity
- Measures the **number of operations** an algorithm performs.
- It is **not measured in seconds** because computer speeds differ.

#### 2. Space Complexity
- Measures **how much memory** an algorithm uses.
- Sometimes we use more memory to make the program run faster.

### Interview Tip
- Most interview questions focus on **Time Complexity**.
- You may also be asked how to optimize **Space Complexity**.

### Key Takeaway
> **Big O is a mathematical way to measure the efficiency of an algorithm.**

---

# Lecture 4: Best, Average & Worst Case

## Three Cases

| Symbol | Meaning |
|---------|---------|
| Ω (Omega) | Best Case |
| Θ (Theta) | Average Case |
| O (Big O) | Worst Case |

### Example

Array:

```text
[1, 2, 3, 4, 5, 6, 7]
```

- Search **1** → Best Case (Ω)
- Search **4** → Average Case (Θ)
- Search **7** → Worst Case (O)

### Interview Tip
- **Big O always represents the Worst Case.**
- Technically:
  - Ω = Best Case
  - Θ = Average Case
  - O = Worst Case

### Key Takeaway
> **Big O = Worst Case Time Complexity.**

---

# Lecture 5: O(n) - Linear Time

## What is O(n)?

- The number of operations grows **directly with the input size (n)**.
- This is called **Linear Time Complexity**.

### Example

```java
for (int i = 0; i < n; i++) {
    System.out.println(i);
}
```

If:

- n = 10 → Loop runs 10 times
- n = 100 → Loop runs 100 times

### Why is it O(n)?

- 1 input item → 1 operation
- 10 input items → 10 operations
- 100 input items → 100 operations

Operations increase **proportionally** with the input size.

### Graph

- Straight line.
- As **n increases**, the **number of operations increases at the same rate**.

### Key Takeaway
> **O(n) means if the input doubles, the work also doubles.**

---

# Quick Revision

- **Big O** → Measures algorithm efficiency.
- **Time Complexity** → Number of operations.
- **Space Complexity** → Memory used.
- **Ω (Omega)** → Best Case.
- **Θ (Theta)** → Average Case.
- **O (Big O)** → Worst Case.
- **O(n)** → Linear Time (operations grow with input size).

---

# Interview One-Liners

- Big O compares the efficiency of algorithms.
- Time Complexity measures operations, not execution time.
- Space Complexity measures memory usage.
- Big O represents the **Worst Case**.
- O(n) means the running time grows linearly with the input size.
