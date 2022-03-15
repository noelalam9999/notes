# Algorithms
- Clear and complete set of instruction to solve a problem
- predictable and reliable outcome
- abstract concept, independent of where it is executed (paper, code)
- be aware of your complexity - time and space - huge impact of performance
- possible to come up with your interview - learn to recognize patters (nested for loop is quadratic)

##Complexity analysis and big O notation
- given an algorithm how does the number of operations to reach a solution change as its size increases
- Complexity analysis studies the `time` (i.e. number of operations) and `space` (i.e. amount of storage required) complexity of a given algorithm.
- It describes a dynamic property, it focuses on how the complexity changes as the size of the problem changes.
- It considers the best, average (expected), and worst case scenario.
- Big O notation is a method to annotate complexity. It typically considers the worst case (which often coincides with the average case).

##Constant complexity
- it does not change as the size increases
- It’s written as O(k) or O(1).
- It’s independent of the size of the problem.
- Examples are accessing an item in an array, and reading from or writing to a hash table.
- holy grail of any algorithm as scaling is not an issue

##Logarithmic complexity
- It’s written as O(log n).
- It grows by one each time the size of the problem doubles.
- great for sorting large amounts of data
- An example is searching an item in a binary search tree (unless it’s very unbalanced).

##Linear complexity
- It’s written as O(n).
- It grows proportional to the size of the problem.
- Examples are for loops, and searching for an item in an array or a linked list.

##N log n complexity
- It’s written as O(n log n).
- It grows “log n” times linear to the size of the problem (aka linearithmic).
- combines logarithmic and linear complexity combined
- An example is the merge sort algorithm. 
- divide and conquer family of algorithms

## Quadratic complexity
- It’s written as O(n^2).
- It grows squared to the size of the problem.
- An example is a for loop inside another one.
- bubble sort is example of quadratic

## Exponential complexity
- It’s written as O(2^n).
- It doubles each time the size of the problem increases by one.
- different from quadratic as in quadratic size determines the base. but here size determines the exponent. which is worse.
- opposite of logarithmic 
- An example is generating all possible combinations from a list of elements (without repetitions).

## Factorial complexity
- It’s written as O(n!).
- It grows factorial to the size of the problem.
- An example is generating all possible permutations from a list of elements (without repetitions).
- one of the worst cases

## Comparison
![img.png](media/img.png)

## Graph traversal
- linear data structure - only one way to traverse data (linked list starts at the head, iterating through array goes from 0 to 1)
- non linear data structure - decide which path to take, can end up in an infinite loop

two ways to traverse through a tree
- Breadth-first (horizontally, one level at the time) and depth-first search (vertically first) are methods to traverse any graph (which includes all trees). 
- BFS explores all adjacent nodes before going to the next level, whereas DFS explores a path till the end before exploring any other adjacent nodes.
- The general procedure for a tree starts with storing the root node in a container. Then, while there are nodes in the container, you get the “next” one, and store all its children in the container again, repeating until done. 
- As a container, for breadth-first use a Queue, and for depth-first a Stack. For depth first you can also use recursion and use the call function stack.
- General procedure
  - store the root node in a container
  - while there are nodes in the container
    - get the next node from the container
    - store all its children in the container
    - BFS - queue, DFS - stack
- In a graph, you can start from any vertex, and add the adjacent vertices to the container in any order. If the graph is cyclical, you also you need to keep track of all the visited vertices to avoid processing the same vertex multiple times.
- Breadth-first search is used when the solution is likely located near the starting point or you need to compare all possible paths to a certain node, whereas depth-first search is used when you need to get to the end of a path to understand if it works or not.
- For example, in a graph you use BFS if you want to find the shortest path between two vertices, whereas you use DFS if you want to find the exit of a maze.

### three types of depth traversals
- preorder (Parent, Left, Right), create a new tree and insert
- In-order (Left, Parent, Right) good for binary search trees
- post-order (Right, Left, Parent) remove leaves before leaving the parent