# Day 6 — Linked List: Constructor, Print List, Append

**Covers:**
- **Lecture 19:** LL: Constructor
- **Lecture 20:** Coding Exercise 2 — LL Constructor
- **Lecture 21:** LL: Print List
- **Lecture 22:** LL: Append (+ Coding Exercise 3)

---

## Lecture 19: LL Constructor

## 1. The Node Class (building block of Linked List)

- A **node** holds two things:
  - `value` → the actual data (example: a number)
  - `next` → a pointer to the **next node** in the list
- Since `next` is of type `Node`, it means it can **point to another node** (just like a variable pointing to a HashMap in the References lesson).
- The Node class has a simple constructor:
  - It takes in a `value`
  - Sets `this.value = value`
  - `this` is used to say "the value that belongs to this specific node", not the one passed in.

**Simple way to think about it:** A node is like a small box with two compartments — one holds the data, the other holds a "pointer" (arrow) to the next box.

---

## 2. Why Constructor, Append, Prepend, and Insert Are Related
*(Lecture 19 continued)*

These 4 methods all:
1. Get passed a **value**
2. Use that value to **create a new node**

Their jobs differ after that:

| Method | What it does |
|---|---|
| Constructor | Creates the linked list AND creates the first node |
| Append | Creates a node and adds it to the **end** |
| Prepend | Creates a node and adds it to the **beginning** |
| Insert | Creates a node and adds it at a **specific index** |

Since all 4 need to create a node, we don't repeat that code — instead we create **one Node class** that all of them can call.

---

## 3. Linked List Class Variables
*(Lecture 19 continued)*

The Linked List class has 3 private variables:
- `head` → points to the **first node**
- `tail` → points to the **last node**
- `length` → keeps track of how many nodes are in the list (an integer)

Best practice: keep class variables **private**.

---

## 4. Linked List Constructor — Step by Step
*(Lecture 19 continued)*

When we create a new linked list:

1. A new **Node** is created using the value passed in.
2. `head` is set to point to this new node.
3. `tail` is also set to point to this same new node.
4. `length` is set to `1` (since we started with one node).

**Example:**
```java
LinkedList myLinkedList = new LinkedList(4);
```
This creates:
- A node with value `4`
- `head` → points to that node
- `tail` → points to that node
- `length` = 1

### Important Concept: Why `head = newNode` Works
- `newNode` is a variable that **points to** the node we just created (not the node itself).
- When we say `head = newNode`, we are telling `head` to **point to the same node** that `newNode` points to.
- This is the same reference concept from the earlier "References" lesson (like `map1` and `map2` pointing to the same HashMap).

---

## 5. Inner Class (Nested Class) Concept

- The **Node class is written inside the Linked List class** — this is called an **inner class / nested class**.
- Reason: Node is only ever used by the Linked List, so it makes sense to keep it inside.
- Node's variables/methods are **not marked public or private** because that's exactly how they need to be written if you ever want to pull Node out into its own file later.

---

## Lecture 21: LL Print List

## 6. Print List Method

Purpose: Print out all values in the linked list so you can **see what's happening** (useful for testing/debugging).

### How it works:
1. Create a temporary variable `temp` and set it equal to `head` (so `temp` starts at the first node).
2. Start a **while loop**:
   - Print `temp.value`
   - Move `temp` forward using `temp = temp.next`
3. When `temp` becomes `null`, it means we've reached the end of the list → loop stops.

**Example:** If the list has one node with value `11`, it will print `11` and then stop.

### Extra Helper Methods Added:
- `getHead()` → prints the value of the head node
- `getTail()` → prints the value of the tail node
- `getLength()` → prints/returns the length of the list

These are simple "peek" methods used mainly for checking/debugging your list.

---

## Lecture 22: LL Append

## 7. Append Method — Adding a Node to the End

### Goal:
Add a new node to the **end** of the linked list..

### Steps:
1. Create a new node using the value passed in.
2. **Check if the list is empty:**
   - If `length == 0` (list is empty):
     - Set `head = newNode`
     - Set `tail = newNode`
     - (Both head and tail now point to this single new node)
   - Else (list already has items):
     - Set `tail.next = newNode` (the current last node now points to the new node)
     - Set `tail = newNode` (move tail forward to the new node)
3. Increase `length` by 1.

### Why check for empty list separately?
If the list is empty, there is no existing `tail.next` to update — so we must directly set `head` and `tail` to the new node instead.

**Example flow:**
- Start: List has one node → `1`
- Call `append(2)`
- Result: List becomes → `1 → 2`
- `tail` now points to node with value `2`

---

## Quick Recap (Plain English Summary)

- A **Node** = a small container with a value + a pointer to the next node.
- **Linked List** = keeps track of `head` (first node), `tail` (last node), and `length`.
- **Constructor** = creates the list with one starting node; head and tail both point to it.
- **Print List** = walks through the list from head to end using a temporary pointer, printing each value.
- **Append** = adds a new node at the end:
  - If list is empty → head and tail both point to new node.
  - If list has items → old tail points to new node, then tail moves to new node.
- All of this works using **references (pointers)**, not actual copies — same concept from the earlier References lesson.
