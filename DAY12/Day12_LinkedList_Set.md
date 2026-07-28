# Day 12 — Linked List: Set

**Covers:**
- **Lecture:** LL Set

---

## Lecture: LL Set

## 1. Goal

- **Set** changes the **value** of the node at a specific index.
- Returns a **boolean**: `true` if we were able to set the value, `false` if we couldn't (index out of range).

### Example
- Linked list: `[11] -> [3] -> [23] -> [7] -> null`
- We want to change the value at index `1` from `3` to `4`.

```
Before:  [11] -> [3] -> [23] -> [7] -> null
                  ^
                index 1

After:   [11] -> [4] -> [23] -> [7] -> null
                  ^
                index 1
```

---

## 2. Key Idea: Reuse the Get Method

- Set is very similar to **Get** — both need to find the node at a given index and both need to handle out-of-range indexes the same way.
- Instead of rewriting that logic, **Set just calls Get** to find the node.

```java
Node temp = get(index);
```

- `get(index)` already handles the range check internally:
  - If index is out of range → returns `null`
  - Otherwise → returns a pointer to the node at that index

So Set doesn't need to repeat the range-check code — it just needs to check whether `temp` came back as `null` or as an actual node.

---

## 3. The Logic

```java
if (temp != null) {
    temp.value = value;
    return true;
}
return false;
```

- **If `temp` is not null** (meaning Get found a valid node):
  - Update `temp.value` to the new value.
  - Return `true` (success).
- **If `temp` is null** (meaning the index was out of range):
  - Skip the update.
  - Return `false` (failure).

---

## 4. Full Method

```java
public boolean set(int index, int value) {
    Node temp = get(index);

    if (temp != null) {
        temp.value = value;
        return true;
    }
    return false;
}
```

---

## 5. Why This Code Is So Short

- Because **Get already does the hard work** (range checking + walking to the index), Set just needs to:
  1. Call Get.
  2. Check if it got a real node back.
  3. Update the value if so.
- This is a good example of **reusing existing methods** instead of rewriting the same logic twice.

---

## 6. Tested in IntelliJ

1. Created a linked list with values `11, 3, 23, 7`.
2. Printed the list → showed `11, 3, 23, 7`.
3. Called `set(1, 4)` — change the value at index `1` from `3` to `4`.
4. Printed the list again → showed `11, 4, 23, 7`.

---

## Quick Recap (Plain English Summary)

- **Set** changes the value of the node at a given index, and returns `true`/`false` depending on success.
- Instead of writing new logic to find the node, **Set reuses the Get method**.
- **Steps:**
  1. Call `get(index)` and store the result in `temp`.
  2. If `temp` is not `null` → update `temp.value`, return `true`.
  3. If `temp` is `null` (index was out of range) → return `false`.
- Good coding lesson: if you already have a method that does part of the job, **reuse it** instead of duplicating code.
