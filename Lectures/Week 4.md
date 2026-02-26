# Data Structures
A data structure is a specialized method for organizing and storing data in a computer so that it can be accessed, searched, and manipulated efficiently. The primary goal is to manage data in a way that optimizes performance (speed) and resource utilization (memory space) for various operations.

## Abstract vs. Concrete Data Types
When discussing data structures, it's important to distinguish between abstract data types (ADTs) and concrete data structures:

-   **Abstract Data Type (ADT)**: An ADT defines a logical model for a data type, specifying the operations that can be performed on the data without detailing how these operations are implemented. It focuses on *what* the data represents and *what* can be done with it, rather than *how* it's stored or *how* the operations work internally. Examples include Stacks, Queues, Lists, and Maps.
-   **Concrete Data Structure**: This refers to the actual implementation of an ADT. It describes *how* the data is physically stored in memory and *how* the operations defined by the ADT are carried out. For instance, a "List" ADT can be concretely implemented using a "Linked List" or a "Dynamic Array".

## Dynamic vs. Static Data Structures
Data structures can also be categorized based on how their size and memory are managed:

-   **Static Data Structures**: These data structures have a fixed size that is determined at compile time or when they are first created. Their memory allocation is typically contiguous and cannot be changed during program execution. Arrays in many languages are often static, requiring you to specify their maximum capacity upfront. While efficient for fixed-size data, they can lead to wasted space if the actual data is smaller than the allocated size, or overflow if the data exceeds the allocated size.
-   **Dynamic Data Structures**: In contrast, dynamic data structures can grow or shrink in size during program execution as needed. Their memory is allocated and deallocated at runtime. This flexibility makes them highly adaptable to varying amounts of data. Examples include Linked Lists, Trees, and Dynamic Arrays (which, despite their name, are a dynamic implementation of an array concept). They offer better memory utilization but might incur a slight overhead for memory management.

## Stacks and Queues

### Stack

![[stack-operations-ex.png| center | 600]]

A stack is a linear data structure that follows the Last-In, First-Out (LIFO) principle. This means the last element added to the stack is the first one to be removed. Imagine a stack of plates: you can only add a new plate to the top, and you can only remove the topmost plate.

Stacks typically support the following primary operations:
-   **PUSH(x)**: Adds an element `x` to the top of the stack.
-   **POP()**: Removes and returns the most recently added element (the top element) from the stack. If the stack is empty, it usually results in an error or returns a special value.
-   **ISEMPTY()**: Returns `true` if the stack contains no elements, and `false` otherwise.
-   **PEEK()** (or TOP()): Returns the top element of the stack without removing it.

```java
import java.util.ArrayList;
import java.util.EmptyStackException; // For handling pop/peek on empty stack

public class MyStack<T> {
    private ArrayList<T> stackList;

    public MyStack() {
        stackList = new ArrayList<>();
    }

    // PUSH operation: Add an element to the top of the stack
    public void push(T item) {
        stackList.add(item);
        System.out.println("Pushed: " + item);
    }

    // POP operation: Remove and return the top element
    public T pop() {
        if (isEmpty()) {
            throw new EmptyStackException();
        }
        T item = stackList.remove(stackList.size() - 1);
        System.out.println("Popped: " + item);
        return item;
    }

    // PEEK operation: Return the top element without removing it
    public T peek() {
        if (isEmpty()) {
            throw new EmptyStackException();
        }
        return stackList.get(stackList.size() - 1);
    }

    // ISEMPTY operation: Check if the stack is empty
    public boolean isEmpty() {
        return stackList.isEmpty();
    }

    // Optional: Get the size of the stack
    public int size() {
        return stackList.size();
    }
}
```

-   **Time Complexity**:
    -   PUSH: O(1) time.
    -   POP: O(1) time.
    -   ISEMPTY: O(1) time.
-   **Space Complexity**:
    -   O(N) space, where N is the number of elements in the stack.
