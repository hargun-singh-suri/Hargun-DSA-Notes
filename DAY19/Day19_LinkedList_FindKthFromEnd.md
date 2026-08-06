# Day 19 — Linked List: Find Kth Node From End

**Covers:**
- **Lecture:** LL Find Kth Node From End (Interview Question)

---

## Lecture: LL Find Kth Node From End

## 1. Goal

- Find and return the **k-th node from the end** of a singly linked list.
- `k` is **1-based**:
  - `k = 1` → the last node (tail)
  - `k = 2` → second-to-last node
  - `k = list length` → the head node
  - `k <= 0` or `k > list length` → return `null`
- **Important constraint:** The linked list does **not** store its length as a usable shortcut here — we must solve this in a **single traversal** (O(n) time, O(1) space) using **two pointers**.

### Example
```
List: 1 -> 2 -> 3 -> 4 -> 5

findKthFromEnd(2) → returns node with value 4 (2nd from end)
findKthFromEnd(5) → returns node with value 1 (head, 5th from end)
findKthFromEnd(6) → returns null (list only has 5 nodes)
findKthFromEnd(0) → returns null (k must be > 0)
```

---

## 2. Why This Is Tricky

- A linked list only lets us move **forward**.
- We don't know where the "end" is until we get there — so we can't just count backward from it.
- The trick: create a **gap of `k` nodes** between two pointers, then move them together. When the front pointer hits the end, the back pointer will be exactly `k` nodes from the end.

---

## 3. The Two-Pointer Strategy

We use `slow` and `fast`, both starting at `head`.

### Step 1: Move `fast` ahead by `k` steps first
- This creates a **gap** of `k` nodes between `slow` and `fast`.
- If `fast` becomes `null` **before** finishing `k` steps → the list is shorter than `k` → return `null`.

### Step 2: Move `slow` and `fast` together
- Now move **both** pointers forward, one step at a time, until `fast` reaches the end (`null`).
- Since there's always a gap of `k` nodes between them, when `fast` hits the end, `slow` will be sitting exactly `k` nodes back from the end.

### Step 3: Return `slow`
- `slow` is now pointing to the k-th node from the end — return it.

---

## 4. Visual Walkthrough

List: `1 -> 2 -> 3 -> 4 -> 5 -> 6`, find `k = 4` (should return node `3`)

### Initial state
```
slow           fast
 |               |
 v               v
[1] -> [2] -> [3] -> [4] -> [5] -> [6] -> null
```

### Move `fast` ahead by 4 steps (creates the gap)
```
slow                                   fast
 |                                       |
 v                                       v
[1] -> [2] -> [3] -> [4] -> [5] -> [6] -> null
```

### Move both together until `fast` hits the end

**Move 1:** `slow` → 2, `fast` → 6
```
       slow                             fast
        |                                 |
        v                                 v
[1] -> [2] -> [3] -> [4] -> [5] -> [6] -> null
```

**Move 2:** `slow` → 3, `fast` → null (stop)
```
              slow
               |
               v
[1] -> [2] -> [3] -> [4] -> [5] -> [6] -> null
                                            ^
                                          fast is null, loop stops
```

### Result
- `slow` is at node `3` → the 4th node from the end. ✅

---

## 5. Pseudocode

1. If `k <= 0`, return `null` right away (invalid input).
2. Set `slow` and `fast` both to `head`.
3. Move `fast` forward `k` times:
   - If `fast` becomes `null` before finishing all `k` steps → list is too short → return `null`.
4. Move `slow` and `fast` forward together, one step at a time, until `fast` becomes `null`.
5. `slow` is now on the k-th node from the end → return it.

---

## 6. The Code

```java
public Node findKthFromEnd(int k) {
    if (k <= 0) {
        return null;
    }

    Node slow = head;
    Node fast = head;

    for (int i = 0; i < k; i++) {
        if (fast == null) {
            return null;
        }
        fast = fast.next;
    }

    while (fast != null) {
        slow = slow.next;
        fast = fast.next;
    }

    return slow;
}
```

### Line-by-line:
1. **`if (k <= 0) return null;`** — invalid `k`, nothing to find.
2. **`slow = head; fast = head;`** — both start at the same place.
3. **`for` loop** — moves `fast` ahead by `k` steps, creating the gap.
   - **`if (fast == null) return null;`** inside the loop — if `fast` runs out before finishing `k` steps, the list is shorter than `k`, so we can't find a valid k-th-from-end node.
4. **`while` loop** — moves both pointers together until `fast` reaches the end (`null`).
5. **`return slow;`** — by the time `fast` is `null`, `slow` is sitting exactly `k` nodes from the end.

---

## 7. Handling Edge Cases

| Case | What happens |
|---|---|
| `k <= 0` | Caught immediately at the top, returns `null` |
| `k > length` | Caught in the first loop — `fast` hits `null` before finishing `k` steps, returns `null` |
| `k == length` | `fast` reaches `null` right as it finishes the k steps, so the second loop never runs, and `slow` is still at `head` → correctly returns the head node |
| `k == 1` | `fast` moves 1 step ahead, then both move together until `fast` hits `null` — `slow` ends up at the last node (tail) |

---

## Quick Recap (Plain English Summary)

- **Find Kth From End** returns the node that is `k` positions from the end of the list (1-based).
- We can't count backward in a singly linked list, so instead we create a **gap of `k` nodes** between two pointers:
  1. Move `fast` ahead by `k` steps first.
  2. If `fast` runs out early → list was too short → return `null`.
  3. Then move `slow` and `fast` together until `fast` hits the end.
  4. `slow` will land exactly on the k-th node from the end.
- This is a **single-pass, O(n) time, O(1) space** solution — no need to know the list's length in advance or make two separate passes.
- Always check invalid `k` (`<= 0`) and too-large `k` (`> length`) up front — these are the main edge cases interviewers look for.
