## topological sort


## shortest path with negative edges


## longest path


## reduction 归约
- e.g.  DAG-LPT reduces to DAG-SPT  
- $A≤_mB$  B at least as difficult as A (A reduces to B)
another e.g.  :
### IND-SET problem
given a graph, find k nodes that are not adjoined.

### 3-SAT problem
given a set of 3-arguments disjunction clauses, find a valueset of args make all clauses true;
$$(x1 + x2 + !x3)(x1 + !x1 + x1)(x2 + x3 + x4) = 1$$
how to solve 3-SAT?
consider draw a graph, each clause form a small triangle, in total k triangles. then link every group of  opposite values(e.g.   x1 and !x1).
__find k nodes that are not adjoined in this graph__
![[Pasted image 20260410183306.png]]
at this point we can say, 3SAT reduces to IND-SET.

## decomposition





