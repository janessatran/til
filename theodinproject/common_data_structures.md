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

### Analysis of stack operations
- **push**: O(1)
- **pop**: O(1)
- **top**: O(1)
- **search**: O(n)

## What is a queue?

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
