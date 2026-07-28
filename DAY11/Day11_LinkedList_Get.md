# Day 11 — Linked List: Get

**Covers:**
- **Lecture:** LL Get

---

## Lecture: LL Get

## 1. Goal

- **Get** a node at a specific **index**, without removing it from the list.
- Just like an array, indexes start at `0`.

### Example
- Linked list: `[0] -> [1] -> [2] -> [3] -> null`
- Valid indexes: `0, 1, 2, 3`
- Invalid indexes: `-1` (too low), `4` (too high, since length is 4)

```
index:    0     1     2     3
         [0] -> [1] -> [2] -> [3] -> null
```

---

## 2. Step 1: Check if Index is Out of Range

- We can't get a node at an index that's **less than 0** or **greater than/equal to the length**.

```java
if (index < 0 || index >= length) {
    return null;
}
```

**Why this matters:** This is the part people most often forget. Without this check, trying to reach an invalid index would cause errors (like trying to walk past the end of the list).

---

## 3. Step 2: Walk to the Index

- Since a linked list has **no direct indexing** (unlike arrays), we must **start at `head`** and move forward one step at a time until we reach the index we want.

### Setting up the pointer:
```java
Node temp = head;
```
- We don't need `head` or `tail` for the rest of this method — only `temp` matters here.

### Using a for loop to move forward:
```java
for (int i = 0; i < index; i++) {
    temp = temp.next;
}
```
- This loop runs **`index` number of times**.
- Example: if `index = 2`, the loop runs twice, moving `temp` forward two steps.

```
Start:  temp
         |
         v
        [0] -> [1] -> [2] -> [3] -> null

After loop runs twice (looking for index 2):

                      temp
                       |
                       v
        [0] -> [1] -> [2] -> [3] -> null
```

---

## 4. Step 3: Return the Node

```java
return temp;
```
- After the loop finishes, `temp` is sitting on the exact node we wanted — just return it.

---

## 5. Full Method

```java
public Node get(int index) {
    if (index < 0 || index >= length) {
        return null;
    }

    Node temp = head;

    for (int i = 0; i < index; i++) {
        temp = temp.next;
    }

    return temp;
}
```

---

## 6. Important: Get Does NOT Remove

- **Get** only **reads/returns** the node — the linked list stays exactly the same afterward.
- This is different from a method like `remove(index)` (covered later), which would **remove and return** the node at that index.

---

## 7. Tested in IntelliJ

1. Created a linked list with values `0, 1, 2, 3` (values match their indexes, for easy testing).
2. Printed the list → showed `0, 1, 2, 3`.
3. Called `get(2)`.
4. Printed the list again → still `0, 1, 2, 3` (nothing removed).
5. Printed `.value` of the returned node → showed `2`, confirming the correct node was returned.

---

## Quick Recap (Plain English Summary)

- **Get** returns the node at a given index, without changing the list.
- **Step 1:** Check if the index is out of range (`< 0` or `>= length`) → if so, return `null`.
- **Step 2:** Start a pointer (`temp`) at `head`, then walk it forward using a for loop until it reaches the target index.
- **Step 3:** Return `temp`.
- Since linked lists have no direct indexing (unlike arrays), we always have to **walk from the start** to reach a specific index — this is why Get is O(n), not O(1).
