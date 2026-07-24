# Day 7 — Linked List: Remove Last

**Covers:**
- **Lecture (Part 1):** LL Remove Last — Concept/Intro
- **Lecture (Part 2):** LL Remove Last — Coding

*(Note: This method is more complex than Append, so the course splits it into two videos — one to understand the idea, one to write the actual code.)*

---

## Lecture Part 1: Remove Last — The Concept

### Goal
Remove the **last node** from the linked list, and also **return** that removed node.

### Why is this harder than Append?
- With Append, we already have `tail` pointing to the last node, so adding is quick.
- With Remove Last, we need `tail` to move **backward** to the second-last node — but a linked list only has **forward-pointing arrows** (`next`). There's no way to go backward directly.
- So the only way to find the second-last node is to **start at `head` and walk through the whole list** until we reach it.

### High-Level Steps (when list has multiple items):
1. Start at `head`.
2. Walk through the list node by node until you reach the **second-last node**.
3. Set `tail` to point to that second-last node.
4. Set `tail.next = null` (this breaks off the old last node).
5. Return the removed node.

### The Two Helper Variables: `pre` and `temp`
To find the second-last node, we use two pointers:
- `temp` → starts at `head`, moves one step at a time (`temp = temp.next`)
- `pre` → always stays **one step behind** `temp`

**How the walk works:**
- Loop keeps running **while `temp.next` is not null**.
- In each loop: `pre = temp`, then `temp = temp.next`.
- When `temp.next` finally becomes `null`, we stop — `temp` is now on the **last node**, and `pre` is on the **second-last node**.

### After the Loop:
- `tail = pre` → moves tail back to the second-last node.
- `tail.next = null` → removes the connection to the old last node.
- `return temp` → gives back the node we removed.

**Plain English:** Think of it like a treasure hunt — you can't jump straight to the second-last box, you have to walk from the start, keeping one hand on the current box and one hand on the previous box, until you reach the end.

---

## Lecture Part 2: Remove Last — The Code

Return type of this method is `Node` (technically a pointer to a node, but think of it as "returning the node").

### Case 1: Empty List
```java
if (length == 0) {
    return null;
}
```
- If there's nothing in the list, there's no node to remove — just return `null`.
- You could also check this using `head == null` or `tail == null` — any of these works to confirm the list is empty.

---

### Case 2: List Has Multiple Items (2 or more nodes)

**Step 1 — Set up two variables:**
```java
Node temp = head;
Node pre = head;
```

**Step 2 — Loop through the list:**
```java
while (temp.next != null) {
    pre = temp;
    temp = temp.next;
}
```
- This keeps moving `pre` and `temp` forward together (with `pre` always one step behind).
- Loop stops when `temp.next == null` → meaning `temp` has reached the **last node**.

**Step 3 — Fix the pointers:**
```java
tail = pre;
tail.next = null;
```
- `tail = pre` → moves tail to the second-last node.
- `tail.next = null` → breaks the last node off from the list.

**Step 4 — Update length:**
```java
length--;
```

**Step 5 — Return the removed node:**
```java
return temp;
```

---

### Case 3: Edge Case — Only ONE Item in the List

This is tricky, so let's walk through why:

- Since list has 1 node, both `head` and `tail` point to that same node.
- `temp = head` and `pre = head` → both also point to that same node.

Now let's check what happens to each line of code:

| Code | What actually happens | Result |
|---|---|---|
| `while (temp.next != null)` | `temp.next` is already `null` (only one node) | Loop never runs |
| `tail = pre;` | `tail` and `pre` already point to the same node | No real change |
| `tail.next = null;` | Already `null` | No real change |
| `length--;` | Length goes from `1` to `0` | **This is where the actual problem starts** |

### The Problem:
After `length--`, length becomes `0` — but `head` and `tail` are **still pointing to the (now removed) node**. That's incorrect. A list with length `0` should have `head` and `tail` both set to `null`.

### The Fix:
```java
if (length == 0) {
    head = null;
    tail = null;
}
```

**Important distinction:**
- The **first check** (`if length == 0` at the very top) catches an **already-empty list** before we do anything.
- This **second check** (`if length == 0` after `length--`) catches the case where the list **just became empty** because we removed its only node.
- Same condition, but used at two different points for two different reasons.

---

## Testing in IntelliJ (What Was Verified)

1. Created a linked list with 2 nodes: values `1` and `2`.
2. Called `removeLast()` three times in a row and printed the result each time:
   - **1st call:** List had 2 items → removed node with value `2`. List now has `[1]`.
   - **2nd call:** List had 1 item → removed node with value `1`. List now empty `[]`.
   - **3rd call:** List was empty → returned `null`.

### Small but Important Gotcha:
- When printing the result, you can do `result.value` to see just the value — but **only if a node was actually returned**.
- On the 3rd call, `removeLast()` returns `null`. Trying to do `null.value` causes a **NullPointerException** (a common Java error when you try to access something on a `null` object).
- Lesson: always check if something is `null` before trying to access its properties.

---

## Quick Recap (Plain English Summary)

- **Remove Last** removes the last node and gives it back to you.
- Since linked lists only point forward, you can't jump straight to the last node — you must **walk from head** using two pointers (`pre` one step behind `temp`).
- **3 cases to handle:**
  1. **Empty list** → return `null` immediately.
  2. **Multiple items** → walk to find second-last node, update `tail`, cut off the last node, return it.
  3. **One item only** → after removing, list becomes empty, so you must manually set `head = null` and `tail = null`.
- Watch out for `NullPointerException` — don't call `.value` on something that might be `null`.
