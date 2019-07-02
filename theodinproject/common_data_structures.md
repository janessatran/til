# Common Data Structures and Algorithms
Notes from Ruby Programming course of [The Odin Project](https://www.theodinproject.com/courses/ruby-programming/lessons/common-data-structures-and-algorithms)

## What is a data structure?
In computer science, it is a data organization, management, and storage format that enables efficient access and modification. More specifically, it's a collection of values, the relatoinships among them, and the functions or operations that can be applied to the data.


# What is a stack?
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

# What is a queue?
A queue is an abstract data type in which the first element is inserted from the rear, and the removal of existing elements takes place from the front. 
- FIFO (first in, first out) data structure (element inserted first will be removed first).
- the process to add an element into the queue is called **enqueue**
- the process to remove an element from the queue is called **dequeue**
- queue is also an ordered list of elements of similar data types
- once a new element is inserted into the queue, all the elements inserted before the new element in the queue must be removed to remove the new element
- `peek()` is ofted used to return the value of the first element without dequeueing it

![stack drawing](https://www.studytonight.com/data-structures/images/introduction-to-queue.png)


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
A stack is first in, last out while a queue is first in, first out.

## What is a stack useful for?
A stack is useful for reversing a string or converting an infix expression to a postfix expression.

## What is a queue useful for?
A queue is useful for when you need to manage a group of objects in the order of when they came into the queue. 

## What’s the best way to implement stacks and queues in Ruby (hint: think simple)?
In Ruby, a stack can be easily implemented using the `Array` class. We can restrict the interface that wraps the array with the `push` and `pop` operations, as well as `size` to emulate stack functionality. 

```ruby
class Stack
  def initialize(capacity)
    @store = Array.new(capacity)
    @store.capacity = capacity
  end
  
  def full?
    @store.size == @store.capacity
  end
  
  def pop
    if @store.nil?
      return nil
    else
      @store.pop
    end
  end
  
  def push(element)
    if @store.full?
      return nil
    else
      @store.push(element)
    end
  end
  
  def size
    @store.size
  end
end
```

Similarly, we can use the `Array` class to create a queue by implementing the `enqueue` and `dequeue` operations. Unlike a stack, a queue is unbounded, so we can use the ruby method `unshift` to insert elements and `pop` to remove an element. 

```ruby
class Queue
  def initialize
    @store = Array.new
  end
  
  def dequeue
    @store.pop
  end
  
  def enqueue(element)
    @store.unshift(element)
    self
  end
  
  def size
    @store.size
  end
end
```

## Why bother having many different search algorithms?
## What is breadth-first-search (BFS)?
## What is depth-first-search (DFS)?
## What situations would you want to use BFS?
## What situations would you want to use DFS instead?
## When would BFS be impractical
