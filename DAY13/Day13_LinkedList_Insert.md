# Day 13 — Linked List: Insert

**Covers:**
- **Lecture:** LL Insert

---

## Lecture: LL Insert

## 1. Goal

- **Insert** a new node with a given value at a given **index**.
- Returns a **boolean**: `true` if inserted successfully, `false` if the index was out of range.

---

## 2. Four Situations to Handle

| Situation | What we do |
|---|---|
| Index is out of range (`< 0` or `> length`) | Return `false` |
| Index is `0` (insert at the very front) | Just call `prepend()` — already built! |
| Index equals `length` (insert at the very end) | Just call `append()` — already built! |
| Index is somewhere in the middle | Need new logic (see below) |

**Key idea:** We already built `prepend()` and `append()` earlier — no need to rewrite that logic. Insert just **reuses** them for the front and back cases.

---

## 3. Case 1: Out of Range

```java
if (index < 0 || index > length) {
    return false;
}
```
- Note: unlike Get/Set (which used `>= length`), Insert allows `index == length` — because inserting exactly at the end is a valid case (it just means "append").

---

## 4. Case 2: Insert at Index 0 (Front)

```java
if (index == 0) {
    prepend(value);
    return true;
}
```
- Inserting at the front is exactly what `prepend()` already does.

---

## 5. Case 3: Insert at Index == Length (End)

```java
if (index == length) {
    append(value);
    return true;
}
```
- Inserting at the very end is exactly what `append()` already does.

---

## 6. Case 4: Insert in the Middle

This is the new logic we need to write.

### The Problem
- Linked lists only have **forward-pointing arrows**.
- To insert a new node in the middle, we need to **redirect an arrow** so it points to our new node.
- But we can't point an arrow backward — so we need a pointer to the node **just before** where we're inserting.

### Example: Insert value at index 2
```
Before:
[A] -> [B] -> [C] -> [D] -> null
        (insert new node here, at index 2)

We need "temp" to point to the node BEFORE index 2 (i.e. node at index 1):
[A] -> [B] -> [C] -> [D] -> null
        ^
       temp (index 1, one before insert point)
```

### Step 1: Create the new node
```java
Node newNode = new Node(value);
```

### Step 2: Find the node just BEFORE the insert index
```java
Node temp = get(index - 1);
```
- Again, we **reuse** the `get()` method instead of writing new walking logic.
- `get(index - 1)` gives us the node right before where we want to insert.

### Step 3: Rewire the pointers

```java
newNode.next = temp.next;
temp.next = newNode;
```

- `newNode.next = temp.next` → new node now points to whatever `temp` was pointing to (the node that comes after the insert point).
- `temp.next = newNode` → `temp` now points to the new node instead, hooking it into the list.

**Order matters here!** We must set `newNode.next` first — otherwise we'd lose the reference to the rest of the list.

```
Step 1: newNode.next = temp.next
                          new
                           |
                           v
[A] -> [B] -> [C] -> [D] -> null
        ^      ^
      temp   (still also pointed to by B)

Step 2: temp.next = newNode
[A] -> [B] -> [new] -> [C] -> [D] -> null
```

### Step 4: Increase length, return true
```java
length++;
return true;
```

---

## 7. Full Method

```java
public boolean insert(int index, int value) {
    if (index < 0 || index > length) {
        return false;
    }

    if (index == 0) {
        prepend(value);
        return true;
    }

    if (index == length) {
        append(value);
        return true;
    }

    Node newNode = new Node(value);
    Node temp = get(index - 1);

    newNode.next = temp.next;
    temp.next = newNode;

    length++;
    return true;
}
```

---

## 8. Example Walkthrough

- Start: Linked list `[0, 2]`
- Call `insert(1, 1)` — insert value `1` at index `1`
- Index `1` is not `0` and not equal to `length` (`2`) → goes to the middle-insert logic
- `temp = get(0)` → points to node with value `0`
- `newNode.next = temp.next` → new node (`1`) now points to node with value `2`
- `temp.next = newNode` → node `0` now points to new node `1`
- Result: `[0, 1, 2]`

---

## 9. Tested in IntelliJ

1. Created a linked list with values `0` and `2`.
2. Printed the list → showed `0, 2`.
3. Called `insert(1, 1)` — insert value `1` at index `1`.
4. Printed the list again → showed `0, 1, 2`.

---

## Quick Recap (Plain English Summary)

- **Insert** adds a new node with a given value at a given index, returning `true`/`false`.
- **4 cases:**
  1. **Out of range** (`index < 0` or `index > length`) → return `false`.
  2. **Index 0** → just call `prepend()`.
  3. **Index equals length** → just call `append()`.
  4. **Middle of the list** → find the node before the insert point using `get(index - 1)`, then rewire pointers: new node points forward first, then the previous node points to the new node.
- **Big lesson:** reuse existing methods (`prepend`, `append`, `get`) instead of duplicating logic — makes the code shorter and easier to trust.
- **Order matters** when rewiring pointers — always hook the new node forward before changing the previous node's pointer, or you'll lose part of the list.