-   **Limitations (for static array-based implementations)**:
    -   Capacity must be known upfront.
    -   Can lead to wasted space if not fully utilized.
    -   Can lead to overflow if data exceeds allocated capacity.

#### Applications of Stacks
-   **Virtual machines**: Used in the execution of bytecode (e.g., Java Virtual Machine, .NET Common Language Runtime) to manage the call stack for method invocations and local variables.
-   **Parsing**: Compilers and interpreters use stacks to parse expressions, check for balanced parentheses, and evaluate arithmetic expressions (e.g., converting infix to postfix notation).
-   **Function calls**: The call stack in programming languages is a stack data structure that keeps track of active function calls, local variables, and return addresses.
-   **Backtracking**: Algorithms that explore multiple paths (like solving mazes, N-Queens problem, or generating permutations) often use a stack to remember previous states and backtrack when a path leads to a dead end.

### Queue
![[queue-operations-ex.png| center | 200]]

A queue is a linear data structure that follows the First-In, First-Out (FIFO) principle. This means the first element added to the queue is the first one to be removed. Imagine a line of people waiting for a service: the person who arrived first is the first to be served.

Queues typically support the following primary operations:
-   **ENQUEUE(x)**: Adds an element `x` to the rear (end) of the queue.
-   **DEQUEUE()**: Removes and returns the earliest added element (the front element) from the queue. If the queue is empty, it usually results in an error or returns a special value.
-   **ISEMPTY()**: Returns `true` if the queue contains no elements, and `false` otherwise.
-   **PEEK()** (or FRONT()): Returns the front element of the queue without removing it.

Here's a simple C# implementation of a queue using a `List<T>`:

```csharp
using System;
using System.Collections.Generic;

public class MyQueue<T>
{
    private List<T> queueList;

    public MyQueue()
    {
        queueList = new List<T>();
    }

    // ENQUEUE operation: Add an element to the rear of the queue
    public void Enqueue(T item)
    {
        queueList.Add(item);
        Console.WriteLine($"Enqueued: {item}");
    }

    // DEQUEUE operation: Remove and return the front element
    public T Dequeue()
    {
        if (IsEmpty())
        {
            throw new InvalidOperationException("Queue is empty.");
        }
        T item = queueList[0];
        queueList.RemoveAt(0);
        Console.WriteLine($"Dequeued: {item}");
        return item;
    }

    // PEEK operation: Return the front element without removing it
    public T Peek()
    {
        if (IsEmpty())
            {
            throw new InvalidOperationException("Queue is empty.");
        }
        return queueList[0];
    }

    // ISEMPTY operation: Check if the queue is empty
    public bool IsEmpty()
    {
        return queueList.Count == 0;
    }

    // Optional: Get the size of the queue
    public int Size()
    {
        return queueList.Count;
    }
}
```

-   **Time Complexity**:
    -   ENQUEUE: O(1) time.
    -   DEQUEUE: O(1) time.
    -   ISEMPTY: O(1) time.
-   **Space Complexity**:
    -   O(N) space, where N is the number of elements in the queue.
-   **Limitations (for static array-based implementations)**:
    -   Capacity must be known upfront.
    -   Can lead to wasted space if not fully utilized.
    -   Can lead to overflow if data exceeds allocated capacity.

#### Applications of Queues
-   **Scheduling processes**: Operating systems use queues to manage processes waiting for CPU time (e.g., ready queue) or I/O operations.
-   **Buffering**: Data streams (like audio/video playback, network communication, or printer spooling) use queues to temporarily store data before it's processed, smoothing out variations in data rates.
-   **Breadth-first searching**: Graph traversal algorithms like Breadth-First Search (BFS) use a queue to explore nodes level by level, ensuring all neighbors at the current depth are visited before moving to the next depth.

## Linked Lists

![[linked-list-ex.png | center | 600]]

A linked list is a fundamental and flexible data structure used to maintain a dynamic sequence of items. Unlike arrays, linked lists do not store elements in contiguous memory locations, providing greater flexibility for insertions and deletions.

