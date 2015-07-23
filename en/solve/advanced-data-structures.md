#Advanced Data Structures
##Tree Algorithms

1. PARENT(n, T). This function returns the parent of node n in tree T. If n is the root, which has no parent, Λ is returned. In this context, Λ is a "null node," which is used as a signal that we have navigated off the tree.
2. LEFTMOST_CHILD(n, T) returns the leftmost child of node n in tree T, and it returns Λ if n is a leaf, which therefore has no children.
3. RIGHT_SIBLING(n, T) returns the right sibling of node n in tree T, defined to be that node m with the same parent p as n such that m lies immediately to the right of n in the ordering of the children of p. For example, for the tree in Fig. 3.7, LEFTMOST_CHILD(n2) = n4; RIGHT_SIBLING(n4) = n5, and
RIGHT_SIBLING (n5) = Λ.
4. LABEL(n, T) returns the label of node n in tree T. We do not, however, require labels to be defined for every tree.
5. CREATEi(v, T1, T2, . . . , Ti) is one of an infinite family of functions, one for each value of i = 0, 1, 2, . . .. CREATEi makes a new node r with label v and
gives it i children, which are the roots of trees T1, T2, . . . , Ti, in order from
the left. The tree with root r is returned. Note that if i = 0, then r is both a leaf
and the root.
6. ROOT(T) returns the node that is the root of tree T, or Λ if T is the null tree.
7. MAKENULL(T) makes T be the null tree.

|Algorithms|Application
|----|----|----|
|Preorder Traverse|1. duplicate binary tree<br/>2. prefix expression|
|Inorder Traverse|1. binary search tree
|Postorder Traverse|1. delete / free a binary tree<br/>2. postfix representation

```
iterativePreorder(node)
  parentStack = empty stack
  while (not parentStack.isEmpty() or node ≠ null)
    if (node ≠ null) 
      visit(node)
      if (node.right ≠ null) parentStack.push(node.right) 
      node = node.left   
    else     
      node = parentStack.pop()
```

```
iterativeInorder(node)
  parentStack = empty stack
  while (not parentStack.isEmpty() or node ≠ null)
    if (node ≠ null)
      parentStack.push(node)
      node = node.left
    else
      node = parentStack.pop()
      visit(node)
      node = node.right
```

```
iterativePostorder(node)
  parentStack = empty stack  
  lastnodevisited = null 
  while (not parentStack.isEmpty() or node ≠ null)
    if (node ≠ null)
      parentStack.push(node)
      node = node.left
    else
      peeknode = parentStack.peek()
      if (peeknode.right ≠ null and lastnodevisited ≠ peeknode.right) 
        /* if right child exists AND traversing node from left child, move right */
        node = peeknode.right
      else
        visit(peeknode)
        lastnodevisited = parentStack.pop() 
```

##Related Concept
###Binary Search Tree
Let x be a node in a binary search tree. If y is a node in the left subtree of x, then y.key ≤ x.key. If y is a node in the right subtree of x, then y.key ≥ x.key.

NOTE: Node deletion

##Heap


##Graph Algorithms

###Undirected Graphs
Let G = (V, E) be a graph with vertex set V and edge set E. A subgraph of G is a graph G' = (V', E') where
1. V' is a subset of V.
2. E' consists of edges (v, w) in E such that both v and w are in V'.
If E' consists of all edges (v, w) in E, such that both v and w are in V', then G' is called an induced subgraph of G.

|Problems|Alogrithms|Complexity|Application|
|:----|:----|:----|
|Minimum-Cost Spanning Trees|Prim's Algorithm|O(n2)<br/>If e is much less than n2, Kruskal's algorithm is superior, although if e is about n2, we would prefer Prim's algorithm.
||Kruskal's Algorithm|
|Depth-First Search|
|Breadth-First Search|||Find a path between verteices
|Articulation Points and Biconnected Components|
|Graph Matching|


####Prim's Algorithm

Prim's algorithm begins with a set U initialized to {1}. It then "grows" a spanning tree, one edge at a time. At each step, it finds a shortest edge (u, v) that connects U and V-U and then adds v, the vertex in V-U, to U. It repeats this step until U = V.

```
procedure Prim ( G: graph; var T: set of edges );
     { Prim constructs a minimum-cost spanning tree T for G } 
     var
          U: set of vertices;
          u, v: vertex; 
     begin
          T:= Ø;
          U := {1};
          while U ≠ V do begin
               let (u, v) be a lowest cost edge such that 
                    u is in U and v is in V-U;
               T := T ∪ {(u, v)};
￼          ￼     U := U ∪ {v} 
          end
     end; { Prim }
```

O(n2)

####Kruskal's Algorithm

