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

#### Applications of a stack
The simplest application of a stack is to reverse a word. You push a word to the stack, letter by letter, and then pop letters from the stack. Other uses include parsing and expression conversion (infix to postfix, postfix to prefix, etc)

#### Complexity Analysis of stack operations
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

![queue drawing](https://www.studytonight.com/data-structures/images/introduction-to-queue.png)


#### Applications of a queue
Used whenenever we need to manage groups of objects in an order in which the first one coming in also gets out first. For example:
- Serving requests on a single shared resource (like a printer, CPU task scheduling, etc)
- Call center phone systems to hold people calling them in an order, until a service rep is free
- Handling of interrupts in real-time systems

#### Complexity Analysis of stack operations
- **enqueue**: O(1)
- **dequeue**: O(1)
- **size**: O(1)


### What’s the difference between a stack and a queue?
A stack is first in, last out while a queue is first in, first out.

### What is a stack useful for?
A stack is useful for reversing a string or converting an infix expression to a postfix expression.

### What is a queue useful for?
A queue is useful for when you need to manage a group of objects in the order of when they came into the queue. 

### What’s the best way to implement stacks and queues in Ruby (hint: think simple)?
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
An **algorithm** is a sequence of computational steps that transform the input into the output. There are many different search algorithms because they satisfy different sorting use-cases. For example, merge sort is good for sorting linked lists while heap sort is good for sorting arrays. 

## What is breadth-first-search (BFS)?
It is a traversing algorithm where you start from a selected node, traverse the graph layer wise (exploring the neighbor nodes which are directly connected to the source node), and then move towards the next level of nodes. 

You are required to traverse the graph breadthwise as follows:
1. first move horizontally and visit all the nodes of the current layer
2. move to the next layer

![BFS algorithm drawing](https://he-s3.s3.amazonaws.com/media/uploads/fdec3c2.jpg)

To avoid processing the same node again, use a boolean array which marks the node after it is processed. While visiting the nodes in the layer of a graph, store them in a manner such that you can traverse the corresponding child nodes in a similar order. In the diagram above, we start at 0 and visit the child nodes 1, 2, and 3. We store them in the array in the order they are visited and then begin visiting their child nodes in order (1 first- 4 and 5; 2- 6 and 7, etc). Use a queue to store the node and mark it as "visited" until all its neighbors are marked. Using a queue ensures that the node is visited in the order they are inserted.

More information on the algorithm [here](https://www.hackerearth.com/practice/algorithms/graphs/breadth-first-search/tutorial/).

## What is depth-first-search (DFS)?
A recursive algorithm that uses the idea of backtracking. It involves exhaustive searches of all the nodes by going ahead, if possible, else backtracking. 

Backtracking means that when you are moving forward and there are no more nodes along the current path, you move backwards on teh same path to find nodes to traverse. All nodes will be visited on the current path till all the univisted nodes have been traversed, after which the next path will be selected.

The recursive nature of DFS is implemented with stacks. 
- Pick a starting node and push all its adjacent nodes into the stack
- Pop a node from a stack to select the next node to visit and push all its adjacent nodes into a stack
- Repeat process until the stack is empty. However, ensure that the nodes that are visited are marked. 

*In depth-first search, we can determine whether two nodes x and y have a path between them by looking at the children of the starting node and recursively determining if a path exists.*

## What situations would you want to use BFS?
If we want to find the shortest path between two nodes in a graph. 

## What situations would you want to use DFS instead?
If you want to determine if there is a path between two nodes.

## When would BFS be impractical
If you have a really big graph. In order to traverse it, you have to store the entire graph which can cost a lot in space and memory.