A linked list is a recursive data structure, meaning its definition refers to itself. Specifically, a linked list is either:
-   **Empty**: It contains no elements.
-   **A reference to a node**: This node, in turn, contains a reference to another linked list (which could be empty or another node).

### Node
At the core of a linked list is the **Node**. A node is an object that typically stores two pieces of information:
-   **Item (or Data)**: The actual value or a reference to the item that the node holds.
-   **Reference (or Pointer)**: A reference (or pointer) to the next node in the sequence. In the case of the last node in the list, this reference is usually `null` (or equivalent) to signify the end of the list.

### Time Complexity
-   Insert at the head of the list: O(1) time.
-   Delete at the head of the list: O(1) time.
-   Traverse the list: O(n) time.

### Space Complexity
-   A list of n items uses O(n) space.

### Related Concepts and Implementations
-   **Other linked data structures**: Linked lists are foundational for more complex structures like cyclic lists, trees, and graphs.
-   **Stacks and Queues using Linked Lists**: Linked lists provide an efficient way to implement Stacks and Queues, offering dynamic resizing capabilities.
    -   **Stack**:
        -   Time: PUSH, POP, ISEMPTY in O(1) time.
        -   Space: O(n)
    -   **Queue**:
        -   Time: ENQUEUE, DEQUEUE, ISEMPTY in O(1) time.
        -   Space: O(n)

![[linked-list-application-ex.png | center | 600]]

Here's a basic C implementation of a singly linked list:

```c
#include <stdio.h>
#include <stdlib.h> // Required for malloc and free

// Define the structure for a Node
typedef struct Node {
    int data;           // Data stored in the node
    struct Node* next;  // Pointer to the next node in the list
} Node;

// Function to create a new node
Node* createNode(int data) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL) {
        printf("Memory allocation failed!\n");
        exit(1); // Exit if memory allocation fails
    }
    newNode->data = data;
    newNode->next = NULL; // New node initially points to NULL
    return newNode;
}

// Function to insert a new node at the beginning of the list
Node* insertAtBeginning(Node* head, int data) {
    Node* newNode = createNode(data);
    newNode->next = head; // New node points to the current head
    return newNode;       // New node becomes the new head
}

// Function to print the linked list
void printList(Node* head) {
    Node* current = head;
    printf("Linked List: ");
    while (current != NULL) {
        printf("%d -> ", current->data);
        current = current->next;
    }
    printf("NULL\n");
}

// Function to free all nodes in the linked list to prevent memory leaks
void freeList(Node* head) {
    Node* current = head;
    Node* nextNode;
    while (current != NULL) {
        nextNode = current->next; // Save the next node
        free(current);            // Free the current node
        current = nextNode;       // Move to the next node
    }
    printf("List freed successfully.\n");
}
```

## Dynamic Arrays

A dynamic array, also known as a resizable array or array list, is a data structure that provides array-like capabilities with the ability to automatically resize itself when elements are added or removed. Unlike static arrays, which have a fixed size determined at compile time, dynamic arrays can grow or shrink during runtime, offering more flexibility.

### Implementing a Stack with Dynamic Arrays

The challenge with implementing a stack efficiently using traditional arrays is the fixed capacity. Can we achieve linear space and constant time operations without needing a fixed capacity upfront?

**Goal:**
-   Implement a stack using arrays in O(n) space for `n` elements.
-   Achieve operations as fast as possible.
-   Focus on PUSH operations initially.

#### Solution 1: Resizing by +1
This approach involves creating a new array of size `current_size + 1` for every PUSH operation when the array is full.

![[dynamic-array-n+1.png | center | 400]]

-   **PUSH(x)**:
    -   Allocate a new array of size `current_size + 1`.
    -   Move all existing elements to the new array.
    -   Add the new element `x`.
    -   Delete the old array.
-   **Time Complexity**:
    -   The `i`-th PUSH operation takes O(i) time because `i-1` elements need to be copied.
    -   The total time for `n` PUSH operations is $1 + 2 + 3 + \dots + n = O(n^2)$.
