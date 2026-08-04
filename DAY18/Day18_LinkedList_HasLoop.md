# Day 18 — Linked List: Has Loop

**Covers:**
- **Lecture:** LL Has Loop (Coding Exercise)

---

## Lecture: LL Has Loop

## 1. Goal

- Check whether a linked list has a **loop** (a node whose `next` eventually points back to an earlier node, instead of ending at `null`).
- Return a **boolean**: `true` if there's a loop, `false` if there isn't.

### Note on this exercise
- This is a **coding/interview exercise** — no starter code is given, just the strategy. The idea is that after learning linked lists in detail, you should be able to write the code yourself using the strategy.

---

## 2. The Strategy: Slow and Fast Pointers

- We use **two pointers**: `slow` and `fast`, both starting at `head`.
- Each loop iteration:
  - `slow` moves **1 step** forward.
  - `fast` moves **2 steps** forward.
- After moving both, we check: **are `slow` and `fast` pointing to the same node?**
  - If yes → there's a loop → return `true`.
  - If `fast` reaches the end of the list (`null`) without ever matching `slow` → no loop → return `false`.

**Why does this work?** Think of two runners on a track — one running twice as fast as the other. If the track is a straight line (no loop), the fast runner just finishes first and there's no loop. But if the track is a **circle** (a loop), the faster runner will eventually **lap** the slower one and they'll meet at the same spot.

---

## 3. Case 1: No Loop

```
[1] -> [2] -> [3] -> [4] -> null
```

- `fast` moves 2 steps, `slow` moves 1 step, each round.
- Eventually `fast` reaches the last node or goes past the end (`null`).
- Since `slow` and `fast` are never equal, we return `false`.

### Even number of nodes example
- Fast pointer reaching `null` (or `fast.next` being `null`) is what breaks us out of the loop.
- No loop was found → return `false`.

---

## 4. Case 2: Has a Loop

```
[1] -> [2] -> [3] -> [4]
        ^              |
        |______________|
```

- Here, the last node's `next` points back into the middle of the list instead of to `null`.
- As `slow` and `fast` keep moving, `fast` (moving twice as fast) will eventually **catch up to and land on the same node** as `slow`.
- When `slow == fast`, we know there's a loop → return `true`.

---

## 5. Pseudocode

1. Set `slow` and `fast` to both point at `head`.
2. Loop **while `fast` is not null AND `fast.next` is not null**:
   1. Move `slow` forward one step (`slow = slow.next`).
   2. Move `fast` forward two steps (`fast = fast.next.next`).
   3. Check if `slow == fast`. If so, return `true` (loop found).
3. If the loop ends without finding a match, return `false` (no loop).

This is known as **Floyd's Tortoise and Hare algorithm**.

---

## 6. The Code

```java
public boolean hasLoop() {
    Node slow = head;
    Node fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) {
            return true;
        }
    }

    return false;
}
```

---

## 7. Why Both `fast != null` and `fast.next != null` Are Needed

- Both checks exist to avoid a **NullPointerException**.
- `fast != null` → checks if `fast` has already reached the end of the list.
- `fast.next != null` → since `fast` moves **two** nodes at a time (`fast.next.next`), we need to make sure there's actually a next node before trying to jump two steps ahead. Without this check, if `fast` were on the last node, `fast.next` would be `null`, and trying to do `null.next` would crash the program.

---

## Quick Recap (Plain English Summary)

- **Has Loop** checks if a linked list loops back on itself instead of ending in `null`.
- Uses the **slow and fast pointer technique** (Floyd's Tortoise and Hare):
  - `slow` moves 1 step at a time.
  - `fast` moves 2 steps at a time.
- After each move, check if `slow` and `fast` point to the **same node** → if so, there's a loop, return `true`.
- If `fast` reaches the end of the list (`null`) without ever meeting `slow` → no loop, return `false`.
- Always check **both** `fast != null` and `fast.next != null` in the while condition to avoid crashing with a NullPointerException.
