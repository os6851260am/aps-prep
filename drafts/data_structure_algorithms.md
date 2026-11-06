# Data Structure & Algorithms

I learned a bunch of data structures and its associated algorithms: Linked List, ADT, BST, Graph, Hash Table.

## Linked List

Linked list is a kind of data type which is not continuous in memory. It’s composed by nodes. Nodes comprise 2 parts: data and next pointer which points to the next node. Therefore, the nodes could be linked. 

## ADT

Abstract Data Types. It includes interface and implementation. The same interface could have varied implementations. We mainly learned 2 types: 1. Stack, 2. Queue

Stack’s feature is LIFO: Last in First out, just like a stack of plates which we could only take the one last pushed in.

Queue’s feature is FIFO: First in first out, as its name, the oldest one would quit at first.
They both could be implemented by array or linked list.

## BST

### BST Data Structure

BST is a kind of linked list: the difference is BST have two next pointers: left and right which point to left child and right child. Left child is less than its parent and right child is bigger. 

### BST: Balancing Algorithms

Sometimes the tree would be unbalanced which cause low performance. So we need some operations to rebalance it: Rotation and Partition.

1. Rotation: Left and Right.
2. Partition: given i, find the node indexed by i, make i the new root by rotation.

## Graph

 Graph is comprised by vertices and edges. 

### Representation

It’s hard to store in memory, so people came up with some means to represent graph: Adjacent Matrix, Adjacent List, Adjacent Edges Array. And we mainly focused on Adjacent List.

Adjacent List is a 2-d pointer array: [edges], [# of Vertices], [# of Edges]. In [edges], the array store the edges by pointer.

### Traversal Algorithms

1. BFS: Bread First Search
2. DFS: Depth First Search

### Shortest Path Algorithms

Dijsktra Algorithm

Destine the source, choose the closest adjacent vertex each step, go back meeting dead end.

### Minimum Spanning Tree

1. Kruskal’s Algorithm
    
    Create a duplicate with only vertices, choose the shortest edge adding in.
    
2. Prim’s Algorithm
    
    Create empty graph, destine a source vertex, choose the closest vertex adding into graph. 
    

## Hash Table

In ordinary array, we can only find the data by index. Index often make no sense, so people thought a new data structure: Hash Table. It is comprised of key-value pairs. A single key could map to multiple values.

### Hash Function

### Collision

The range of key is infinite,  but the bucket is finite, it would cause collision.

3 Solutions: 

1. Chaining: each key mapping to a linked list.
2. Open Addressing: e.g. linear probing.
3. Double Hashing