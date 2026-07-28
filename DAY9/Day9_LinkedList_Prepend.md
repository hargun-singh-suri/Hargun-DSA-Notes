# Day 9 — Linked List: Prepend

**Covers:**
- **Lecture:** LL Prepend

---

## Lecture: LL Prepend

## 1. Goal

- **Prepend** = add a new node to the **beginning** of the linked list (opposite of Append, which adds to the end).
- Return type is `void` — we just add the node, we don't return anything.

---

## 2. The Core Idea

- Normally, `head` points to the first node.
- To prepend, we:
  1. Create a new node.
  2. Make the **new node point to the old first node** (so it hooks into the list).
  3. Make **`head` point to the new node** instead (so it becomes the new first node).

### Before Prepend
```
head                          tail
 |                              |
 v                              v
[11] -> null
```

### Step 1: New node created, pointing to old head
```
                 head                tail
                  |                    |
                  v                    v
[new] -> [11] -> null
  ^
  |
(new node points to 11, but head still points to 11)
```

### After Prepend (head moved to new node)
```
head                                  tail
 |                                     |
 v                                     v
[new] -> [11] -> null
```

---

## 3. Two Cases to Handle

Just like Append, we need to check: **is the list empty or not?**

| Case | What happens |
|---|---|
| List is **empty** (`length == 0` or `head == null`) | `head` and `tail` both point to the new node |
| List has **items** | `newNode.next = head` (new node points to old first node), then `head = newNode` (head moves to new node) |

### Why check for empty list separately?
- If the list is empty, there is no existing `head` to link to — so `newNode.next = head` would just point to `null`, which isn't useful.
- In that case, we simply set both `head` and `tail` to the new node directly.

---

## 4. The Code

```java
public void prepend(int value) {
    Node newNode = new Node(value);

    if (length == 0) {
        head = newNode;
        tail = newNode;
    } else {
        newNode.next = head;
        head = newNode;
    }

    length++;
}
```

### Step-by-step breakdown:
1. **Create the node** — `Node newNode = new Node(value);`
2. **Check if list is empty** — `if (length == 0)` (same as checking `head == null`)
   - If empty → `head = newNode` and `tail = newNode` (both point to the new node)
   - Else → `newNode.next = head` (hook new node to old first node), then `head = newNode` (move head to new node)
3. **Increase length by 1**

---

## 5. Example Walkthrough

- Start: Linked list has `[2, 3]`
- Call `prepend(1)`
- New node created with value `1`
- Since list is **not empty** → `newNode.next = head` (1 now points to 2), then `head = newNode` (head now points to 1)
- Result: Linked list is `[1, 2, 3]`

```
Before: head -> [2] -> [3] -> null

prepend(1):

  [1] -> [2] -> [3] -> null
   ^
  head (moved here)
```

---

## 6. Tested in IntelliJ

1. Created a linked list with values `2` and `3`.
2. Printed the list → showed `2, 3`.
3. Called `prepend(1)`.
4. Printed the list again → showed `1, 2, 3`.

---

## Quick Recap (Plain English Summary)

- **Prepend** adds a new node to the **front** of the linked list.
- Return type is `void` — nothing is returned.
- **Two cases:**
  1. **Empty list** → `head` and `tail` both point to the new node.
  2. **List has items** → new node points to the old first node (`newNode.next = head`), then `head` moves to the new node.
- Don't forget to **increase `length` by 1** at the end.
- Same reference/pointer logic as Append — just working on the **front** of the list instead of the back.