-   **Space Complexity**: O(n) for `n` elements.

This solution is inefficient due to the quadratic time complexity for PUSH operations.

**Rust Implementation:**

```rust
pub struct StackNaive<T> {
    data: Vec<T>,
}

impl<T> StackNaive<T> {
    pub fn new() -> Self {
        StackNaive {
            data: Vec::with_capacity(0),
        }
    }

    pub fn push(&mut self, x: T) {
        // Naive approach: when array is full, allocate new array of size current_size + 1
        if self.data.len() == self.data.capacity() {
            let mut new_data = Vec::with_capacity(self.data.len() + 1);
            // Copy all existing elements to the new array
            for item in self.data.drain(..) {
                new_data.push(item);
            }
            self.data = new_data;
        }
        self.data.push(x);
    }

    pub fn pop(&mut self) -> Option<T> {
        self.data.pop()
    }

    pub fn is_empty(&self) -> bool {
        self.data.is_empty()
    }

    pub fn size(&self) -> usize {
        self.data.len()
    }
}
```

#### Solution 2: Resizing by Doubling
To improve efficiency, we can reduce the frequency of array reallocations by doubling the array size when it becomes full.

![[dynamic-array-n*2.png | center | 400]]

-   **PUSH(x)**:
    -   If the array is full:
        -   Allocate a new array of twice the current size.
        -   Move all existing elements to the new array.
        -   Delete the old array.
    -   Add the new element `x`.
-   **Time Complexity**:
    -   A PUSH operation that triggers a resize (e.g., at sizes $1, 2, 4, 8, \dots, 2^k$) takes O($2^k$) time to copy elements.
    -   All other PUSH operations take O(1) time.
    -   The total time for `n` PUSH operations is approximately $1 + 2 + 4 + 8 + \dots + 2^{\log n} + (\text{remaining O(1) pushes}) = O(n)$.
    -   This means the amortized time complexity per PUSH operation is O(1).
-   **Space Complexity**: O(n) for `n` elements.

This doubling strategy significantly improves performance, achieving linear total time for `n` operations.

**Rust Implementation:**

```rust
pub struct StackDoubling<T> {
    data: Vec<T>,
}

impl<T> StackDoubling<T> {
    pub fn new() -> Self {
        StackDoubling {
            data: Vec::with_capacity(1),
        }
    }

    pub fn push(&mut self, x: T) {
        // Doubling strategy: when array is full, double the capacity
        if self.data.len() == self.data.capacity() {
            let new_capacity = if self.data.capacity() == 0 { 
                1 
            } else { 
                self.data.capacity() * 2 
            };
            let mut new_data = Vec::with_capacity(new_capacity);
            // Copy all existing elements to the new array
            for item in self.data.drain(..) {
                new_data.push(item);
            }
            self.data = new_data;
        }
        self.data.push(x);
    }

    pub fn pop(&mut self) -> Option<T> {
        self.data.pop()
    }

    pub fn is_empty(&self) -> bool {
        self.data.is_empty()
    }

    pub fn size(&self) -> usize {
        self.data.len()
    }

    pub fn capacity(&self) -> usize {
        self.data.capacity()
    }
}
```

### Stack and Queue with Dynamic Arrays
-   **Stack with Dynamic Array**:
    -   `n` PUSH, POP, and ISEMPTY operations can be performed in O(n) total time and O(n) space.
    -   The time complexity is amortized O(1) per operation.
    -   With more advanced techniques, it's possible to deamortize to achieve O(1) worst-case time per operation.
-   **Queue with Dynamic Array**:
    -   Similar results can be achieved for queues, with amortized O(1) time for ENQUEUE, DEQUEUE, and ISEMPTY operations.

### Global Rebuilding
Dynamic arrays are a prime example of a technique called **global rebuilding**. This technique is used to make static data structures (like fixed-size arrays) dynamic by periodically rebuilding the entire structure into a larger (or smaller) one when its capacity is exhausted or underutilized.

