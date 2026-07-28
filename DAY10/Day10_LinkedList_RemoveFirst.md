# Day 10 — Linked List: Remove First

**Covers:**
- **Lecture:** LL Remove First

---

## Lecture: LL Remove First

## 1. Goal

- Remove the **first node** from the linked list, and **return** that removed node.
- `head` moves forward to point to the new first node.

### Before Remove First
```
head                          tail
 |                              |
 v                              v
[11] -> [3] -> null
```

### After Remove First
```
              head           tail
               |               |
               v               v
[11]  ->  [3] -> null
(removed)
```

---

## 2. Why This Is Similar to Remove Last

- Just like Remove Last, there are **edge cases** to handle:
  1. List is **empty** — nothing to remove.
  2. List has **only one item** — after removing, list becomes empty.
  3. List has **multiple items** — the normal case.

---

## 3. Case 1: Empty List

```java
if (length == 0) {
    return null;
}
```
- Same idea as `head == null` — if there's nothing in the list, just return `null`.

---

## 4. Case 2: Multiple Items

### The idea:
1. Save a pointer to the current first node (so we can return it later).
2. Move `head` forward to the next node.
3. Disconnect the old first node from the list.
4. Decrease `length` by 1.
5. Return the removed node.

### The Code:
```java
Node temp = head;
head = head.next;
temp.next = null;
length--;
return temp;
```

### Step-by-step:
- `temp = head` → `temp` now points to the node we're about to remove (the old first node).
- `head = head.next` → `head` moves forward to point to the second node.
- `temp.next = null` → cuts the old first node off from the rest of the list (cleans it up).
- `length--` → one less node in the list.
- `return temp` → gives back the removed node.

```
Step 1: temp = head
temp
 |
 v
[11] -> [3] -> null
 ^
head

Step 2: head = head.next
temp
 |
 v
[11]    [3] -> null
         ^
        head

Step 3: temp.next = null
temp
 |
 v
[11] -> null      [3] -> null
                   ^
                  head
```

---

## 5. Case 3: Edge Case — Only ONE Item in the List

Let's trace through what happens when there's just **one node**:

| Code | What actually happens | Result |
|---|---|---|
| `temp = head` | `temp` points to the only node | fine |
| `head = head.next` | `head.next` is `null` (only one node) → `head` becomes `null` | `head` is now `null` |
| `temp.next = null` | `temp.next` was already `null` | No real change |
| `length--` | Length goes from `1` to `0` | **This is where the problem starts** |

### The Problem:
- After `length--`, length is `0`.
- But `tail` is **still pointing to the removed node**.
- A list with length `0` should have both `head` and `tail` set to `null` — but only `head` got fixed automatically (because we moved it). `tail` didn't.

### The Fix:
```java
if (length == 0) {
    tail = null;
}
```

**Important distinction (same pattern as Remove Last):**
- The **first check** (`if length == 0` at the top) catches an **already-empty list** before doing anything.
- This **second check** (`if length == 0` after `length--`) catches the case where the list **just became empty** because we removed its only node — here we clean up `tail`.

---

## 6. Full Method

```java
public Node removeFirst() {
    if (length == 0) {
        return null;
    }

    Node temp = head;
    head = head.next;
    temp.next = null;
    length--;

    if (length == 0) {
        tail = null;
    }

    return temp;
}
```

---

## 7. Tested in IntelliJ

1. Created a linked list with values `2` and `1`.
2. Called `removeFirst()` three times in a row, printing `.value` each time:
   - **1st call:** List had 2 items → removed node with value `2`. List now has `[1]`.
   - **2nd call:** List had 1 item → removed node with value `1`. List now empty `[]`.
   - **3rd call:** List was empty → returned `null`.

### Gotcha to remember:
- On the 3rd call, `removeFirst()` returns `null`.
- Trying to do `null.value` would cause a **NullPointerException**.
- Always check if the result is `null` before accessing `.value`.

---

## Quick Recap (Plain English Summary)

- **Remove First** removes the first node and gives it back to you.
- **3 cases to handle:**
  1. **Empty list** → return `null` immediately.
  2. **Multiple items** → save the first node in `temp`, move `head` forward, disconnect the old node, decrease length, return it.
  3. **One item only** → after removing, list becomes empty, so you must manually set `tail = null` (head already got set to `null` naturally through `head = head.next`).
- Watch out for `NullPointerException` — don't call `.value` on something that might be `null`.
