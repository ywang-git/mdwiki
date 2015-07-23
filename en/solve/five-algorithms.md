#Five Common Algorithms
|Algorithms|Description|Example Usages|
|----|----|----|
| Divide and Conquer | Breaking a problem of size _n_ into smaller problems in such a way that from solutions to the smaller problems we can easily construct a solution to the entire problem. |Merge Sort, Binary Search Tree|
|Dynamic Programming||1. Count number of combinations (ways of walking up a staircase, number of structurally unique BST's).<br/>2. Find optimal solution in combinations (best profit single sell, minimum coins change making).<br/>
|Greedy Algorithms|Find local optimistic solution (but not necessary to be global optimistic one).|Change making
|Backtracking Alogrithms|traverse serch tree in depth-first order:<br/>At each node c, the algorithm checks whether c can be completed to a valid solution. ...|8 Queen problem|
|Branch and Bound Algrithms||Integer programming<br/>Nonlinear Programming<br/>Travelling salesman<br/>0/1 knapsack problem
||||
|Local Search Algorithm|||

##Dynamic Programming
###my notes:
####what is the difference between "stock sale" problem and "matrix-chain multiplication"?

1. When using bottom-up approach to construct optimal solutions for "stock sale" problem, if we find the final solution at index j (0 <=j < n), we do not need to care about any subproblem of [j + 1 .. n]. However with "matrix-chain multiplication" (or "boolean satisfaction") problem, we do need to combine the result for [j + 1 .. n]. That is why when we track the partial result of subproblems (memoization), we need to track all of them.
2. Meanwhile, solving "matrix-chain multiplication" problem and "rod cutting" problem also involves optimal solutoin to all it sub-range.

"stock sale" prolem is actually kind of special as we do not need the optimal solution from the subrange to construct the final solution. Similar problems include: "least step to reach other side".

The optimal solution of "stock sale" problem only depend on the optimal subproblem itself; "rod cutting" depend further on the solution of subtproblems of subproblem; "matrix-chain multiplication" problem's subproblem has an extra property as each subproblem has a unique property besides its size.


|Problems|Number of Subproblems|Number of Choices for Each Subproblem| Complexity|
|----|----|----|----|
|Stock sale|O(n)|O(1)|O(n)|
|Cutting Rod|O(n)|O(n)|O(n2)|
|Matrix-chain Multiplication|O(n2)|O(n)|O(n3)|


####divide subproblem

When dividing subproblem, we divide them in the solution's space, which is not necessarily related to the actuall space of the parameters.

However, there are two cases when we deal with the solutions to the subproblems:

1. we use the subproblem's solution to construct the final solution. in this case, a solution to the subproblem, can be only part of the final solution. (rod cutting, matrix chain multiplication, etc.)
2. the solution to the subproblem could be the final solution, we solve the subproblem, and compare with the best solution we cached so far, to decide whether it is better. normally besides the solution to the subproblems, we need to caches extra data to get to the solution to subproblems. such data usually describe the characteristics of the input data, such as the lowest stock price, the longest increasing sequence, etc. 




####what to cache
in some problems, such as [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/), you don't construct an optimal solution based on any previous solution. in such cases, variables we are caching are not solutions for subproblems.



###elements of dynamic programming

> Recall that a problem exhibits optimal substructure if an optimal solution to the problem contains within it opti- mal solutions to subproblems. 
> 
> 1. You show that a solution to the problem consists of making a choice
> 2. You suppose that for a given problem, you are given the choice that leads to an optimal solution
> 3. Given this choice, you determine which subproblems ensue and how to best characterize the resulting space of subproblems
> 4. You show that the solutions to the subproblems used within an optimal solution to the problem must themselves be optimal by using a “cut-and-paste” tech- nique.


> Optimal substructure varies across problem domains in two ways:
> 
> 1. how many subproblems an optimal solution to the original problem uses, and
> 2. how many choices we have in determining which subproblem(s) to use in an optimal solution.


####Subtleties

1. Independent of subproblems

2. overlapping of subproblems

	> In contrast, a problem for which a divide-and- conquer approach is suitable usually generates brand-new problems at each step of the recursion. Dynamic-programming algorithms typically take advantage of overlapping subproblems by solving each subproblem once and then storing the solution in a table where it can be looked up when needed, using constant time per lookup.


##Dynamic Programming v.s. Greeday Algorithm
> One major difference between greedy algorithms and dynamic programming is that instead of first finding optimal solutions to sub- problems and then making an informed choice, greedy algorithms first make a “greedy” choice—the choice that looks best at the time—and then solve a resulting subproblem, without bothering to solve all possible related smaller subproblems.

##Backtracking

P as a parameter and should do the following:

1. root(P): return the partial candidate at the root of the search tree.
2. reject(P,c): return true only if the partial candidate c is not worth completing.
3. accept(P,c): return true if c is a solution of P, and false otherwise.
4. first(P,c): generate the first extension of candidate c.
next(P,s): generate the next alternative extension of a candidate, after the extension s.
5. output(P,c): use the solution c of P, as appropriate to the application.

The backtracking algorithm reduces then to the call bt(root(P)), where bt is the following recursive procedure:

```
procedure bt(c)
  if reject(P,c) then return
  if accept(P,c) then output(P,c)
  s ← first(P,c)
  while s ≠ Λ do
    bt(s)
    s ← next(P,s)
```    

##Branch and Bound

* Using a heuristic, find a solution xh to the optimization problem. Store its value, B = f(xh). (If no heuristic is available, set B to infinity.) B will denote the best solution found so far, and will be used as an upper bound on candidate solutions.

* Initialize a queue to hold a partial solution with none of the variables of the problem assigned.
* Loop until the queue is empty:
	* Take a node N off the queue.
	* If N represents a single candidate solution x and f(x) < B, then x is the best solution so far. Record it and set B ← f(x).
	* Else, branch on N to produce new nodes Ni. For each of these:
		* If g(Ni) > B, do nothing; since the lower bound on this node is greater than the upper bound of the problem, it will never lead to the optimal solution, and can be discarded.
		* Else, store Ni on the queue.
		
##Loacal Search
1. Start with a random solution.
2. Apply to the current solution a transformation from some given set of transformations to improve the solution. The improvement becomes the new "current" solution.
3. Repeat until no transformation in the set improves the current solution. The resulting solution may or may not be optimal. In principle, if the "given set of transformations" includes all the transformations that take one solution and replace it by any other, then we shall never stop until we reach an optimal solution. But then the time to apply (2) above is the same as the time needed to examine all solutions, and the whole approach is rather pointless.


##Reference
1. [Five Common Algorithms (Chinese)](http://c.chinaitlab.com/special/algorithm/)