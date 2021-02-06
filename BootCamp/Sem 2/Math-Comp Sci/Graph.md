# Graph

A graph is a representation of pairwise relationships between objects. The objects are represented as **nodes** and the relationships are represented by **edges**.

## How do we use graphs

Graphs are used to represent many things - roads connecting cities, links between users in an application (like connections in LinkedIn), websites connected by hyperlinks, computers connected on a network, etc. We can use a representation of that connection information to find a path between two objects, and optimized paths between objects.

Graphs are used to rank pages by search engines. They are used to route network traffic. They are used to suggest the best route on roads in navigation software. There are many applications of graphs and graph theory to solve problems.

#### Undirected vs Directed graphs

In an undirected graph, all relationships between objects are bi-directional. There are no arrows in this graphs.

In a directed graph, relationships are explicitly noted with arrows.

#### Weighted graph

A weighted graph assigns values to edges. These values can be considered when finding the optimal path. This can be noted by a number above the line connecting 2 points.

#### Tree

A tree is an undirected graph in which two vertices are connected by only one path, and every child node has only one parent. A **root node** has no parent. **Leaf nodes** have no children.

There are no loops or circuits.

A good example for a tree would be a computer directory.

#### Binary tree

In a binary search tree (BST), the rule is that the left node is less than it's parent node and the right node is greater than it's parent node.

We can use this to perform binary search.

This would look like the top node holding a 5 and it's child on the left being a 2 and the child on it's right being a 6. This can continue going on.

### Representing graphs - adjacency matrix

Make a table or matrix, with a row and column for each node. Indicate with 0 or 1 if an edge exists between each pair of nodes (where row is the origin and column is the destination edge)

|       | A    | B    | C    | D    |
| ----- | ---- | ---- | ---- | ---- |
| **A** | 0    | 1    | 0    | 0    |
| **B** | 1    | 0    | 0    | 1    |
| **C** | 1    | 0    | 0    | 1    |
| **D** | 0    | 1    | 0    | 0    |

The 0 denotes it can not go in that direction. The 1 results in an option that can be taken.

#### Weighted adjacency matrix

This is the exact same way as above but we use the weight instead of a 1 or 0



|       | A    | B    | C    | D    |
| ----- | ---- | ---- | ---- | ---- |
| **A** | 0    | 2    | 3    | 4    |
| **B** | 2    | 0    | 0    | 5    |
| **C** | 3    | 0    | 0    | 2    |
| **D** | 4    | 5    | 2    | 0    |

### Representing graphs - edge list

An **adjacency list** or **edge list**  can also be used to representing a graph. In this example we can write an edge list as:

G = [AB, BA, BD, CA, CD, DB]

This is an example of a directed graph, or **diagraph**. We could refer to the list as a **diagraph edge list**

#### Weighted, undirected

In an undirected graph, both directions are included for each edge, and weights are specified:

G= [A2B, B2A, A3C, C3A, A4D, D4A, B5D, D5B, C2D, D2C]

Note: you may also see the weights specified a bit differently, such as '2AB' or 'AB2'. It doesn't matter. What's important is that the left node symbol is the origin of the connection.



## Dijkstra's Algorithm

This algorithm is one used to find the shortest path between one node in a weighted graph to every other node. Here are the steps:

Mark distance to the source node as 0 and all other nodes as infinity. Starting with the source node:

1. Mark it as the current node
2. Update distance for all adjacent nodes with the shortest distance from the current node (which is the sum of the shortest distance for the current node and the weight of the edge connecting the current node to this adjacent node)
3. Mark the current node as visited
4. The next current node is an unvisited node that currently has the shortest distance
5. Repeat steps 1-4 until all nodes are marked visited
6. Starting from any destination node, the shortest path can be traced backwards to the source node.


### When Dijkstra's is not appropriate

Dijkstra's algorithm is not appropriate:

- To find the shortest path that **<u>visits all nodes</u>**
- when there is no specific origin node given

Use Dijkstra for finding the shortest path when a specific origin is given, and there is no requirement to visit all nodes.

### The shortest path that visits all nodes

There are no simple algorithms for finding the shortest path that visits all nodes - it's a hard problem. If the graph is small enough, you can do it by brute force- check all paths that visit all nodes and find the least expensive.