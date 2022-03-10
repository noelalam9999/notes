# Data Structures
- Abstract way to organize data to provide useful properties - detach yourself from code
- Can be represented in many forms - on whiteboard
- Trade offs to decide which one is best for your usecase
- some easy and some can be really complex
- access time and space allocation are important decisions to make when deciding

## Stack
- It’s like a stack of paper.
- It offers “push” (add to the first) and “pop” methods (takes the last one out).
- In programming, function calls form a stack. (call stack, check it out in inspector in source tree)
- It’s a “LIFO” collection (i.e. “last in, first out”).
```javascript
function two () {}
function one () {
  debugger; // will stop execution here in inspector
  two();
}

// the call stack of functions will be one, then two, then two will be executed so will be out and the one will return
```
- not an array in js! In data structure arrays - all elements must be of same type and elements are allocated continuous space in memory. Arrays in C are actual arrays
## Queue
- It’s like a queue at a restaurant.
- It offers “enqueue” (add to the back) and “dequeue” methods (takes the first one out).
- In computers, CPU operations form a queue.
- It’s a “FIFO” collection (i.e. “first in, first out”).


## Linked list
- It’s a linear collection of data elements, called nodes, each pointing to the next node by means of a pointer.
- In double linked lists, each node also has a pointer to the previous one (can then go back to its predecessor)
- Insertion and deletion of nodes is not expensive.
- There is no need to define an initial size.
- It’s a dynamic data structure (no need to preallocate memory)
- in linked list we have to loop to the xth position to access, in arrays we can access using index
- in order to input a new element, in linked list we can just input at that position but in arrays we have to rewrite all the following elements

## Set
- It’s a collection of elements, without any particular order, and no repeated values.
- elements can be members of one or more sets (think venn diagrams)
- sets can have a size property
- Operations that you can perform on sets include:
  - adding and removing members 
  - checking if a set contains an element 
  - calculate the union, intersection, and difference of multiple sets 
  - check if a set is a subset of another

## Tree
- It’s a non-linear collection of nodes that are connected to each other without having any cycles. 
- if you keep going in one direction there is no way you can get back to the original node
- Each node has a value, and can have children, parents, siblings, cousins, descendents, ancestors (just like in a family) and leaves (the last elements)
- Any sub-tree, forms a tree on its own. Subtree can also be called branches
- values do not have to be unique
- good for any branching structure

## Array
- oldest and one of the most important data structures
- It’s an ordered collection of elements, stored next to each other in memory. 
- The total length is known at the beginning, and each element occupies the same size. 
- Elements can be accessed in constant time. (no need to loop through the list but access directly) Because they are allocated next to each other in memory and we know where it starts.
- if we want to add an element in the middle we have to rewrite it though

## Hash table
- It’s a structure that maps keys to values (aka “hash map”). 
- To do so internally it uses an array and a hash function. 
- A hash function maps data of arbitrary size to data of fixed size (aka “hash code”, “digest”, or simply “hash”). 
- Hash functions are deterministic (given the same input they always returns the same output) and uniform (map the expected inputs as evenly as possible over its output range). 
- For the purpose of hash tables, the hash function takes a key and a limit, and returns a number, guaranteeing to distribute keys evenly along the range. 
- When two or more keys are assigned the same index you have a key “collision” (aka “conflict”). 
- Key collisions are handled through linked lists. 
- To avoid too many collisions, or the usage of unnecessary space, hash tables can self-resize.

## Binary tree
- It’s a tree where each node has at most two children. (if each node has only one node then it can still be a binary one)
- The max number of possible nodes is (2^h)-1. h = number of vertical levels.
- Is considered “complete” if every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
- Is considered “full” if every node other than the leaves has two children.
- subset of trees, not a data structure on their own

## Heap
- It’s a semi-sorted tree, where parent nodes values are always greater (or always smaller) than those of their children.
- The most used type of heap is a binary heap, which is a binary tree, ordered as we just mentioned and complete.
- the nodes on one level do not have any relationship to each other directly
- It’s a good tradeoff between the cost of maintaining complete order and the cost of searching through random chaos.
- It’s useful whenever you need to immediately find the object with the highest (or lowest) priority.

## Binary search tree
- It’s a sorted binary tree. 
- Each node can have maximum 2 children (left and right).
- The value in each node must be greater or equal to any value stored in the left sub-tree, and smaller or equal to any value stored in the right sub-tree.
- The shape of the tree depends entirely on the order of insertion or deletion of its nodes.
- balanced = all branches have more or less the same height, the distance from one leaf to the root compared to the distance of any other leaf to the root does not have a difference more than one step
  - takes approximately same time to reach the root
