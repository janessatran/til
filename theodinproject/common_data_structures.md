# Common Data Structures and Algorithms
Notes from Ruby Programming course of [The Odin Project](https://www.theodinproject.com/courses/ruby-programming/lessons/common-data-structures-and-algorithms)

## What is a data structure?
In computer science, it is a data organization, management, and storage format that enables efficient access and modification. More specifically, it's a collection of values, the relatoinships among them, and the functions or operations that can be applied to the data.


## What is a stack?
A stack is an abstract data type with a bounded capacity. It allows adding and removing elements in a particular order.
- Stack is an ordered list of similar data type.
- Stack is LIFO (last in, first out) structure
- the `push()` function is used to insert new element into the stack
- the `pop()` function is used to remove an element from the stack
- insertion and removal are only allowed at the top of the stack

A stack is said to be in **overflow** state when its completely full and is said to be in **underflow** state if it is completely empty. 

![stack drawing](https://www.tutorialspoint.com/data_structures_algorithms/images/stack_representation.jpg)

### Applications of a stack
The simplest application of a stack is to reverse a word. You push a word to the stack, letter by letter, and then pop letters from the stack. Other uses include parsing and expression conversion (infix to postfix, postfix to prefix, etc)

### Complexity Analysis of stack operations
- **push**: O(1)
- **pop**: O(1)
- **top**: O(1)
- **search**: O(n)

## What is a queue?
A queue is an abstract data type in which the first element is inserted from the rear, and the removal of existing elements takes place from the front. 
- FIFO (first in, first out) data structure (element inserted first will be removed first).
- the process to add an element into the queue is called **enqueue**
- the process to remove an element from the queue is called **dequeue**
- queue is also an ordered list of elements of similar data types
- once a new element is inserted into the queue, all the elements inserted before the new element in the queue must be removed to remove the new element
- `peek()` is ofted used to return the value of the first element without dequeueing it

### Applications of a queue
Used whenenever we need to manage groups of objects in an order in which the first one coming in also gets out first. For example:
- Serving requests on a single shared resource (like a printer, CPU task scheduling, etc)
- Call center phone systems to hold people calling them in an order, until a service rep is free
- Handling of interrupts in real-time systems

### Complexity Analysis of stack operations
- **enqueue**: O(1)
- **dequeue**: O(1)
- **size**: O(1)


## What’s the difference between a stack and a queue?

## What is a stack useful for?

## What is a queue useful for?

## What’s the best way to implement stacks and queues in Ruby (hint: think simple)?

## Why bother having many different search algorithms?
## What is breadth-first-search (BFS)?
## What is depth-first-search (DFS)?
## What situations would you want to use BFS?
## What situations would you want to use DFS instead?
## When would BFS be impractical
