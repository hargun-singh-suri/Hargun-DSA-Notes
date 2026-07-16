# DSA Notes - Day 4

## Lecture 10: O(log n) - Logarithmic Time

### What is O(log n)?

- O(log n) reduces the problem size by **half in every step**.
- It is very efficient for **large datasets**.
- Usually requires the data to be **sorted**.

### Example (Binary Search)

Array:

```text
[1, 2, 3, 4, 5, 6, 7, 8]
```

Find **1**:

1. Check the middle.
2. Ignore half of the array.
3. Check the middle of the remaining half.
4. Repeat until the item is found.

Instead of checking every element, we keep **dividing the search space by 2**.

### Why is it O(log n)?

For 8 elements:

```
8 → 4 → 2 → 1
```

Only **3 steps** are needed.

For over **1 billion** elements:

- Only about **31 steps** are needed.

### Key Takeaway

> **O(log n) repeatedly divides the problem in half, making it one of the most efficient time complexities.**

---

# Lecture 11: Different Terms for Different Inputs

### Rule

When a method has **multiple independent inputs**, use **different variables** for each.

### Example 1

```java
for (int i = 0; i < a; i++) {
    // Operation
}

for (int j = 0; j < b; j++) {
    // Operation
}
```

Time Complexity:

```
O(a + b)
```

**Not**

```
O(n)
```

because **a** and **b** can be different sizes.

---

### Example 2

```java
for (int i = 0; i < a; i++) {
    for (int j = 0; j < b; j++) {
        // Operation
    }
}
```

Time Complexity:

```
O(a × b)
```

### Interview Tip

Never assume different inputs are the same variable.

### Key Takeaway

> **Different inputs must use different variables in Big O.**

---

# Lecture 12: Big O of ArrayList

## Add at the End

```java
list.add(value);
```

- Item is added at the end.
- No shifting is required.

**Time Complexity**

```
O(1)
```

---

## Remove from the End

```java
list.remove(lastIndex);
```

- Remove the last element.
- No shifting is required.

**Time Complexity**

```
O(1)
```

---

## Add at the Beginning

```java
list.add(0, value);
```

- Every element must shift one position.

**Time Complexity**

```
O(n)
```

---

## Remove from the Beginning

```java
list.remove(0);
```

- Every remaining element shifts left.

**Time Complexity**

```
O(n)
```

---

## Add or Remove in the Middle

```java
list.add(index, value);
list.remove(index);
```

- Elements after the index must shift.

**Time Complexity**

```
O(n)
```

---

## Search by Value

```java
list.contains(value);
```

or

```java
list.indexOf(value);
```

- Search starts from the beginning.
- May need to check every element.

**Time Complexity**

```
O(n)
```

---

## Access by Index

```java
list.get(index);
```

Example:

```java
list.get(3);
```

- Directly accesses the required position.

**Time Complexity**

```
O(1)
```

### Key Takeaway

| Operation | Big O |
|-----------|-------|
| Add at End | O(1) |
| Remove at End | O(1) |
| Add at Beginning | O(n) |
| Remove at Beginning | O(n) |
| Insert in Middle | O(n) |
| Remove from Middle | O(n) |
| Search by Value | O(n) |
| Access by Index | O(1) |

---

# Lecture 13: Big O Wrap Up

## Comparison

| Big O | Name | Performance |
|-------|------|-------------|
| O(1) | Constant Time | ⭐⭐⭐⭐⭐ Best |
| O(log n) | Logarithmic Time | ⭐⭐⭐⭐ |
| O(n) | Linear Time | ⭐⭐⭐ |
| O(n²) | Quadratic Time | ⭐ Worst |

---

## Memory Keywords

| Big O | Remember As |
|-------|-------------|
| O(1) | Constant Time |
| O(log n) | Divide & Conquer |
| O(n) | Linear Growth |
| O(n²) | Nested Loops |

---

## Performance Example

For **n = 100**

| Big O | Operations |
|-------|------------|
| O(1) | 1 |
| O(log n) | ~7 |
| O(n) | 100 |
| O(n²) | 10,000 |

---

For **n = 1000**

| Big O | Operations |
|-------|------------|
| O(1) | 1 |
| O(log n) | ~10 |
| O(n) | 1,000 |
| O(n²) | 1,000,000 |

Notice how **O(n²)** grows much faster than the others.

---

# Quick Revision

### Big O Learned So Far

| Big O | Meaning |
|-------|---------|
| O(1) | Constant Time |
| O(log n) | Divide the problem by half each step |
| O(n) | Linear growth |
| O(n²) | Nested loops |

---

### Big O Simplification Rules

- **Drop Constants**
  - `O(2n)` → `O(n)`

- **Drop Non-Dominant Terms**
  - `O(n² + n)` → `O(n²)`

- **Different Inputs**
  - Sequential loops → `O(a + b)`
  - Nested loops → `O(a × b)`

---

# Interview One-Liners

- O(log n) works by repeatedly dividing the problem in half.
- Binary Search is a classic example of O(log n).
- Different inputs use different variables in Big O.
- Accessing an ArrayList by index is O(1).
- Searching an ArrayList by value is O(n).
- Adding or removing at the beginning of an ArrayList is O(n) because elements must shift.
- O(1) is the most efficient time complexity, while O(n²) is much less efficient for large inputs.
