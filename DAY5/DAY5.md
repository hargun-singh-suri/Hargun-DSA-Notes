# DSA Course Notes

## 14. Classes

- A **class** is like a *cookie cutter* — it's not a cookie itself, but you use it to create (many) cookies.
- Example: We create a class called `Cookie`.
- **Class variables** (also called fields):
  - Best practice: keep them **private**.
  - Example: `Cookie` has one variable → `color`.
- **Constructor**:
  - A special method used to create a new object from the class.
  - It always has the **same name as the class** (e.g., `Cookie()`).
  - When called, it sets up the object — here it takes a `color` and stores it using `this.color = color`.
  - `this` refers to *this specific object* being created (not all cookies, just the one being made right now).
- **Creating objects (instances)**:
  - `Cookie cookie1 = new Cookie("green");` → creates a green cookie.
  - `Cookie cookie2 = new Cookie("blue");` → creates a blue cookie.
  - `new` keyword = "run the constructor and build a new object."
  - `cookie1` and `cookie2` are two separate instances of the same class.
- **Other methods** (besides constructor):
  - `getColor()` → returns the color of that specific cookie.
  - `setColor(color)` → changes the color of that specific cookie.
- **Syntax to call a method**: `instanceName.methodName()`
  - Example: `cookie1.getColor()` → prints `"green"`
  - After `cookie1.setColor("yellow")` → `cookie1.getColor()` now prints `"yellow"`
- **Why this matters for the course**:
  - Every data structure (linked list, stack, queue, etc.) will be built as a class.
  - Each will have a constructor + methods like `append`, `remove`, `insert`, etc.
  - Understanding classes conceptually is key before building data structures.

---

## 15. References

- In Java, variables either hold a **value** or hold a **reference**.

### Value type variables
- Example: `int num1 = 11;`
- `num1` directly holds the value `11`.
- If `num2 = num1;` → `num2` also becomes `11`, but they are **independent**.
- Changing `num1` later (e.g., to `22`) does **not** affect `num2`.

### Reference type variables
- Example: `map1` is set equal to a `HashMap`.
- `map1` does **not** hold the actual HashMap — it holds the **address/reference** pointing to it.
- If `map2 = map1;` → `map2` does **not** get its own copy. Both `map1` and `map2` now point to the **same** HashMap in memory.
- So if you change a value through `map1`, it will reflect when accessed through `map2` too — because they're pointing to the same object.

### Reassigning references
- `map2 = map3;` → now `map2` points to `map3`'s HashMap instead. `map1` still points to the old one.
- `map1 = map2;` → now `map1` also points to the same HashMap as `map2` and `map3`.
- The old HashMap that nothing points to anymore becomes **unusable** — it's stuck in memory with no way to access it.
- **Garbage Collection**: Java automatically finds these "orphaned" objects (nothing pointing to them) and removes them from memory periodically.

### Why this matters (Linked Lists preview)
- Instead of `map1`, `map2`, `map3` pointing to HashMaps, think of `node1`, `node2`, `node3` pointing to **nodes**.
- If `node1`'s value is changed, and `node2`/`node3` point to the same node, they'll reflect the same change.
- **`head`** variable in a linked list = a reference that points to a node (the first one).
- `temp = head;` → `temp` now points to the *same* node that `head` points to (not a new copy).
- Each node also has its own pointer to the **next** node.
- If a variable/pointer is not pointing to anything → it is `null`.
- The **last node** in a linked list always points to `null` → called a **null-terminated list**.
- To make `head` point to a different node (say, the 2nd node), you set `head` equal to the reference/pointer that already points to that node.
- This is exactly what happens when **removing the first node** from a linked list — `head` gets reassigned to point to the next node.
- If **all** nodes are removed → `head = null` (empty linked list).

**Key takeaway**: Any variable pointing to a node is a *reference*, not an actual value — this concept applies throughout linked lists, doubly linked lists, stacks, queues, and binary search trees.

---

## 16. Linked List: Intro

- A **linked list** is most often compared to an **array list** because both are **dynamic in length** (unlike plain arrays, which are fixed length).

### Key differences from Array List
1. **No indexes** — you can't jump directly to an item using an index like `list[2]`.
2. **Not stored contiguously in memory** — nodes are scattered around, not stored next to each other like an array list.

### Visual representation (just a teaching convention)
- Array lists/arrays → shown as **green squares** (stored together in memory).
- Linked lists → shown as **purple circles** (scattered in memory, connected via pointers).

### Structure of a Linked List
- **`head`** → pointer to the **first** node.
- **`tail`** → pointer to the **last** node.
- Each node has a pointer to the **next** node, forming a chain.
- The **last node's pointer** = `null` (points to nothing).

### Summary
- Because nodes are spread out in memory (not contiguous), we **cannot use indexes** like we do with arrays/array lists.
- This lack of contiguous memory is the core reason for most differences between array lists and linked lists.

---

## 17. Linked List: Big O

Big O here is measured based on `n` = number of nodes in the list.

| Operation | Big O | Why |
|---|---|---|
| Add to end | O(1) | Just point `tail`'s pointer to new node, move `tail`. Fixed steps regardless of list size. |
| Remove from end | O(n) | To move `tail` back one node, you must start at `head` and iterate all the way to the second-last node (no going backwards). |
| Add to front (prepend) | O(1) | Point new node to `head`, then move `head` to new node. Fixed steps. |
| Remove from front | O(1) | Move `head` to `head.next`, then remove old first node. Fixed steps. |
| Insert in the middle | O(n) | Must iterate from `head` to reach the insertion point first. |
| Remove from middle | O(n) | Must iterate from `head` to reach that node first. |
| Search by value | O(n) | Must check each node one by one until value is found. |
| Search by index | O(n) | Must iterate from `head`, counting nodes, until reaching that index. |

### Linked List vs Array List — quick comparison
- **Array List wins at**:
  - Removing the last item
  - Looking up an item by index
  (because array lists use direct indexing)
- **Linked List wins at**:
  - Adding to the front (prepend) → O(1) vs O(n) for array list (array list must re-index everything)
  - Removing from the front → O(1) vs O(n) for array list

**Key takeaway**: Linked lists are great for adding/removing at the front. Array lists are great for random access (by index) and removing from the end.

---

## 18. Linked List: Under the Hood

- A **node** = a value + a pointer to the next node (both bundled together in one unit).
- Think of a node like a small hash map/object holding: `{ value: ..., next: pointer }`.

### How linking works
- To connect one node to the next: just set the current node's `next` pointer **equal to** the new node.
  - This works the same way as reference assignment (from the References topic) — you're not copying the node, just pointing to it.
- This same logic applies to **every node** in the list — each one's `next` pointer is set to point to the following node.

### Head and Tail under the hood
- `head` = set equal to the **first node** → so `head` just points to it.
- `tail` = set equal to the **last node** → so `tail` just points to it.

### Two ways to think about a linked list
1. **Conceptual/diagram view** — simple circles connected by arrows (easier to understand visually).
2. **Under-the-hood view** — each node is really like a small object/hash map, and the "connections" are just reference pointers stored inside each node.

**Key takeaway**: A linked list *looks* like a simple chain in diagrams, but internally it's built entirely using reference pointers (from the References concept) connecting node objects together.
