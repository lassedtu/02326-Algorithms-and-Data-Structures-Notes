Abstract data types and concrete data types describe two different layers of thinking about data.

---

## Natural Explanation

An ADT is the interface idea: what operations are available and what behavior they promise.
A concrete type is the implementation choice: how those operations are actually carried out in memory.

Simple way to think about it:
- ADT = contract.
- Concrete type = engineering design that fulfills the contract.

Example:
- Stack ADT says PUSH, POP, PEEK, ISEMPTY.
- You can implement it with a dynamic array or a linked list.

---

## Academic View

An abstract data type specifies:
- A set of values.
- A set of operations.
- Semantic rules (preconditions/postconditions/invariants) for those operations.

It intentionally hides representation details.

A concrete data type (or concrete data structure) specifies:
- The memory representation of data.
- The exact algorithms used for each operation.
- Resulting time and space costs.

So one ADT can have multiple concrete implementations with different complexity trade-offs.

---

## Why This Distinction Matters

- It separates specification from implementation.
- It allows replacing implementations without changing external usage.
- It makes complexity analysis clearer:
  - ADT tells you what operation you need.
  - Concrete type determines how fast that operation is.

---

## Common Examples

- List ADT:
  - Concrete choices: dynamic array, linked list.
- Queue ADT:
  - Concrete choices: circular array, linked list with head/tail pointers.
- Map ADT:
  - Concrete choices: hash table, balanced binary search tree.

---

## Complexity Perspective

Same ADT, different implementation, different costs.

Example for Stack ADT:
- Dynamic array implementation:
  - PUSH/POP are amortized $O(1)$.
- Linked list implementation:
  - PUSH/POP are worst-case $O(1)$.

Both satisfy the Stack ADT contract, but performance behavior differs.

---

## Pitfalls

- Treating an ADT and one concrete implementation as the same thing.
- Comparing algorithms without stating which implementation is used.
- Ignoring representation constraints (for example, random access in arrays vs pointer traversal in linked lists).

---

## Related

- [[Amortized Analysis]]
- [[Searching Algorithms]]
- [[Sorting Algorithms]]
- [[Lectures/Week 4]]
