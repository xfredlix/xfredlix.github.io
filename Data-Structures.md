# Data Structures

# Graph
- Nearly all graph problems will somehow use a grid or network in the problem
- Common keywords associated with graph problems are: vertices, nodes, edges, connections, connectivity, paths, cycles and direction
- Consists of two components: nodes and edges
- A vertex (or node) is a discrete position in the graph
- An edge (or connection) is a link between two vertices that can be either directed or undirected and may have a cost associated with it. An undirected edge means that the relationship goes both ways (u,v) is the same as (v,u). A directed edge only allows travel in one direction, so if there were a directed edge from A to B you could travel from A to B, but not from B to A
- Order: The number of vertices in a graph
- Size: The number of edges in a graph
- Types of graphs: singly linked list, tree, 2D array, directed acyclic graph(directed graph with no cycles)

### Edge List
- An array, of ∣E∣ edges, which we call an edge list. To represent an edge, we just have an array of two vertex numbers, or an array of objects containing the vertex numbers of the vertices that the edges are incident on. If edges have weights, add either a third element to the array or more information to the object, giving the edge's weight. Since each edge contains just two or three numbers, the total space for an edge list is O(E)
- If we want to find whether the graph contains a particular edge, we have to search through the edge list. If the edges appear in no particular order, that's a linear search through ∣E∣ edges
- [ [0,1], [0,6], [0,8], [1,4], [1,6], [1,9], [2,4], [2,6], [3,4], [3,5], [3,8], [4,5], [4,9], [7,8], [7,9] ]

### Adjacency Matrix
- 2D array of size V x V where V is the number of vertices in a graph. Let the 2D array be adj[][], a slot adj[i][j] = 1 indicates that there is an edge from vertex i to vertex j. Adjacency matrix for undirected graph is always symmetric. Adjacency Matrix is also used to represent weighted graphs. If adj[i][j] = w, then there is an edge from vertex i to vertex j with weight w
- Pros: Representation is easier to implement and follow. Removing an edge takes O(1) time. Queries like whether there is an edge from vertex ‘u’ to vertex ‘v’ are efficient and can be done in O(1)
- Cons: Consumes more space O(V^2). Even if the graph is sparse(contains less number of edges), it consumes the same space. Adding a vertex is O(V^2) time
- [ [0, 1, 0, 0, 0, 0, 1, 0, 1, 0],
  [1, 0, 0, 0, 1, 0, 1, 0, 0, 1],
  [0, 0, 0, 0, 1, 0, 1, 0, 0, 0],
  [0, 0, 0, 0, 1, 1, 0, 0, 1, 0],
  [0, 1, 1, 1, 0, 1, 0, 0, 0, 1],
  [0, 0, 0, 1, 1, 0, 0, 0, 0, 0],
  [1, 1, 1, 0, 0, 0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0, 0, 0, 0, 1, 1],
  [1, 0, 0, 1, 0, 0, 0, 1, 0, 0],
  [0, 1, 0, 0, 1, 0, 0, 1, 0, 0] ]

### Adjacency List
- Combines adjacency matrices with edge lists. For each vertex ii, store an array of the vertices adjacent to it. We typically have an array of |V|∣V∣ adjacency lists, one adjacency list per vertex.
- Pros: Saves space O(|V|+|E|) . In the worst case, there can be C(V, 2) number of edges in a graph thus consuming O(V^2) space. Adding a vertex is easier
- Cons: Queries like whether there is an edge from vertex u to vertex v are not efficient and can be done O(V)
- For an undirected graph, contains 2|E| elements
- For a directed graph, contains |E| elements
- We can get to each vertex's adjacency list in constant time, because we just have to index into an array. To find out whether an edge (i,j)(i,j) is present in the graph, we go to ii's adjacency list in constant time and then look for jj in ii's adjacency list. How long does that take in the worst case? The answer is \Theta(d)Θ(d), where dd is the degree of vertex ii, because that's how long ii's adjacency list is. The degree of vertex ii could be as high as |V|-1∣V∣−1 (if ii is adjacent to all the other |V|-1∣V∣−1 vertices) or as low as 0 (if ii is isolated, with no incident edges). In an undirected graph, vertex jj is in vertex ii's adjacency list if and only if ii is in jj's adjacency list. If the graph is weighted, then each item in each adjacency list is either a two-item array or an object, giving the vertex number and the edge weight
- [ [1, 6, 8],
  [0, 4, 6, 9],
  [4, 6],
  [4, 5, 8],
  [1, 2, 3, 5, 9],
  [3, 4],
  [0, 1, 2],
  [8, 9],
  [0, 3, 7],
  [1, 4, 7] ]

### DFS
- Utilizes a stack that can either by represented explicitly (by a stack data-type in our language) or implicitly when using recursive functions
- 4 operations on a stack:
Push: Adds an element to the top of the stack
Pop: Removes the top element from the stack
Top: Returns the top element on the stack
Empty: Tests if the stack is empty or not
- Use on problems where we want to find any solution to the problem (not necessarily the shortest path), or to visit all of the nodes in the graph
- Visit a node, then push all of the nodes to be visited onto the stack. To find the next node to visit we simply pop a node off the stack, and then push all the nodes connected to that one onto the stack as well and we continue doing this until all nodes are visited. It is a key property of the Depth First search that we not visit the same node more than once, otherwise it is quite possible that we will recurse infinitely. We do this by marking the node as we visit it
- Mark a vertex visited as we pop

### BFS
- Utilizes a queue, FIFO
- 4 operations on a queue:
Enqueue: Adds an element to the back of the queue
Dequeue: Removes the front element from the queue
Front: Returns the front element on the queue
Empty: Tests if the queue is empty or not
- If all of the edges in a graph are unweighted (or the same weight) then the first time a node is visited is the shortest path to that node from the source node
- A vertex's distance is null until it has been visited, at which time it gets a numeric value for its distance. Therefore, when we examine the neighbors of a vertex, we visit only the neighbors whose distance is currently null
- Breadth-first search assigns two values to each vertex v:
- A distance, giving the minimum number of edges in any path from the source vertex to vertex v
- The predecessor vertex of v along some shortest path from the source vertex. The source vertex's predecessor is some special value, such as null, indicating that it has no predecessor
- If there is no path from the source vertex to vertex v, then v's distance is infinite and its predecessor has the same special value as the source's predecessor
- In BFS, we initially set the distance and predecessor of each vertex to the special value (null). We start the search at the source and assign it a distance of 0. Then we visit all the neighbors of the source and give each neighbor a distance of 1 and set its predecessor to be the source. Then we visit all the neighbors of the vertices whose distance is 1 and that have not been visited before, and we give each of these vertices a distance of 2 and set its predecessor to be vertex from which we visited it. We keep going until all vertices reachable from the source vertex have been visited, always visiting all vertices at distance kk from the source before visiting any vertex at distance k+1
- O(V + E) time complexity

### Dijkstra (Heap method)
- Find the shortest path from one position to another
- Write a BFS, and instead of using a queue you use a Priority queue and define a sorting function on the nodes such that the node with the lowest cost is at the top of the Priority queue. This allows us to find the best path through a graph in O(m * log(n)) time where n is the number of vertices and m is the number of edges in the graph

# Heap
- Semi-ordered data structure: Define some ordering on elements that are inserted into the structure, then the structure keeps the smallest (or largest) element at the top
- 4 operations:
Add: Inserts an element into the heap, putting the element into the correct ordered location O(log n)
Pop: Pops the top element from the heap, the top element will either be the highest or lowest element, depending on implementation O(log n)
Top: Returns the top element on the heap O(1)
Empty: Tests if the heap is empty or not