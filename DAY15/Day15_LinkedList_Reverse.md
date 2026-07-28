# Day 15 — Linked List: Reverse

**Covers:**
- **Lecture:** LL Reverse

---

## Lecture: LL Reverse

## 1. Goal

- **Reverse** the entire linked list — **in place** (no new list is created, we just flip the existing arrows around).
- Return type is `void` — nothing is returned, the original list itself gets reversed.

### Example
```
Before:  head                              tail
          |                                  |
          v                                  v
         [1] -> [2] -> [3] -> [4] -> null

After:   head                              tail
          |                                  |
          v                                  v
         [4] -> [3] -> [2] -> [1] -> null
```

---

## 2. Step 1: Swap `head` and `tail`

- Since we're reversing the list, whatever was the last node (`tail`) becomes the first node (new `head`), and vice versa.

```java
Node temp = head;
head = tail;
tail = temp;
```

- `temp = head` → save the old head so we don't lose it.
- `head = tail` → head now points to what used to be the last node.
- `tail = temp` → tail now points to what used to be the first node.

**Why do we need `temp` here?** Same reason as always with swapping — if we did `head = tail` first, we'd lose the original `head` before we could save it into `tail`.

---

## 3. Step 2: Set Up Three Helper Pointers

To flip every arrow in the middle of the list, we need **three pointers** moving together:

| Pointer | Purpose |
|---|---|
| `before` | The node before `temp` (starts at `null`, since there's nothing before the first node) |
| `temp` | The current node we're flipping the arrow for |
| `after` | The node after `temp` (so we don't lose our place once we flip `temp`'s arrow backward) |

```java
Node after = temp.next;
Node before = null;
```

- Wait — remember `temp` was already reassigned in Step 1 (it was pointing to the *old* head). So at this point, `temp` still points to the very first node of the original list — that's exactly where we want to start flipping from.

---

## 4. Step 3: The For Loop — Flipping Each Arrow

This is the tricky part. Inside the loop, we need **4 lines in this exact order**, or the list breaks.

```java
for (int i = 0; i < length; i++) {
    after = temp.next;
    temp.next = before;
    before = temp;
    temp = after;
}
```

### Why the order matters:

1. **`after = temp.next`** — FIRST, save where `temp` currently points (before we destroy that pointer in the next line). This is our "bridge" across the gap that's about to form.
2. **`temp.next = before`** — NOW flip the arrow: `temp` now points backward to `before` instead of forward.
3. **`before = temp`** — Move `before` forward to catch up to `temp`.
4. **`temp = after`** — Jump `temp` across the gap to the node we saved in step 1.

**If you did `temp.next = before` before saving `after`, you would lose the rest of the list forever** — there'd be no way to reach the remaining nodes.

### Visual: One iteration of the loop

```
Before this iteration:
before        temp         (rest of list)
  |            |
  v            v
 null         [1] -> [2] -> [3] -> [4] -> null

Step 1: after = temp.next
                after
                 |
                 v
 null         [1] -> [2] -> [3] -> [4] -> null

Step 2: temp.next = before
 null <- [1]    [2] -> [3] -> [4] -> null
          ^
        (arrow flipped)

Step 3: before = temp
       before
         |
         v
 null <- [1]    [2] -> [3] -> [4] -> null

Step 4: temp = after
                temp
                 |
                 v
 null <- [1]    [2] -> [3] -> [4] -> null
```

- The loop repeats this same 4-step process for every node, walking `before` and `temp` forward together until the whole list is flipped.

### Last iteration (important edge case):
- On the final loop, `temp.next` is already `null` (temp is on the old last node).
- So `after = temp.next` sets `after` to `null`.
- `temp.next = before` flips the last arrow.
- `temp = after` sets `temp` to `null`, which naturally ends things (loop finishes since it's based on `length`, not on checking `null`).

---

## 5. Full Method

```java
public void reverse() {
    Node temp = head;
    head = tail;
    tail = temp;

    Node after = temp.next;
    Node before = null;

    for (int i = 0; i < length; i++) {
        after = temp.next;
        temp.next = before;
        before = temp;
        temp = after;
    }
}
```

---

## 6. Example Walkthrough

- Start: Linked list `[1, 2, 3, 4]`
- Call `reverse()`
- `head`/`tail` swap first (head now "points at" old tail conceptually, gets fixed properly as loop runs)
- Loop flips each arrow one at a time, walking from the old first node to the old last node
- Result: `[4, 3, 2, 1]`

---

## 7. Tested in IntelliJ

1. Created a linked list with values `1, 2, 3, 4`.
2. Printed the list → showed `1, 2, 3, 4`.
3. Called `reverse()`.
4. Printed the list again → showed `4, 3, 2, 1`.

---

## Quick Recap (Plain English Summary)

- **Reverse** flips the linked list **in place** — no new list is made, the arrows just get turned around.
- **Step 1:** Swap `head` and `tail` (using a `temp` variable so nothing gets lost).
- **Step 2:** Set up `before` (starts at `null`) and `after` (starts one step ahead of `temp`).
- **Step 3:** Loop through the list, and in each pass do these 4 steps **in this exact order**:
  1. Save `after = temp.next` (bridge to the rest of the list).
  2. Flip the arrow: `temp.next = before`.
  3. Move `before` forward to `temp`.
  4. Jump `temp` forward to `after`.
- **The order is critical** — if you flip the arrow before saving `after`, you permanently lose access to the rest of the list.