Suppose again we are given a connected graph G = (V, E), with V = {1, 2, . . . , n} and a cost function c defined on the edges of E. Another way to construct a minimum-cost spanning tree for G is to start with a graph T = (V, Ø) consisting only of the n vertices of G and having no edges. Each vertex is therefore in a connected component by itself. As the algorithm proceeds, we shall always have a collection of connected components, and for each component we shall have selected edges that form a spanning tree.

We can implement this algorithm using sets and set operations discussed in Chapters 4 and 5. First, we need a set consisting of the edges in E. We then apply the DELETEMIN operator repeatedly to this set to select edges in order of increasing cost. The set of edges therefore forms a priority queue, and a partially ordered tree is an appropriate data structure to use here.

We also need to maintain a set of connected components C. The operations we apply to it are:
1. MERGE(A, B, C) to merge the components A and B in C and to call the result either A or B arbitrarily.†
2. FIND(v, C) to return the name of the component of C of which vertex v is a member. This operation will be used to determine whether the two vertices of an edge are in the same or different components.
3. INITIAL(A, v, C) to make A the name of a component in C containing only vertex v initially.


```
procedure Kruskal ( V: SET of vertex; E: SET of edges; var T: SET of edges );
	var	
		ncomp: integer; { current number of components }
		components: MFSET; { the set V grouped into a MERGE-FIND set of components }
		u, v: vertex;
		e: edge;
		nextcomp: integer; { name for new component } 
		ucomp, vcomp: integer; { component names }
	begin
		MAKENULL(T); 
		MAKENULL(edges);
		nextcomp := 0;
		ncomp := number of members of V; 
		for v in V do begin { initialize a component to contain one vertex of V }
			nextcomp := nextcomp + 1;
			INITIAL( nextcomp, v, components) 
		end;
		for e in E do { initialize priority queue of edges } 
			INSERT(e, edges);
		while ncomp > 1 do begin { consider next edge } 
			e := DELETEMIN(edges);
			let e = (u, v);
			ucomp := FIND(u, components);
			vcomp := FIND(v, components); 
			if ucomp <> vcomp then begin { e connects two different components } 
				MERGE (ucomp, vcomp, components); 
				ncomp := ncomp - 1;
				INSERT(e, T)
			end 
		end
	end; { Kruskal }
```

####Breadth First Search
```
void search(Node root) {
     Queue queue = new QueueQ;
     root.visited = true;
     visit(root);
     queue.enqueue(root); // Add to end of queue
     while (!queue.isEmpty()) {
          Node r = queue.dequeueQ; // Remove from front of queue
          foreach (Node n in r.adjacent) {
               visit(n);
               n.visited = true;
               queue.enqueue(n)
          }
     }
}
```

####Depth First Search
```
void search(Node root) {
     if (root == n u ll) return; visit(root);
     root.visited = true;
     foreach (Node n in root.adjacent) {
          if (n.visited == false) {
          search(n);
     }
}
```
###Directed Graphs
Directed Graph ADT's

common operations:

read the label of a vertex or arc

insert or delete vertices and arcs

navigate by following arcs from tail to head

1. FIRST(v) returns the index for the first vertex adjacent to v. The index for the null vertex Λ is returned if there is no vertex adjacent to v.
2. NEXT(v, i) returns the index after index i for the vertices adjacent to v. Λ is returned if i is the last index for vertices adjacent to v.
3. VERTEX(v, i) returns the vertex with index i among the vertices adjacent to v.

|Problems|Alogrithms|Complexity|
|----|----|----|
|The Single Source Shortest Paths Problem|Dijkstra's Algorithm|O(elogn)|
|The All-Pairs Shortest Paths Problem|Floyd's Algorithm|
||Warshall's algorithm|
|Topological Sort||
|Strong Components|

####Dijkstra's algorithm
Dijkstra's algorithm: maintaining a set S of vertices whose shortest distance from the source is already known.

```
procedure Dijkstra;
{ Dijkstra computes the cost of the shortest paths
from vertex 1 to every vertex of a directed graph }
begin
(1)     S := {1};
(2)     for i := 2 to n do
(3)          D[i] := C[1, i]; { initialize D }
(4)     for i := 1 to n-1 do begin
(5)           choose a vertex w in V-S such that 
               D[w] is a minimum;
(6)          add w to S;
(7)          for each vertex v in V-S do
(8)               D[v] := min(D[v], D[w] + C[w, v])
     end
end; { Dijkstra }
```



####Topological Sort

Topological sort is a process of assigning a linear ordering to the vertices of a dag so that if there is an arc from vertex i to vertex j, then i appears before j in the linear ordering.

Topological sort can be easily accomplished by adding a print statement after line (4) to the depth-first search procedure in Fig. 6.24:

```
procedure topsort ( v: vertex );
     { print vertices accessible from v in reverse topological order } 
     var
          w: vertex; 
     begin
          mark[v] := visited;
          for each vertex w on L[v] do
               if mark[w] = unvisited then 
                    topsort(w) ;
          writeln(v) 
     end; { topsort }
```